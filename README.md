# dsp-audio-enhancement

# EE 321: Digital Signal Processing (DSP) Assignment

## Overview

This assignment involves working with audio files to design digital filters and analyze signal characteristics using Python. The tasks include removing echo noise from an audio signal and segmenting a speech signal into voiced, unvoiced, and noise components. All tasks are to be completed using custom Python functions without the aid of DSP libraries.

## Task 1: Removing Echo from Audio Signal

### Task Description
An audio file, `goodmorning.wav`, contains the phrase "good morning" with added echo noise. The task is to design a digital filter that eliminates the echo from the signal. This involves:
- Loading the audio signal into a numpy array.
- Designing a digital filter (without using DSP Python libraries) to remove the echo.
- Applying the filter to the audio signal and showing that it has removed the echo.
- Comparing the original noisy signal and the filtered signal by plotting their frequency content.

### Approach
We used a custom FIR filter with a **band-pass** characteristic:
- **Frequency Pass Band**: [250 Hz, 2200 Hz] to target and filter the frequency range of the human voice while attenuating the echo.
- **Filter Order**: 1023 for a balance between sharp roll-off and computational complexity.
- **Windowing Technique**: Hamming window to reduce spectral leakage.

The key steps involved designing the filter, plotting its magnitude and phase response, and applying it to the audio signal.

### Filter Equations
- **Ideal Low-Pass Filter (LPF) Impulse Response**:
  \[
  h_d[n] = \left(\frac{f_c}{f_s}\right) \cdot \text{sinc}\left(2f_c\left(n - \frac{N-1}{2}\right)\right)
  \]
  where \(f_s\) is the sampling frequency, \(f_c\) is the cutoff frequency, and \(N\) is the filter order.

- **Hamming Window**:
  \[
  w(n) = \alpha - \beta \cdot \cos\left(\frac{2\pi n}{N-1}\right)
  \]
  with \(\alpha = 0.54\) and \(\beta = 0.46\).

- **Final Filter Coefficients**:
  \[
  h(n) = h_d'[n] \cdot w(n)
  \]
  where \(h_d'[n]\) is the impulse response of the band-pass filter.

- **Filtering Process**:
  The filtered signal \(y(n)\) is obtained by convolving the input signal \(x(n)\) with the filter coefficients:
  \[
  y(n) = x(n) * h(n)
  \]

### Results
The original and filtered signals were plotted and compared. The designed filter successfully removed the echo, as seen in the amplitude vs. time plot.

## Task 2: Segmenting Speech Signal into Voiced, Unvoiced, and Noise Components

### Task Description
The audio file `safety.wav` contains the word "safety" spoken by a male speaker with background noise. The goal is to segment the signal into voiced, unvoiced, and silence (background noise) portions.

### Approach
- **Voiced Segment**: Frequencies with maximum magnitude (1–850 Hz).
- **Unvoiced Segment**: Frequencies with medium magnitude (950–1050 Hz).
- **Noise Segment**: Frequencies with minimum magnitude (1051–3000 Hz).

### Filter Design
We used three different band-pass filters to extract the three components:
- **Filter Order**: 101 for computational efficiency.
- **Windowing Technique**: Hamming window, as in Task 1.

### Power Spectral Density (PSD)
- Voiced component: Max PSD around -20 dB under 600 Hz.
- Unvoiced component: Medium PSD around -50 dB between 500-800 Hz.
- Noise component: Lowest PSD around -60 dB between 800-1750 Hz.

### Results
The original raw signal and segmented signals were plotted. The PSD of each segment was computed and compared, confirming the correct segmentation.

## Conclusion
Both tasks successfully demonstrated the design of custom digital filters in Python. Task 1 removed the echo from the audio signal, while Task 2 segmented the speech signal into its key components.
