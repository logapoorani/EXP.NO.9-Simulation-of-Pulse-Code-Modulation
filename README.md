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

# Binary data
data = [1, 0, 1, 1, 0]
bit_duration = 1
Fs = 8000 # Sampling rate
t_bit = np.linspace(0, bit_duration, Fs, endpoint=False)

# Carrier frequencies
f1 = 100 # FSK freq for bit 1
f0 = 5  # FSK freq for bit 0
f_c = 10  # Common carrier for ASK and PSK

# --- ASK Function ---
def ask(bit):
    return np.cos(2 * np.pi * f_c * t_bit) if bit == 1 else np.zeros(len(t_bit))

# --- Repeater ---
def repeat_waveform(fn, bitstream):
    modulated = []
    for b in bitstream:
        modulated.extend(fn(b))
    return modulated

# Generate signals
digital = np.repeat(data, Fs)
ask_signal = repeat_waveform(ask, data)

# FSK signal
fsk_signal = []
for bit in data:
    freq = f1 if bit else f0
    wave = np.sin(2 * np.pi * freq * t_bit)
    fsk_signal.extend(wave)

# PSK signal
psk_signal = []
for bit in data:
    phase = 0 if bit == 1 else np.pi
    wave = np.sin(2 * np.pi * f_c * t_bit + phase)
    psk_signal.extend(wave)

# Time axis
time = np.linspace(0, bit_duration * len(data), Fs * len(data), endpoint=False)

# Plotting
plt.figure(figsize=(14, 10))

# Digital Signal
plt.subplot(4, 1, 1)
plt.plot(time, digital, color='black')
plt.title("Digital Input Signal")
plt.ylabel("Amplitude")
plt.grid(True)

# ASK Signal
plt.subplot(4, 1, 2)
plt.plot(time, ask_signal, color='green')
plt.title("Amplitude Shift Keying (ASK using Cosine Carrier)")
plt.ylabel("Amplitude")
plt.grid(True)

# FSK Signal
plt.subplot(4, 1, 3)
plt.plot(time, fsk_signal, color='blue')
plt.title("Frequency Shift Keying (FSK)")
plt.ylabel("Amplitude")
plt.grid(True)

# PSK Signal
plt.subplot(4, 1, 4)
plt.plot(time, psk_signal, color='red')
plt.title("Phase Shift Keying (PSK)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()
```

# OUTPUT

![Screenshot 2025-04-10 153814](https://github.com/user-attachments/assets/5caf0b8b-bbac-44a2-b70a-fd61dbada6cb)
 
# RESULT / CONCLUSIONS
```
Thus the simulation of pulse Code Modulation is verified and the graph is simulated.
```
