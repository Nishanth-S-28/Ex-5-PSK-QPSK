

# Aim

Write a simple Python program for the modulation and demodulation of PSK and QPSK.

# Tools required

Python IDE with Numpy and Scipy Libraries or Colab

# Program

BPSK (PSK):
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Low-pass filter
def lowpass(x, fc, fs):

    b, a = butter(4, fc / (0.5 * fs))

    return lfilter(b, a, x)

# Parameters
fs = 1000
fc = 50
bit_rate = 10
T = 1

# Time vector
t = np.linspace(0, T, fs, endpoint=False)

# Message signal
bits = np.random.randint(0, 2, bit_rate)

bit_duration = fs // bit_rate

msg = np.repeat(bits, bit_duration)

# Carrier signal
carrier = np.sin(2 * np.pi * fc * t)

# BPSK Modulation
psk_signal = np.sin(
    2 * np.pi * fc * t + np.pi * msg
)

# Demodulation
demodulated = psk_signal * carrier

filtered_signal = lowpass(
    demodulated,
    fc,
    fs
)

# Decode bits
decoded_bits = (
    filtered_signal[::bit_duration] < 0
).astype(int)

# Plotting
plt.figure(figsize=(10, 8))


plt.suptitle("NAME : NISHANTH S\nREG NO : 212224060175", 
             fontsize=12, fontweight='bold')


# Message signal
plt.subplot(4, 1, 1)
plt.plot(t, msg)
plt.title("Message Signal")
plt.grid()

# Carrier signal
plt.subplot(4, 1, 2)
plt.plot(t, carrier)
plt.title("Carrier Signal")
plt.grid()

# PSK signal
plt.subplot(4, 1, 3)
plt.plot(t, psk_signal)
plt.title("BPSK Modulated Signal")
plt.grid()

# Demodulated bits
plt.subplot(4, 1, 4)
plt.step(
    range(len(decoded_bits)),
    decoded_bits,
    where='mid'
)

plt.title("Demodulated Bits")
plt.grid()

plt.tight_layout()
plt.show()
```
QPSK:
~~~
import numpy as np
import matplotlib.pyplot as plt

# Input symbols
symbols = ['10', '11', '11', '10']

num_sym = len(symbols)

# Time axis
t = np.arange(-np.pi, np.pi, 0.1)

# QPSK phase signals
s00 = np.sin(t + np.pi / 4)
s01 = np.sin(t + 3 * np.pi / 4)
s10 = np.sin(t + 5 * np.pi / 4)
s11 = np.sin(t + 7 * np.pi / 4)

# Modulation
mod_signal = []
input_bits = []

for sym in symbols:

    if sym == '00':
        mod_signal.extend(s00)
        input_bits.extend([0, 0])

    elif sym == '01':
        mod_signal.extend(s01)
        input_bits.extend([0, 1])

    elif sym == '10':
        mod_signal.extend(s10)
        input_bits.extend([1, 0])

    else:
        mod_signal.extend(s11)
        input_bits.extend([1, 1])

# Input waveform
inp_time = np.repeat(
    np.arange(len(input_bits)),
    2
)

inp_wave = np.repeat(input_bits, 2)

# Demodulation
demod_bits = []

sample_pt = 2

for i in range(num_sym):

    val = mod_signal[i * len(t) + sample_pt]

    if val <= -0.77:
        demod_bits.extend([0, 0])

    elif val < -0.63:
        demod_bits.extend([0, 1])

    elif val >= 0.77:
        demod_bits.extend([1, 0])

    else:
        demod_bits.extend([1, 1])

# Demodulated waveform
demod_time = np.repeat(
    np.arange(len(demod_bits)),
    2
)

demod_wave = np.repeat(demod_bits, 2)

# Plotting
plt.figure(figsize=(10, 6))


plt.suptitle("NAME : NISHANTH S\nREG NO : 212224060175", 
             fontsize=12, fontweight='bold')



# Input bits
plt.subplot(3, 1, 1)
plt.plot(
    inp_time,
    inp_wave,
    drawstyle='steps-post'
)

plt.title("Input Binary Data")
plt.ylim(-0.5, 1.5)
plt.grid()

# QPSK signal
plt.subplot(3, 1, 2)
plt.plot(mod_signal)

plt.title("QPSK Modulated Signal")
plt.grid()

# Demodulated signal
plt.subplot(3, 1, 3)
plt.plot(
    demod_time,
    demod_wave,
    drawstyle='steps-post'
)

plt.title("Demodulated Signal")
plt.ylim(-0.5, 1.5)
plt.grid()

plt.tight_layout()
plt.show()
~~~
# Output Waveform

PSK:
<img width="989" height="789" alt="image" src="https://github.com/user-attachments/assets/9a737342-1e28-4464-916a-23c9f2be34f2" />


QPSK:

<img width="989" height="593" alt="image" src="https://github.com/user-attachments/assets/20e6984e-6bb1-49c1-9d83-b31a42696d0f" />


# Results

Thus, the Python program for the modulation and demodulation of PSK and QPSK has been successfully simulated and verified.
