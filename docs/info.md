## How it works

This project currently holds the Tiny Tapeout template's example design, as a placeholder while the timing-margin sensor is being designed.

It adds two 8-bit numbers. The first comes in on the `ui_in` pins and the second on the `uio_in` pins. All eight bidirectional pins are used as inputs, because `uio_oe` is set to 0. The 8-bit sum appears on the `uo_out` pins.

The adder is combinational: it has no flip-flops, so the output changes as soon as the inputs change, and the clock and reset are not used. Only 8 bits of the result are kept, so any sum above 255 wraps around: the carry out of the top bit is dropped, and the output is the sum minus 256.

## How to test

1. Clock and reset: not needed. The output follows the inputs directly.
2. Set `ui_in` to 20 and `uio_in` to 30. `uo_out` should read 50.
3. Edge case: set `ui_in` to 255 and `uio_in` to 1. `uo_out` should read 0, because the true sum, 256, needs a ninth bit that the design doesn't keep.

The automated test in `test/test.py` checks step 2 in simulation.
