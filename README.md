# The Bitwise Gamedev Challenge

## The Concept

There is *one rule*: the core game logic is allowed to persist *no more* than 64 bits (8 bytes) of data between
frames/ticks.

## Additional Details

In effect, your game should be a pure function with the following inputs:

- the 64 bit integer emitted by the last frame (you may provide a default value for the first frame)

- player inputs (keyboard/mouse/controller/etc.) & other environmental information (time delta since the last frame, etc.)

- Random number generation, provided the state of the RNG is not relied upon for gameplay (i.e: it should be possible to
  reseed the RNG from true random sources every frame without changing the nature of the gameplay)

and the following outputs:

- a 64-bit integer that will be persisted to the next frame

- UI/graphics/other outputs in some stateless form, such as a framebuffer or sound waveforms

No statics, global values, IO (beyond that which falls within the aforementioned categories), side-channel state (such
as inducing lag to use the frame time delta as extra state), or other unprincipled 'tricks' are permitted: it should
be possible to recreate the *entire* state of the game at any given frame given only the 64-bit integer and the code
that composes the game logic.

## Why 64 bits?

Based on personal experimentation, I've found 64 bits to be the perfect middle-ground that keeps the challenge engaging and
forces creativity, while also not forbidding a lot of different potential game genres.

## Ambiguities

Some games do not have a strict definition of 'frames' or 'ticks'.

For example, a text adventure game might accept many characters of input, but only act on them once the 'return' key
is pressed. Does this mean that the game has to store the partially-complete string within its 64-bit state? There is
no right answer.

My suggestion would be to decide beforehand where your dividing line is between the 'input system' and the 'core game',
and then respect the rules of the challenge within that core. For example, you might decide that an entire command to
the text adventure game counts as a single atomic input, and hence need not count toward the stored state of the game.

## Suggested Formats

The Bitwise Challenge can be taken both as an individual endeavour, or as a group activity/competition such as a
game jam or hackathon.

## Pure caches

An exception is made for [memoization caches](https://en.wikipedia.org/wiki/Memoization), provided the result of
using the cache is indistinguishable from recomputing the cached function on the input every time (you can't, for
example, rely on whether a value was present in the cache for some behaviour of the game logic).

You may use such caches for the sake of performance. For example, procedurally generating a game world from a seed on
every frame would, understandably, be prohibitely expensive.

An example of such a memoization cache is the [`cached`](https://crates.io/crates/cached) Rust crate.

## Variations

- Increasing or decreasing the number of bits for varying difficulty

## Showcases

- `@izabera`: ['2048' in 64 bits](https://github.com/izabera/bitwise-challenge-2048)
- `@toombs-caeman`: [Wordle in 64 bits](https://github.com/toombs-caeman/wordle)
- `@toombs-caeman`: [Conway's Game of Life in 64 bits](https://github.com/toombs-caeman/gol64/)
- `@zesterer`: [Snake in 8 bytes](https://github.com/zesterer/bitwise-examples#bitwise-snake) (part of my example games)
- `@Garklein`: [Connect 4 in 64 bits](https://github.com/Garklein/connect-6-4)
- `@maksverver`: [Typer 64, a typing game in 64 bits](https://maksverver.github.io/typer-64/)
- `@toombs-caeman`: [Maze64, a maze solving game in 64 bits](https://github.com/toombs-caeman/maze64)
- `@sam-mccall`: [Shlurdle: A sliding windows word game similar to Absurdle](https://github.com/sam-mccall/sam-mccall.github.io/tree/main/shlurdle)

*If you want your entry added to the list, open an issue!*

## Inspiration

The idea was partially inspired by
[this blog post](https://www.andreinc.net/2022/05/01/4-integers-are-enough-to-write-a-snake-game) by @nomemory.
