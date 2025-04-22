# EXP.NO.9-Simulation-of-Pulse-Code-Modulation

## AIM
To Simulate of PCM using Python.
## SOFTWARE REQUIRED
Google Collab
## ALGORITHMS
1. Generate an analog signal (e.g., sine wave).
2. Sample the signal at regular intervals (sampling).
3. Quantize the sampled values to the nearest levels (quantization).
4. Convert the quantized values into binary code (encoding).
5. Plot the: Original analog signal Sampled signal Quantized signal Encoded PCM output
## PROGRAM
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
## OUTPUT
![image](https://github.com/user-attachments/assets/fc62aa8c-e5fa-4c3c-9cac-9bf29a41589e)

## RESULT / CONCLUSIONS
To Simulate of PCM using Python was verified successfully.
