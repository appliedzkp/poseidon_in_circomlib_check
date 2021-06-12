# Comparing the Poseidon hash function implementation in `circomlib` against the reference implementation

## Output from circomlib

`circomlib` version 0.5.2 (commit `4b2989a4431f332e2d1d494882c6f52f2d423558`)
contains an implementation of the Poseidon hash function.

The `test/poseidonjs.js` test file checks that the following are true:

1. The output of `poseidon([1,2]` equals
`115cc0f5e7d690413df64c6b9662e9cf2a3617f2743245519e19607a4417189a`

2. The output of `poseidon([1,2,3,4])` equals
`299c867db6c1fdd79dcefa40e4510b9837e60ebb1ce0663dbaa525df65250465`

## Output of the reference implementation

The code for the reference implementation is at this URL:

https://extgit.iaik.tugraz.at/krypto/hadeshash

At the time of writing, the commit hash I checked out was:

`659de89cd207e19b92852458dce92adf83ad7cf7`

I had SageMath installed:

```
$ sage --version
SageMath version 8.6, Release Date: 2019-01-15
```

To check (1), I ran:

```bash
sage poseidonperm_x5_254_3.sage
```

```
Input:
['0x0000000000000000000000000000000000000000000000000000000000000000', '0x0000000000000000000000000000000000000000000000000000000000000001', '0x0000000000000000000000000000000000000000000000000000000000000002']
Output:
['0x115cc0f5e7d690413df64c6b9662e9cf2a3617f2743245519e19607a4417189a', '0x0fca49b798923ab0239de1c9e7a4a9a2210312b6a2f616d18b5a87f9b628ae29', '0x0e7ae82e40091e63cbd4f16a6d16310b3729d4b6e138fcf54110e2867045a30c']
Input (concat):
0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002
Output (concat):
0x115cc0f5e7d690413df64c6b9662e9cf2a3617f2743245519e19607a4417189a0fca49b798923ab0239de1c9e7a4a9a2210312b6a2f616d18b5a87f9b628ae290e7ae82e40091e63cbd4f16a6d16310b3729d4b6e138fcf54110e2867045a30c
```

To check (2), I ran:

```bash
sage poseidonperm_x5_254_5.sage
```

```
Input:
['0x0000000000000000000000000000000000000000000000000000000000000000', '0x0000000000000000000000000000000000000000000000000000000000000001', '0x0000000000000000000000000000000000000000000000000000000000000002', '0x0000000000000000000000000000000000000000000000000000000000000003', '0x0000000000000000000000000000000000000000000000000000000000000004']
Output:
['0x299c867db6c1fdd79dcefa40e4510b9837e60ebb1ce0663dbaa525df65250465', '0x1148aaef609aa338b27dafd89bb98862d8bb2b429aceac47d86206154ffe053d', '0x24febb87fed7462e23f6665ff9a0111f4044c38ee1672c1ac6b0637d34f24907', '0x0eb08f6d809668a981c186beaf6110060707059576406b248e5d9cf6e78b3d3e', '0x07748bc6877c9b82c8b98666ee9d0626ec7f5be4205f79ee8528ef1c4a376fc7']
Input (concat):
0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000030000000000000000000000000000000000000000000000000000000000000004
Output (concat):
0x299c867db6c1fdd79dcefa40e4510b9837e60ebb1ce0663dbaa525df652504651148aaef609aa338b27dafd89bb98862d8bb2b429aceac47d86206154ffe053d24febb87fed7462e23f6665ff9a0111f4044c38ee1672c1ac6b0637d34f249070eb08f6d809668a981c186beaf6110060707059576406b248e5d9cf6e78b3d3e07748bc6877c9b82c8b98666ee9d0626ec7f5be4205f79ee8528ef1c4a376fc7
```

## Conclusions

The first output of `sage poseidonperm_x5_254_3.sage` matches that of
`circomlib`'s Poseidon implementation for 2 inputs (t = 3).

The first output of `sage poseidonperm_x5_254_5.sage` matches that of
`circomlib`'s Poseidon implementation for 4 inputs (t = 5).
