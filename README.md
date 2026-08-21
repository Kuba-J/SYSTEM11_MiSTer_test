<p align="center">
  <img src="art/XelaNotPu-LogoTransparent-GithubSocial.png" alt="SYSTEM11 MiSTer banner" width="100%">
</p>
# Namco System 11 for MiSTer

FPGA implementation of the [Namco System 11](https://en.wikipedia.org/wiki/Namco_System_11) arcade board for the [MiSTer platform](https://github.com/MiSTer-devel/Main_MiSTer/wiki).

Namco System 11 (1994) is an arcade board built around Sony PlayStation technology: an R3000A-compatible MIPS CPU, a System 11 GPU (CXD8538Q) with 2 MB VRAM, and main RAM — paired with Namco-specific hardware that has no PlayStation equivalent: banked game ROM in place of a CD drive, a Namco C76 (Mitsubishi M37702) MCU handling sound and cabinet I/O, the Namco C352 32-voice PCM sound chip, and per-game KEYCUS protection chips. This core implements all of the above, including the C76 coprocessor and C352 sound.

The core is derived from the excellent [PSX_MiSTer](https://github.com/MiSTer-devel/PSX_MiSTer) core by **Robert Peip (FPGAzumSpass)**, which provides the CPU, GPU, GTE, DMA, and memory subsystem foundation.

## New in 20260818

**Core renamed:** the release bitstream is now `Arcade-SYSTEM11_20260818.rbf` and every MRA
resolves `<rbf>SYSTEM11</rbf>` — the interim "XN" prefix is retired. If you installed an
earlier build, delete any old `XNSYSTEM11*.rbf` from `_Arcade/cores/` and replace your MRAs
with this release's set (the old MRAs point at the old name). The bitstream content is
identical to the verified 20260816 build (same MD5).

## Games

Primary titles (one per game; other regions/revisions live in `releases/_Arcade/_alternatives/_<Game>/`):

- Tekken (TE2 Ver.C)
- Tekken 2 Ver.B (TES2-VER.D)
- Soul Edge Ver. II (SO4-VER.C)
- Xevious 3D/G (XV32-VER.B)
- Dunk Mania (DM2-VER.C)
- Prime Goal EX (PG1-VER.A)
- Dancing Eyes (DC2-VER.B)
- Star Sweep (STP1-VER.A)
- Kosodate Quiz My Angel 3 (KQT1-VER.A)
- Pocket Racer (Japan PKR1-VER.B)
- Point Blank 2 (World GNB2-VER.A)
- Gunbarl (Japan GNB1-VER.A)

*(+20 alternate region/revision MRAs under `releases/_Arcade/_alternatives/`.)*
**Family Bowl** remains out of scope

### CRT Adjust (analog geometry)

Includes **CRT Adjust** (OSD → Video & Audio): H-Size / H-Position / V-Shift for analog CRTs. Default **Off** (HDMI/analog untouched); turn On when driving a CRT off the analog DAC. H-Size is invisible on HDMI by design.

### DB9 / SNAC8 joystick support

**UserIO Joystick** OSD option enables DB9MD Megadrive (3/6-button) and DB15 Neo-Geo/Supergun joystick input via splitters designed by Antonio Villena (compatible with the MiSTer-DB9 project's DB9MD 3-button and 6-button connectors, and the DB15 Neo-Geo standard). Up to 2 players supported.

**OSD navigation from the stick** requires the [MiSTer-DB9 project's Main_MiSTer fork](https://github.com/MiSTer-devel/Main_MiSTer) with a compatible `menu.rbf`. In-game input works with stock MiSTer firmware.

## Controls

Standard System 11 controls (up to 4 buttons in the P1 register, plus coin/start). Labels come from each MRA's `<buttons>` tag. Supports keyboard, joystick, and UserIO Joystick (DB9/DB15) via the OSD option above.

## Install

Copy the `_Arcade/` folder onto your SD card's root folder: this places the `.mra` files (and `_alternatives/`) directly in `_Arcade/`, and `cores/Arcade-SYSTEM11_20260818.rbf` in `_Arcade/cores/`. **Remove stale `XNSYSTEM11_*` cores and MRAs from earlier builds** — they reference the retired name. **Provide your own romsets — nothing copyrighted is included.** 

MRAs reference romsets by name only. The MRA names are self-descriptive).

## Credits & attribution

This core stands on the work of others, gratefully acknowledged:

- **PSX_MiSTer** by **Robert Peip (FPGAzumSpass)** — the PlayStation core this System 11 core derives from, providing the R3000A CPU, GPU, GTE, DMA, and memory subsystem.
- **The MiSTer project** and its framework (`sys/`) — Alexey Melnikov (**Sorgelig**) and the MiSTer-devel contributors.
- **MiSTer-CRT-Adjust** — rmonic79 (with Andrea Bogazzi) — the core-side analog CRT geometry module used for H-Size / H-Position / V-Shift.
- **MiSTer-DB9 project** — Aitor Pelaez (**NeuroRulez**), Victor Trucco, Fernando Mosquera, Timothy Redaelli, and Antonio Villena (DB9 splitter hardware design) — the joystick adapter and controller framework.
- **C76 M37702 / C352 / KEYCUS** — original FPGA re-implementations of System 11's sound and security hardware.
- **The MAME project** — the hardware documentation and reference behavior used to develop System 11 board support (per-manufacturer boot ROM, CAT702 security, ROM banking, NVRAM/EEPROM) as an independent re-implementation.
- **System 11 hardware and chipset re-implementations** — **XelaNotPu**: the System 11 hardware (per-manufacturer boot ROM, CAT702 security, ROM banking, NVRAM/EEPROM), the sound-chip re-implementations (C76 M37702, C352), and the XN pause-overlay artwork and README banner.

## License

This core is a combined/derived work licensed under the **GNU General Public License, version 3 or later (GPLv3-or-later)**.

It builds on [PSX_MiSTer](https://github.com/MiSTer-devel/PSX_MiSTer) (Robert Peip) and the MiSTer framework. Several files in the build tree — the MiSTer `sys/` HPS-I/O, SD-card, scandoubler and DDR-service modules, and the SDRAM/DDR memory controllers — are licensed **GPL version 3 or later**. Combining GPLv2-or-later code with GPLv3-or-later code yields a work that can only be conveyed under GPLv3-or-later, so that is the license of this core as a whole. The full texts of both licenses are included (`COPYING.GPL2`, `COPYING.GPL3`); GPLv2-or-later files remain individually available under their own terms.

## Legal

**No ROMs.** This repository contains no game ROMs and no copyrighted game data, and it provides no links or instructions for obtaining them. To use this core you must supply your own ROM dumps, made from original hardware or media that you legally own, where and to the extent your local law permits.

**Trademarks.** "Namco", "System 11", "Tekken", and related names and logos are trademarks or registered trademarks of Bandai Namco Entertainment Inc. and/or their respective owners. "PlayStation" is a trademark of Sony Interactive Entertainment Inc. This project is not affiliated with, endorsed by, or sponsored by Bandai Namco, Sony Interactive Entertainment, or any other rights holder. Such names are used here in a purely nominative and descriptive manner, solely to identify the hardware being re-implemented.

**Purpose.** This is an independent, non-commercial hardware-preservation and interoperability project. The FPGA logic is an original re-implementation of the System 11 board's behavior, developed from observation and from publicly available documentation and references (including the MAME project's hardware documentation); it contains no proprietary source code from the original manufacturers.

**Security-chip emulation.** Namco System 11 boards used per-game KEYCUS chips (C406, C409, …) as a protection measure. This core re-implements that logic for interoperability and preservation, in the same manner as MAME and comparable FPGA cores. The KEYCUS is a small challenge/response algorithm rather than stored key data, so no manufacturer key material is embedded in the bitstream. Laws such as the U.S. DMCA §1201 address circumvention of technological protection measures; whether and how they apply to this kind of preservation/interoperability use can depend on your jurisdiction and circumstances. Users are responsible for their own compliance.

**User responsibility.** Users are solely responsible for ensuring that their use of this core — including the acquisition and use of any ROM images — complies with copyright law and all other applicable laws in their jurisdiction.

**No warranty.** As set out in sections 15–16 of the GNU General Public License (v3) and the equivalent clauses of v2: THIS PROGRAM IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. IN NO EVENT WILL ANY COPYRIGHT HOLDER OR CONTRIBUTOR BE LIABLE TO YOU FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THIS PROGRAM, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.
