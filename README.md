# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques

## AIM:
To simulate digital modulation techniques such as:
1. Amplitude Shift Keying (ASK)
2. Frequency Shift Keying (FSK)
3. Phase Shift Keying (PSK

## SOFTWARE REQUIRED:
python (Google Colab)

## ALGORITHM:


### Amplitude Shift Keying (ASK)
1. Define a binary input signal (e.g., [1, 0, 1, 1, 0]).
2. Set a carrier frequency.
3. Multiply the carrier by the bit (1 or 0) to get ASK modulated signal.
4. Plot the input signal, carrier, and ASK signal.



### Frequency Shift Keying (FSK)
1. Define two carrier frequencies: one for bit 1, another for bit 0.
2. Multiply bit 1 with one frequency, bit 0 with the other.
3. Concatenate all modulated bits.
4. Plot the input signal and FSK signal.



### Phase Shift Keying (PSK)
1. Use a single frequency carrier.
2. For bit 1, send the signal with phase 0.
3. For bit 0, invert the signal (phase shift by 180°).
4. Plot the input signal and PSK signal.


## PROGRAM:
```
import numpy as np
import matplotlib.pyplot as plt

# Binary data
data = [1, 0, 1, 1, 0]
bit_duration = 1
Fs = 1000  # Sampling rate
t_bit = np.linspace(0, bit_duration, Fs, endpoint=False)

# Carrier frequencies
f1 = 10  # FSK freq for bit 1
f0 = 2   # FSK freq for bit 0
f_c = 5  # Common carrier for ASK and PSK

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
plt.plot(time, digital, color='brown')
plt.title("Digital Input Signal")
plt.ylabel("Amplitude")
plt.grid(True)

# ASK Signal
plt.subplot(4, 1, 2)
plt.plot(time, ask_signal, color='red')
plt.title("Amplitude Shift Keying (ASK using Cosine Carrier)")
plt.ylabel("Amplitude")
plt.grid(True)

# FSK Signal
plt.subplot(4, 1, 3)
plt.plot(time, fsk_signal, color='orange')
plt.title("Frequency Shift Keying (FSK)")
plt.ylabel("Amplitude")
plt.grid(True)

# PSK Signal
plt.subplot(4, 1, 4)
plt.plot(time, psk_signal, color='black')
plt.title("Phase Shift Keying (PSK)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()
```

## OUTPUT:
### ASK OUTPUT:
![image](https://github.com/user-attachments/assets/c2990b00-396a-4752-ac5a-3e42d0be5557)

### FSK OUTPUT:
![image](https://github.com/user-attachments/assets/20fc4e08-8ecc-4f5a-a133-6b33585c32dc)

### PSK OUTPUT:
![image](https://github.com/user-attachments/assets/6c7e2e19-64b7-4615-84fc-a359f5715087)

 
## RESULT:
The simulation of digital modulation techniques such as ASK, FSK, and PSK was successfully implemented using Python and the waveform is obtained.
