# GNU Radio QPSK Doppler Test

This directory contains the GNU Radio flowgraph used to generate a controlled QPSK frequency-variation test for the MATLAB estimator.

## Flowgraph

```text
qpsk_doppler_example.grc
```

The flowgraph reads an interleaved signed 16-bit QPSK IQ recording and multiplies it by the output of a voltage-controlled oscillator.

## Test Configuration

| Parameter | Value |
|---|---|
| GNU Radio version | 3.10.12 |
| Modulation | QPSK |
| Sampling rate | 2 MHz |
| Input format | Interleaved signed 16-bit I/Q |
| Output format | Interleaved signed 16-bit I/Q |
| Output duration | 10 seconds |
| Frequency-control amplitude | 70 Hz |
| First control frequency | 0.1 Hz |
| Second control frequency | 0.3 Hz |

The applied frequency variation is approximately:

```text
Δf(t) = 70 × cos(2π × 0.1t) × sin(2π × 0.3t) Hz
```

Equivalently:

```text
Δf(t) = 35 × [sin(2π × 0.4t) + sin(2π × 0.2t)] Hz
```

The frequency profile repeats every 5 seconds and reaches approximately ±61.6 Hz.

## Required Input

The flowgraph expects a local QPSK recording named:

```text
qpsk_input_int16.dat
```

The recording must contain interleaved signed 16-bit samples in the following order:

```text
I0, Q0, I1, Q1, I2, Q2, ...
```

If a different input recording is used, update the path in the GNU Radio File Source block before running the flowgraph.

## Generated Output

The default output filename is:

```text
qpsk_doppler_test_int16.dat
```

The generated IQ file can be analyzed using the MATLAB estimator in:

```text
src/doppler_estimator_parametric_resolution.m
```

Raw IQ recordings are excluded from the main Git repository because of their size.
