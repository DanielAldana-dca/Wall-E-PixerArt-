# Wall-E Pixel Art

A code-driven pixel art editor built with **Godot Engine and C#**. Create digital artwork by writing instructions in a custom programming language designed to control a drawing canvas.

Wall-E combines a code editor, a command interpreter, and a pixel-based drawing environment, allowing you to generate shapes, build patterns, and automate drawing operations through code.

## Features

- **Pixel art canvas:** Work with a configurable grid ranging from 16 × 16 to 400 × 400 pixels, with a default size of 200 × 200.
- **Custom scripting language:** Write instructions to control the drawing process using variables, arithmetic expressions, labels, and conditional jumps.
- **Drawing tools:** Draw lines, circles, and rectangles, fill connected areas, and configure brush colors and sizes.
- **Code editor:** Write and execute scripts with syntax highlighting.
- **Project management:** Save and load scripts using the `.pw` file format and access recently opened files.
- **Canvas navigation:** Use integer coordinates for precise positioning and mouse-wheel zoom to inspect the artwork.
- **Canvas inspection:** Query drawing state, retrieve coordinates, and inspect pixel colors through supported language functions.

## Technology Stack

- **Language:** C#
- **Engine:** Godot Engine 4.6 with .NET support
- **Framework:** .NET 8
- **Application type:** Desktop application

## Getting Started

### Prerequisites

Install the following software:

- [Godot Engine .NET 4.6](https://godotengine.org/download/)
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

Use a Godot build with C# support rather than the standard build.

### Installation

Clone the repository and navigate to its directory:

```bash
git clone https://github.com/DanielAldana-dca/Wall-E-PixerArt-.git
cd Wall-E-PixerArt-
```

Open the project in Godot by selecting `project.godot`, allow the project to import its resources, and build the C# project if required.

### Running the Application

1. Open the project in Godot.
2. Build the project if necessary.
3. Run the main scene, `Main.tscn`.
4. Write a script in the code editor.
5. Execute the script to render the drawing on the canvas.

## Scripting Language

Wall-E uses a custom language for describing drawing operations and controlling their execution.

### Drawing Commands

| Command | Description |
|---|---|
| `Spawn(x, y)` | Positions the drawing cursor. |
| `Color("name")` | Sets the brush color. |
| `Size(n)` | Sets the brush size, from 1 to 10. |
| `DrawLine(dx, dy, len)` | Draws a line in a specified direction. |
| `DrawCircle(dx, dy, radius)` | Draws a circle. |
| `DrawRectangle(dx, dy, width, height)` | Draws a rectangle. |
| `Fill()` | Fills a connected area. |
| `GoTo[label](condition)` | Jumps to a label when the condition is satisfied. |

### Canvas and Brush Queries

| Function | Description |
|---|---|
| `GetActualX()` | Retrieves the current X coordinate. |
| `GetActualY()` | Retrieves the current Y coordinate. |
| `GetCanvasSize()` | Retrieves the canvas dimensions. |
| `GetColorCount(color, x1, y1, x2, y2)` | Counts pixels of a specified color within an area. |
| `IsBrushColor(color)` | Checks the current brush color. |
| `IsBrushSize(n)` | Checks the current brush size. |
| `IsCanvasColor(color, dx, dy)` | Checks a canvas color at a relative position. |

The language uses integer-based arithmetic and coordinates. Decimal values are not supported.

## Example

The following script draws a series of increasingly smaller circles to create a spiral-like pattern.

```text
Spawn(100, 100)

Color("Purple")

radio <- 50

loop_espiral

DrawCircle(1, 1, radio)

radio <- radio - 5

GoTo[loop_espiral](radio > 10)
```

This example demonstrates variable assignment, drawing commands, arithmetic operations, labels, and conditional control flow.

## Project Structure

The application separates the main stages of script processing and rendering.

| File | Responsibility |
|---|---|
| `Lexer.cs` | Converts source code into tokens. |
| `Parser.cs` | Parses tokens into executable instructions. |
| `AST.cs` | Defines the structures used to represent parsed code. |
| `Interpreter.cs` | Executes the instructions. |
| `CommandRegistry.cs` | Registers supported drawing commands. |
| `CanvasRenderer.cs` | Handles canvas rendering. |
| `MainUI.cs` | Coordinates the application interface. |
| `Main.tscn` | Defines the main Godot scene. |

## Technical Notes

- Canvas dimensions are configurable within the supported range.
- Coordinates and arithmetic operations use integers.
- Command names are reserved and cannot be used as variable names.
- Drawing operations must respect the configured canvas boundaries.
- Scripts are stored using the `.pw` extension.

---

**Wall-E Pixel Art** — Programmatic drawing through a custom scripting language.