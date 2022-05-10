# The Bitwise Gamedev Challenge

## The concept

There is **one rule*: the core game logic is allowed to persist *no more* than 64 bits of data between frames.

## Additional Details

In effect, your game should be a pure function with the following inputs:

- the 64 bit integer emitted by the last frame (you may provide a default value for the first frame)

- player inputs (keyboard/mouse/controller/etc.) & other environmental information (time delta since the last frame)

and the following outputs:

- a 64-bit integer that will be persisted to the next frame

- UI/graphics in some stateless form, such as a framebuffer or sound waveforms

No statics, global values, IO (beyond that which falls within the aforementioned category), side-channel state (such
as artifically inducing lag to change the frame time delta), or other unprincipled 'tricks' are permitted: it should
be entirely possible to recreate the *entire* state of the game at any given frame given only the 64-bit integer and
the code that composes the game logic.

## Exceptions

An exception is made for [memoization caches](https://en.wikipedia.org/wiki/Memoization), provided the result of
using the cache is indistinguishable from recomputing the cached function on the input every time.

You may use such caches for the sake of performance (procedurally generating a game world from a seed on every frame
would, understandably, be prohibitely expensive).

An example of such a memoization cache is the [`cached`](https://en.wikipedia.org/wiki/Memoization) Rust crate.

## Variations

- Increasing or decreasing the number of bits for varying difficulty

## Showcases

*No known examples currently exist*