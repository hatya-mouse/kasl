# kasl

`kasl` is an umbrella crate that includes re-exports of `kasl-core` and backends (currently there is only Cranelift backend).

# About the KASL language

KASL is a programming language designed for audio processing.
The KASL language itself is implemented as a simple numerical calculation language with unique `input`, `output` and `state` variables, and can be used for audio processing with my [Krenic DAW](https://github.com/hatya-mouse/krenic), which is under development.

## How to Run the KASL Programs

You can use Krenic DAW to play audio using the KASL language.
Also, you can run KASL code for genuine numerical calculation and there two ways to run it:

- [`kaslc`](https://github.com/hatya-mouse/kaslc) — A command-line tool to run KASL programs locally.
- [`kasl.hatya.dev`](https://kasl.hatya.dev) — Features **online KASL playground** where you can run KASL programs without installation.

## Characteristics

KASL is specificlly designed for audio synthesis, so there are some points that this language is different from the other languages. 

### Input, Output and State Variables

KASL natively supports `input`, `output` and `state` variables.
`input` variables are the variables that can receive data from the execution host. For example, when you run KASL program on Krenic and connect an edge to the input in the graph editor, the value will be passed to the variable.
`output` variables pass the calculated data back to the execution host. To illustrate, this can be used for synthesizers to pass the generated samples to the DAW.
`state` variables can preserve the stored value over the samples. This is useful for creating a delay buffer to create effects such as echo, or reverb.

### Fixed-Count Loop

KASL supports fix count loop, which can be used by specifying `loop` keyword as follows:

```kasl
func main() {
    loop 5 {
        do_something()
    }
}
```

This is the same as:

```kasl
func main() {
    do_something()
    do_something()
    do_something()
    do_something()
    do_something()
}
```

Because KASL compiler can find the definition of the constant, you can also write like this:

```kasl
func main() {
    let loop_count = 5
    loop loop_count {
        do_something()
    }
}
```
