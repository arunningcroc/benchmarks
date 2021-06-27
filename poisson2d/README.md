## Poisson solver in various languages

This solver uses a simple Jacobi iteration to solve a Poisson equation. For details, see, for example,
"Computational Physics" by Mark Newman, Chap 9. Compiler commands were:

```gfortran sourcefile.f95 -Ofast -o program```

```gcc sourcefile.c -Ofast -o program```

For Cython module (import it to run):

```python setup.py build_ext --inplace```

And the timing results (the grid is MxM):

| Language            | M=100 (seconds) | M=200 (seconds)       | M=300 (seconds)        |
|---------------------|-----------------|-----------------------|------------------------|
| Python (pure)       | 276             | Until sun's expansion | Heat death of universe |
| Cython              | 1.02            | 32.8                  | 229                    |
| Fortran (naive)     | 0.34            | 13.2                  | 69.7                   |
| Fortran (optimized) | 0.18            | 6.25                  | 31.4                   |
| C (naive)           | 0.42*           | 7.25                  | 33.7                   |
| C (optimized)       | 0.37*           | 6.80                  | 32.8                   |

For all of these results, the amount of iterations performed by the respective codes was approximately
the same, with the exception of the 100x100 grid C codes, which did nearly a double amount of iterations
compared to the rest, for some reason.

Some thoughts on the code at https://runningcrocodile.fi/articles/pythonperformance.html