# Modular hackathon project
Mojo explorations around benchmarking and tiling

## Details

Code is based off of the Puzzle 14 solutions here: https://github.com/modular/mojo-gpu-puzzles/blob/main/problems/p14/p14.mojo

## Summary

Two things were accomplished

1.  Learned how to perform benchmarking on mojo code
2.  Investigated running code without barrier() and synchronize() calls which resulted in correct results for up to 10K runs

### === p14_benchmarking.mojo - p14 with benchmarking added. 

$ mojo p14.mojo --naive
--------------------------------------------------------------------------------
Benchmark Report (s)
--------------------------------------------------------------------------------
- Mean: 1.6751968148706355e-05
- Total: 2.334135482
- Iters: 139335
- Warmup Total: 1.7766e-05
- Fastest Mean: 1.6751968148706355e-05
- Slowest Mean: 1.6751968148706355e-05

$ mojo p14.mojo --tiled
--------------------------------------------------------------------------------
Benchmark Report (s)
--------------------------------------------------------------------------------
- Mean: 1.638169004186603e-05
- Total: 2.410336346
- Iters: 147136
- Warmup Total: 1.4912e-05
- Fastest Mean: 1.638169004186603e-05
- Slowest Mean: 1.638169004186603e-05


$ mojo p14_benchmark.mojo --idiomatic-tiled

--------------------------------------------------------------------------------
Benchmark Report (s)
--------------------------------------------------------------------------------
- Mean: 1.6362159057688895e-05
- Total: 2.395518259
- Iters: 146406
- Warmup Total: 1.4461e-05
- Fastest Mean: 1.6362159057688892e-05
- Slowest Mean: 1.6362159057688892e-05

p14_benchmarker.mojo with all barrier() and synchronize() calls commented out
--------------------------------------------------------------------------------
Benchmark Report (s)
--------------------------------------------------------------------------------
- Mean: 3.3620162330914076e-06
- Total: 2.393970727
- Iters: 712064
- Warmup Total: 4.277e-06
- Fastest Mean: 3.3620162330914076e-06
- Slowest Mean: 3.3620162330914076e-06


### === p14_size_100.mojo - p14 with barrier() and synchronize() commented out and various SIZE_TILED values

SIZE_TILED = 8 and BLOCKS_PER_GRID_TILED = (3, 3) - OK

SIZE_TILED = 12 and BLOCKS_PER_GRID_TILED = (4, 4) - OK

SIZE_TILED = 16 and BLOCKS_PER_GRID_TILED = (4, 4) - Result mismatch
