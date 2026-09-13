# Text to paste as the first `open-question` issue

**Create it, apply the `open-question` label, and pin it.** Then link it from
Bulletin No. 1's closing section in place of the "we'd like to hear it" line.

---

**Title:** How should a Wimp library represent a fixed 32-bit OS block in C at LP64?

**Labels:** `open-question`

---

A Wimp window block is a fixed run of 32-bit words, defined by the OS. The
moment a C struct describing one contains a pointer, the struct changes size at
LP64 and every field after that pointer moves.

This is not hypothetical and it is not one project's problem:

- **DeskLib, from the 32-bit side.** A group of `unsigned int : 1` bitfields in
  `wimp_colourflags` pushed the struct from 8 bytes to 12 under a modern
  Norcroft, shifting `numicons`/`icons` by 4. Template loading then requested a
  bogus allocation and the application died on launch with *"not enough memory
  to copy template"*. Documented by Andrew Youll in
  [desklib32](https://github.com/adyoull/desklib32).
- **riscos64-oslib, from the 64-bit side.** Its structs are unusable at LP64 for
  the same underlying reason.
- **Us.** It currently blocks a WindowScroll port, and it stands between the
  community and a 64-bit DeskLib.

Two people found it from opposite directions — 32-bit Norcroft and 64-bit GCC —
and hit the same wall.

## The question

Given a block whose layout is fixed by the OS as N 32-bit words, what should the
C representation be?

Options we can see, none obviously right:

1. **Explicit-width fields only, no pointers.** Store offsets or handles where a
   pointer would go, and resolve them through an accessor. Correct at both
   widths; costs ergonomics and touches every call site.
2. **A raw `uint32_t[]` plus named accessors.** Layout cannot drift because
   there is no struct to pad. Verbose, and loses type checking.
3. **Keep the struct, add `_Static_assert` on every offset and size**, and fix
   what fails. Cheapest to adopt; does nothing about the pointer that has to
   live somewhere.
4. Something better that somebody has already done and we have not seen.

## Why we are asking rather than deciding

Whoever answers this first effectively sets a convention. If several projects
each solve it privately we end up with **incompatible representations in
different libraries**, which is materially worse than the current state of
nobody having solved it — a caller would then have to know which library's idea
of a window block it was holding.

We would much rather it were settled once, in the open, by the people who
maintain these libraries.

**If you have already solved this in your own code, that is the most useful
possible reply** — including if your answer is "we did option 2 and regret it".

## Related

- Bulletin No. 1, Part 1 §3 (LP64 struct aliasing) and §4 (a pointer resizing an
  external format) describe the same failure mode in other places.
- This blocks 64-bit DeskLib work, which is separately gated on DeskLib's own
  long-standing intention to relicence to MIT.
