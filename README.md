# kasl

`kasl` is an umbrella crate that includes re-exports of `kasl-core` and backends (currently there is only Cranelift backend).

# About the KASL language

KASL is a programming language designed for audio processing.
The KASL language itself is implemented as a simple numerical calculation language with unique `input`, `output` and `state` variables, and can be used for audio processing with my [Knodiq DAW](https://github.com/hatya-mouse/knodiq), which is under development.

## How to Run the KASL Programs

Currently, there are no hosts that can run KASL program for audio processing.
However, you can run KASL code for genuine numerical calculation and there two ways to run it:

- [`kaslc`](https://github.com/hatya-mouse/kaslc) — A command-line tool to run KASL programs locally.
- [`kasl.hatya.dev`](https://kasl.hatya.dev) — Features **online KASL playground** where you can run KASL programs without installation.

## Examples

### Example 1 — Fibonacci

The following program calculates the fibonacci sequence by using `state` variable to store the last two numbers.
I recommend running this program on the online playground, since it can show the outputs for each iterations, while `kaslc` can only show the output from the last iteration.

```kasl
import std

state a = 0
state b = 1
output result = 0

func main() {
    result = a
    let next = a + b
    a = b
    b = next
}
```

### Example 2 — Audio Processing

Here's an example KASL code which generates sine wave with the sample rate of 44100, and the frequency of 440Hz. The program takes an input variable called `time`, and outputs a output variable called `out`.

```kasl
import std

let pi = 3.1415926535
let sample_rate = 44100.0
let frequency = 440.0

input time = 0.0
output out = 0.0

func main() {
    out = std.float.sin((2.0 * pi * frequency * time) / sample_rate)
}
```
