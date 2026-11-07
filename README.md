# JavaScript Brainfuck interpreter #

As the title implies, this is a [Brainfuck](http://esolangs.org/wiki/Brainfuck) interpreter written in JavaScript.

It runs your code directly in the browser and provides a small debugger: step-by-step execution, memory inspection, and live program state. The interface is styled after Windows 98 using [98.css](https://github.com/jdan/98.css).

## Usage ##

Enter your Brainfuck code in the **Brainfuck input** field.

- **Run** — execute the program.
- **Step** — execute a single instruction.
- **Step auto:** — automatically step through the program; enter the delay in milliseconds in the interval field first.
- **Pause** — pause the currently running program.
- **Stop** — stop execution / auto-stepping.
- **(Re-)initialise** — reset the program and memory and rebuild it from the current input.
- **Clear** — clear the input field.

The **Execution** panel highlights the current instruction. The **Program output** panel shows the output and a live **Memory view** table (Dec/Hex/Bin/ASCII) with the current cell highlighted. The status bar shows the current program status and the data pointer position.

Input support is available through an `onkeypress` event while the program is running.

## Project structure ##

```
public/
├── index.html
└── assets/
    ├── css/
    │   ├── 98.css            Windows 98 component styles
    │   ├── brainfuck.css     App-specific theme
    │   └── ms_sans_serif*.woff(2)   Pixelated MS Sans Serif font
    └── js/
        └── brainfuck.js      Interpreter and UI logic
```

Everything inside `public/` is static and can be served as-is from the web root of any static host.

## Implementation notes ##

- **Memory size** is 512 bytes.
- **Infinite loops** are supported. Execution is throttled by delaying 5ms every `THROTTLE_THRESHOLD` (1000) instructions. Change `THROTTLE_THRESHOLD` in `public/assets/js/brainfuck.js` to adjust.
- Execution is controlled through statuses (`ready`, `running`, `stepping`, `paused`, `stopped`), which drive the Run/Pause/Stop buttons and the UI status bar.

## Latest upgrades ##

- **Windows 98 theme** applied via 98.css, with the original pixelated MS Sans Serif font, title bar, sunken panels and status bar.
- Added a **status bar** showing the program status and the current data pointer (index, decimal and hex value).
- Output and memory views redesigned for the new theme; the memory table scrolls inside a sunken panel.
- Fixed layout issues (Clear button spacing, title-bar control alignment).

## Credits ##

The original interpreter was written by [Mich D](https://michd.me) — original source: [michd/brainfuck-interpreter-js](https://github.com/michd/brainfuck-interpreter-js). Many thanks for the solid foundation this project is built on.

The Windows 98 look is provided by [98.css](https://github.com/jdan/98.css) by Jordan Scales.

## Running locally ##

Because the page uses relative asset paths, serve the `public/` folder over HTTP, for example:

```sh
cd public
python3 -m http.server 8000
```

Then open <http://localhost:8000>.
