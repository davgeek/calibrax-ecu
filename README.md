# CalibraX

CalibraX is a Windows desktop application for tuning JTEC engine control units
(ECUs) used in 1996-2004 Chrysler, Jeep, and Dodge vehicles (68HC16-based,
communicating over J2534/SCI). It lets you read and write the ECU's flash memory,
edit calibration tables and scalars with the correct addresses/scales for your
specific part number, compare edits against the original file, undo changes, and
visualize tables as curves or 3D surfaces.

![CalibraX table editor](docs/screenshot-main-editor.png)

## Features

- **Read ECU flash** over a J2534 pass-thru interface, or open a previously saved
  project file. Choose whether the controller is a JTEC or a JTEC+ before reading.
- **Table and scalar editors** with correct units, scaling, and axis breakpoints
  per part number — no hand-picked offsets.
- **Compare & Undo** against the original flash image while editing, with a
  per-table count of what changed.
- **Curve and 3D surface views** for any table, alongside the standard grid.
- **Logger**: a dedicated screen for live engine data, separate from the table
  editor.
  - View real-time parameters (RPM, MAP, coolant temp, fuel trims, and more)
    while connected to the vehicle, and record them to a CSV log.
  - Log tables fill in live as you drive: short and long term fuel trim, spark
    advance, and injector pulse width, each averaged by RPM and MAP — the same
    layout as the base fuel table, so a rich or lean cell is easy to spot.
  - Open a previously recorded log to browse it: a chart of every channel
    against time (zoom, pan, scrub), and the same log tables filled from the
    whole file or filled live as you play it back.

  ![Logger: live data and log tables](docs/screenshot-logger-live.png)
  ![Logger: a recorded log's chart](docs/screenshot-logger-chart.png)
  ![Logger: log tables from a recorded file](docs/screenshot-log-tables.png)

- **Trouble codes**: read stored, pending, and one-trip fault codes, named from
  your calibration when possible. 🔒 *clearing codes requires a license*
- **Apps**: extend CalibraX with additional tools that run inside the app — the
  first one available is a byte-level Hex Editor for the flash and other
  captured memory images. 🔒 *some apps require a separate license*
- **Growing vehicle coverage**: support for new part numbers is added regularly.
- **Automatic update check**: the app checks this repository on startup and
  points you to the latest release when one is available.
- **Write ECU flash / checksum repair** 🔒 *requires a license* — see
  [Licensing](#licensing) below.

Everything above except the parts marked 🔒 works with no license at all.

## Supported vehicles

| ECU | Year | Vehicle | Engines | View & edit calibration | Read / write ECU |
| --- | ---- | ------- | ------- | ----------------------- | ---------------- |
| JTEC | 1996 | Jeep Cherokee (XJ) | 2.5L, 4.0L | ✅ | ⚠️ Untested |
| JTEC | 1996 | Jeep Grand Cherokee (ZJ/ZG) | 4.0L, 5.2L | ✅ | ⚠️ Untested |
| JTEC | 1997 | Jeep Cherokee (XJ) | 4.0L | ✅ | ✅ |
| JTEC | 1997 | Jeep Grand Cherokee (ZJ/ZG) | 4.0L, 5.2L | ✅ | ✅ |
| JTEC | 1997 | Dodge Ram (BR) | 5.2L | ✅ | ✅ |
| JTEC | 1998 | Jeep Cherokee (XJ) | 4.0L | ✅ | ✅ |
| JTEC | 1998 | Jeep Grand Cherokee (ZJ/ZG) | 4.0L, 5.2L, 5.9L | ✅ | ✅ |
| JTEC+ | 1999 | Jeep Cherokee (XJ) | 2.5L, 4.0L | ✅ | ⚠️ Untested |
| JTEC+ | 1999 | Jeep Grand Cherokee (WJ) | 4.0L, 4.7L V8 | ✅ | ⚠️ Untested |
| JTEC+ | 1999 | Dodge Ram, Dakota, Durango and vans | 2.5L, 3.9L, 5.2L, 8.0L V10 | ✅ | ⚠️ Untested |
| JTEC+ | 2000 | Dodge Ram, Dakota, Durango and vans | 2.5L, 3.9L, 4.7L, 5.2L, 8.0L V10 | ✅ | ⚠️ Untested |
| JTEC+ | 2001 | Jeep Cherokee (XJ) | 4.0L | ✅ | ⚠️ Untested |
| JTEC+ | 2001 | Jeep Wrangler (TJ) | 2.5L, 4.0L | ✅ | ⚠️ Untested |
| JTEC+ | 2001 | Jeep Grand Cherokee (WJ) | 4.0L, 4.7L V8 | ✅ | ✅ |
| JTEC+ | 2001 | Dodge Ram, Dakota, Durango and vans | 2.5L, 3.9L, 4.7L, 5.2L, 8.0L V10 | ✅ | ⚠️ Untested |
| JTEC+ | 2001 | Dodge Viper | 8.0L V10 | ✅ | ⚠️ Untested |

Coverage is by part number; more vehicles and part numbers are added regularly.
Writing to the ECU requires a license (see [Licensing](#licensing)).

## Download

Grab the latest build from the [Releases](../../releases) page. Each release is a
portable, self-contained `.exe` for Windows (win-x86) — no separate .NET runtime
install required. Unzip and run `CalibraX.exe`.

### Windows SmartScreen warning

Windows may show a "Windows protected your PC" prompt the first time you run the
downloaded `.exe`. This is expected: the build isn't signed with a paid code-signing
certificate, so it has no publisher reputation with Microsoft yet. Click **More
info**, then **Run anyway**. You can always verify what you're running by comparing
the file's SHA256 hash against the value shown on the release page, or by reading
the source in the private development repository.

## Licensing

CalibraX is free to download and try: you can open a project, browse calibrations,
and edit tables/scalars without a license. **Writing a checksum-valid flash back to
a real ECU, and some optional apps, require a license**, since a bad checksum can
leave the ECU unable to boot.

To purchase one, contact the developer. You'll receive an additional file to drop
into the app's `definitions` folder that unlocks the licensed feature immediately —
no account, activation server, or restart required.

## Supported interfaces

CalibraX is compatible with J2534 pass-thru devices. Real-world behavior varies
device to device, so here's what's actually been tried:

| Interface           | Status        |
| -------------------- | ------------- |
| Scanmatik 2 Pro (SM2 Pro) | ✅ Validated |
| Autel MaxiFlash / V200    | ⚠️ Untested |
| Tactrix OpenPort 2.0      | ⚠️ Untested |
| Drew Technologies Mongoose Pro | ⚠️ Untested |
| OBDLink MX+ (J2534 mode)  | ⚠️ Untested |

"Untested" doesn't mean unsupported — it means nobody has confirmed it against a
real ECU yet. If you try one of these (or another J2534 device) and it works (or
doesn't), open an issue so this list can be updated.
