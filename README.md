# EXP.NO.9-Simulation-of-Pulse-Code-Modulation
9.Simulation of PCM

# AIM
```
To study and simulate the pulse Code Modulation using the required program.
```

# SOFTWARE REQUIRED
```
Colab softaware.
```

# ALGORITHMS
```
Step 1: Generate the Analog Signal
Set the sampling frequency (fs) and duration.

Create a time vector (t) from 0 to 1 second.

Define the signal frequency (f) and generate a sine wave.

Step 2: Quantize the Signal
Set the number of quantization levels (L).

Find the maximum value of the signal.

Shift and scale the signal to fit into the range [0, L-1].

Round the values to the nearest integer.

Clip values to ensure they stay within [0, L-1].

Step 3: Encode the Signal
Calculate how many bits are needed (e.g., 4 bits for 16 levels).

Convert each quantized value into a fixed-length binary string.

Step 4: Plot the Results
Plot the original analog signal.

Plot the quantized signal using a stem plot.

Plot the PCM values (as integers).

Print the first 10 binary encoded values.

```

# PROGRAM
```
import matplotlib.pyplot as plt
import numpy as np

# Parameters
sampling_rate = 5000
duration = 0.1
quantization_levels = 16

# Time base
t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

# Two message signals
frequency1 = 50
frequency2 = 120
message_signal1 = np.sin(2 * np.pi * frequency1 * t)
message_signal2 = np.sin(2 * np.pi * frequency2 * t)

# Quantization
def quantize(signal, levels):
    step = (max(signal) - min(signal)) / levels
    quantized = np.round(signal / step) * step
    pcm = ((quantized - min(quantized)) / step).astype(int)
    return quantized, pcm

quantized_signal1, pcm_signal1 = quantize(message_signal1, quantization_levels)
quantized_signal2, pcm_signal2 = quantize(message_signal2, quantization_levels)

# Multiplexing the PCM signals
# Interleaving samples from both signals
multiplexed_pcm = np.empty((pcm_signal1.size + pcm_signal2.size,), dtype=int)
multiplexed_pcm[0::2] = pcm_signal1
multiplexed_pcm[1::2] = pcm_signal2

# Time base for multiplexed stream (double samples)
t_mux = np.linspace(0, duration, multiplexed_pcm.size, endpoint=False)

# Clock signal for reference
clock_signal = np.sign(np.sin(2 * np.pi * 200 * t))

# Plotting
plt.figure(figsize=(14, 12))

plt.subplot(8, 1, 1)
plt.plot(t, message_signal1, label="Message Signal 1 (50Hz)", color='blue')
plt.title("Original Message Signal 1")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 2)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

plt.subplot(8, 1, 3)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.title("Quantized Signals")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 4)
plt.plot(t, message_signal2, label="Message Signal 2 (120Hz)", color='orange', alpha=0.7)
plt.title("Original Message Signal 2")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 5)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

plt.subplot(8, 1, 6)
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Quantized Signals")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 7)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Quantized Signals")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 8)
plt.step(t_mux, multiplexed_pcm, label="Multiplexed PCM Signal", color='black')
plt.title("Multiplexed PCM Signal (Interleaved)")
plt.xlabel("Time [s]")
plt.ylabel("PCM Value")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()

```

# OUTPUT

![Screenshot 2025-04-16 214805](https://github.com/user-attachments/assets/911acaf0-696d-4cf8-bea7-b8c7de47a13a)

# RESULT / CONCLUSIONS
```
Thus the simulation of pulse Code Modulation is verified and the graph is simulated.
```
