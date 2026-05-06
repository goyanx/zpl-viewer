# zpl-viewer

Desktop ZPL (Zebra Programming Language) viewer and printer emulator.

`zpl-viewer` listens on a JetDirect-style TCP socket (default `9100`) and renders incoming ZPL using Labelary.

It now supports **multi-label navigation** for ZPL batches (`^XA ... ^XZ` repeated): use the **Prev** and **Next** buttons to move label-by-label.

![alt text](zpl_viewer.png)

## Requirements

- Windows desktop
- Internet access to `api.labelary.com` (for rendering)
- Optional: Lazarus/FreePascal if you want to build from source

## Quick Start (prebuilt EXE)

1. Download the latest Windows release artifact.
2. Extract and run `zplview.exe`.
3. In your label source app (or Zebra Designer), send ZPL to:
   - Host: `127.0.0.1`
   - Port: `9100`
4. `zpl-viewer` receives the job and renders it.

## Build From Source

### Option A: Lazarus IDE

1. Open `zplview.lpi` in Lazarus.
2. Build/Run the project from the IDE.

### Option B: command line (if `lazbuild` is installed)

```powershell
lazbuild zplview.lpi
```

## Windows Printer Setup (for apps that print to a printer queue)

If your app expects a printer instead of raw socket output:

1. Add a printer in Windows.
2. Choose a TCP/IP/JetDirect style port (or Standard TCP/IP Port).
3. Set printer address to `127.0.0.1`.
4. Set port to `9100`.
5. Use any Zebra-compatible driver your workflow expects.
6. Print from your app to that printer.

This routes the print stream to `zpl-viewer` locally.

## Firewall

If needed, allow inbound TCP `9100` on your machine.

## App Setup (inside zpl-viewer)

Open `File -> Settings` and configure:

- DPI (`152`, `203`, `300`, `600`)
- Rotation (`0`, `90`, `180`, `270`)
- Label Width/Height (inches)
- Bind address / TCP port (`0.0.0.0:9100` default)
- Optional:
  - save rendered PNG
  - save raw ZPL
  - print/reprint behavior

## Manual Render

You can also paste ZPL into the right panel and click `Render`.

## Multi-label Navigation

For a batch containing multiple labels:

1. Render or receive the batch.
2. Use **Next** to go to the next label.
3. Use **Prev** to go to the previous label.
4. The status bar shows the current label index.

Keyboard shortcuts:
- `>` or Right Arrow = next label
- `<` or Left Arrow = previous label

When the last label is reached, the app shows: `No additional labels found in this ZPL batch.`

## Notes

- Label rendering currently uses Labelary public API (fair use).
- If rendering fails, verify internet access and that the ZPL dimensions/DPI are set correctly.
