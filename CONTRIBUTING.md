# Corrections and contributions

The most valuable thing you can send us is **a correction**.

Bulletin No. 1 already contains two entries that contradict what this project
itself wrote earlier, and a third claim was caught and fixed on the day it was
published. That is not a sign the process is broken — it is the process. A
bulletin nobody corrects is a bulletin nobody is reading.

---

## Telling us something is wrong

**Open an issue.** There is a template for it. You do not need to be polite
about it, and you do not need to be certain — "I think this is wrong because…"
is a perfectly good issue.

What helps most, in rough order:

1. **What you measured**, and on what. A command and its output beats a
   description of the output.
2. **Which claim** — quote the sentence, or link the anchor.
3. **Which platform / toolchain version**, if it might matter. A lot of these
   findings are version-specific and we may simply be on a different one.

What we will do: check it against the source or the hardware, fix the bulletin,
and credit you unless you would rather we didn't. Corrections are recorded in
the git history so the change is visible, not silently swapped in.

---

## Open questions

Issues tagged **`open-question`** are problems we have not solved and do not
think we should solve alone — usually because whoever answers first effectively
sets a convention for everyone else, and three projects each answering privately
is worse than none answering.

These are open for anyone to weigh in on, including "we already did this and
here is what we chose". Especially that.

---

## Adding to the bulletins

If you have a hazard worth recording, an issue describing it is welcome and a
pull request is welcome too. Two things we hold ourselves to and would ask of
anything added:

- **Say whether it is measured or inferred.** Both are useful; conflating them
  is not. "A probable answer stated as a known one is still a wrong
  attribution."
- **Give the symptom, not just the cause.** People arrive at these documents via
  the symptom — the error message, the crash, the wrong pixel. If the entry
  cannot be found from the symptom, it will not be found.

---

## What this repository is not

It is not the Phoenix source tree, which is not public yet. Issues about the
kernel's behaviour are welcome but we may not be able to show you the code that
causes them.

It is not a support channel for RISC OS generally. For that, the
comp.sys.acorn.programmer newsgroup and the ROOL forums have far more people and
far more history than we do.

---

## Tone

This project owes a great deal to a small number of people maintaining a large
amount of software in their spare time. Where the bulletins describe a defect in
someone else's tool, they are describing a thing that will cost a reader a day,
not making a complaint — and they say what has already been reported upstream.
Please keep that spirit in anything you add.
