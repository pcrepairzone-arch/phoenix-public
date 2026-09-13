# Phoenix RISC OS — public view

Phoenix is a bare-metal **AArch64 RISC-OS-compatible kernel** for the Raspberry
Pi 4, CM4, Pi 5 and CM5. It boots to a real `*` supervisor, runs BASIC, reads
FileCore discs off NVMe/USB/SD, does networking and NTP, and loads real 64-bit
RISC OS modules from disc.

**The kernel source is not public yet.** This repository is the public-facing
part of the project: what we have learned, and a map of how the thing is built.

---

## What's here

| | |
|---|---|
| **[Developer bulletins](docs/bulletins/)** | What actually bites when you port RISC OS code to 64-bit, and the working habits that surface those bugs early. Written for anyone using the riscos64 toolchain, not only for Phoenix. |
| **[Architecture map](docs/architecture/)** | An interactive browser over Phoenix's structure — layers, files, functions and how they relate. Generated from the source, so it stays honest about what actually exists. |

Both are published at **https://pcrepairzone-arch.github.io/phoenix-public/**

---

## The bulletins

**No. 1 — [Porting to 64-bit RISC OS: what actually bites](docs/bulletins/01-porting-to-64-bit-risc-os.html)**

Three parts: the toolchain-level hazards (sentinels that sign-extend, flags that
never reach a C caller, struct padding that moves every field, alignment,
relocations), Phoenix-specific notes, and the debugging method that found them.

Every technical claim in it is measured on real hardware or read out of the
source. Where something is a hypothesis rather than a measurement, it says so.

---

## The architecture map

The map is generated from the private source tree, so it shows **structure and
intent without shipping code**. Each node carries a name, a path, a plain-English
summary, tags and a size — there are no source bodies in it.

It is regenerated periodically. `docs/graph/meta.json` records exactly when, and
against which commit — **check that date before trusting the map**, the same way
you would check a build stamp. See [docs/graph/README.md](docs/graph/README.md)
for how it is produced.

---

## Corrections

**Please open an issue.** The bulletins invite correction and mean it — two
claims in No. 1 contradict things this project itself wrote earlier, and one of
those was caught on the day of publication.

A correction is more useful to us than a compliment, and an issue is better than
an email because everyone else gets to see it too.

There is an issue template for corrections. If you would rather not use GitHub,
the contact details are in the bulletin footer.

---

## Open questions

Some problems are bigger than one project, and solving them privately is worse
than solving them once in the open. Those are filed as issues tagged
**`open-question`** — the current one is how a Wimp library ought to represent a
fixed 32-bit OS block in C at LP64, which currently blocks work in more than one
codebase. Views welcome from anyone who has hit it.

---

## Licence

- **Prose, bulletins and documentation** — [CC BY 4.0](LICENCE.md). Quote it,
  translate it, put it in your own wiki; just say where it came from.
- **Code snippets and the map viewer** — MIT.
- **Phoenix itself** — MIT.

See [LICENCE.md](LICENCE.md).

---

## Credits

The RISC OS 64-bit toolchain, and a great many of the modules Phoenix loads, are
Charles Ferguson's (gerph) work. Phoenix would not be reachable without it.

Andrew Youll's [desklib32](https://github.com/adyoull/desklib32) debugging notes
prompted the alignment investigation in Bulletin No. 1 — worth reading if you
are porting anything to 32-bit Norcroft.
