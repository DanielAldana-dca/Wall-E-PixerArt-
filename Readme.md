# Wall-E Pixel Art

A code-driven pixel art editor built with **Godot Engine 4.6 and C#**. Create drawings by writing instructions in a custom language and executing them on a pixel-based canvas.

## Features

- Pixel-based drawing canvas with configurable dimensions.
- Custom language with tokens, parsing, an abstract syntax tree, and an interpreter.
- Drawing commands for lines, circles, rectangles, and flood fill.
- Brush color and size controls.
- Variables, arithmetic expressions, labels, and conditional jumps.
- Canvas and brush inspection functions.
- Script editor with line numbers and execution controls.
- Save and load scripts using the `.pw` format.
- Canvas grid, clear, and resize controls.

## Technology

- **Engine:** Godot Engine 4.6 (.NET build)
- **Language:** C#
- **Runtime:** .NET 8

## Requirements

Install [Godot Engine 4.6 with .NET support](https://godotengine.org/download/) and the [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0). The standard non-.NET Godot build cannot compile the C# project.

## Run locally

```bash
git clone https://github.com/DanielAldana-dca/Wall-E-PixerArt-.git
cd Wall-E-PixerArt-
```

Open the folder containing `project.godot` in Godot, let the editor import the project, build the C# solution if prompted, and run the main scene.

## Example scripts

The `examples/` directory contains sample `.pw` scripts. Open one in the application or copy its contents into the code editor and execute it.

## Language overview

The language is case-insensitive for recognized keywords. Its supported operations include:

| Instruction / function | Purpose |
|---|---|
| `Spawn(x, y)` | Sets the drawing position. |
| `Color("Purple")` | Selects the brush color. |
| `Size(n)` | Sets the brush size. |
| `DrawLine(dx, dy, length)` | Draws a line. |
| `DrawCircle(dx, dy, radius)` | Draws a circle. |
| `DrawRectangle(dx, dy, width, height, stroke)` | Draws a rectangle. |
| `Fill()` | Fills a connected region from the current drawing position. |
| `GoTo[label](condition)` | Jumps to a label when the condition evaluates as true. |
| `GetActualX()` / `GetActualY()` | Reads the current drawing coordinates. |
| `GetCanvasSize()` | Reads the canvas dimensions. |
| `GetColorCount(color, x1, y1, x2, y2)` | Counts matching pixels in a rectangular region. |
| `IsBrushColor(color)` / `IsBrushSize(n)` | Checks the current brush settings. |
| `IsCanvasColor(color, dx, dy)` | Checks a pixel color relative to the current position. |

Example:

```text
Spawn(100, 100)
Color("Purple")
radius <- 50

loop
DrawCircle(0, 0, radius)
radius <- radius - 5
GoTo[loop](radius > 10)
```

Use the supplied example scripts as the reference for the exact syntax accepted by the current interpreter.

## Project structure

```text
Wall-E-PixerArt-/
├── assets/
│   ├── icon.svg
│   └── icon.svg.import
├── examples/
│   ├── example-01.pw
│   ├── example-02.pw
│   ├── example-03.pw
│   └── example-04.pw
├── scenes/
│   └── Main.tscn
├── scripts/
│   ├── canvas/
│   │   └── CanvasRenderer.cs
│   ├── language/
│   │   ├── AST.cs
│   │   ├── CommandRegistry.cs
│   │   ├── Interpreter.cs
│   │   ├── Lexer.cs
│   │   ├── Parser.cs
│   │   ├── Token.cs
│   │   └── WallEException.cs
│   └── ui/
│       └── MainUI.cs
├── .gitignore
├── project.godot
├── Wall-E.csproj
└── Wall-E.sln
```

The `.uid` sidecar files for C# scripts are kept alongside their corresponding scripts so Godot can preserve resource identities.

## Notes

- Godot-generated editor/import data is not included in the source archive; Godot regenerates it when the project is opened.
- This reorganization separates source files by responsibility and updates the main-scene, script, and icon paths. The application logic itself has not intentionally been changed.
