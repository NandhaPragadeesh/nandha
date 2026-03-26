# SKILL ASSESSMENT 2

### 🎯 **Aim**
Task 1:
Generate a composite audio signal consisting of three sine waves (500 Hz, 1500 Hz, 3000 Hz).

Sample the signal at 16 kHz.

Downsample the signal by a factor of 4.

Plot

Original signal

Downsampled signal

Compare the frequency spectrum of both signals.

Task 2:
Generate an ECG-like signal.

Design a low-pass FIR filter.

Apply the filter before decimation by factor 3.

Plot:

Original signal

Filtered signal

Decimated signal

### ⚙️ **Components Required**
PC installed scilab

---

### 💻 **Program**


```c
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import decimate

# Sampling parameters
fs = 16000
t = np.arange(0, 0.02, 1/fs)

# Composite signal
x = (np.sin(2*np.pi*500*t) +
     np.sin(2*np.pi*1500*t) +
     np.sin(2*np.pi*3000*t))

# Downsample by factor 4
factor = 4
x_down = x[::factor]
fs_down = fs//factor
t_down = np.arange(0,len(x_down))/fs_down

# -------- Plot signals ----------
plt.figure(figsize=(10,6))

plt.subplot(2,1,1)
plt.plot(t, x)
plt.title("Original Signal (16 kHz)")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.subplot(2,1,2)
plt.plot(t_down, x_down)
plt.title("Downsampled Signal (4 kHz)")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.tight_layout()
plt.show()

# -------- Frequency Spectrum --------
X = np.fft.fft(x)
f = np.fft.fftfreq(len(x),1/fs)

X_down = np.fft.fft(x_down)
f_down = np.fft.fftfreq(len(x_down),1/fs_down)

plt.figure(figsize=(10,6))

plt.subplot(2,1,1)
plt.plot(f[:len(f)//2], np.abs(X[:len(X)//2]))
plt.title("Original Spectrum")

plt.subplot(2,1,2)
plt.plot(f_down[:len(f_down)//2], np.abs(X_down[:len(X_down)//2]))
plt.title("Downsampled Spectrum")

plt.tight_layout()
plt.show()

```
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import firwin, lfilter

# Sampling
fs = 360
t = np.arange(0, 2, 1/fs)

# ECG-like signal
ecg = (np.sin(2*np.pi*1.7*t) +
       0.5*np.sin(2*np.pi*40*t) +
       0.2*np.random.randn(len(t)))

# FIR Low pass filter
cutoff = 20
numtaps = 51
h = firwin(numtaps, cutoff/(fs/2))

# Filter signal
filtered = lfilter(h, 1, ecg)

# Decimation factor
M = 3
decimated = filtered[::M]
t_dec = t[::M]

# -------- Plotting ----------
plt.figure(figsize=(10,8))

plt.subplot(3,1,1)
plt.plot(t, ecg)
plt.title("Original ECG Signal")

plt.subplot(3,1,2)
plt.plot(t, filtered)
plt.title("Filtered ECG Signal")

plt.subplot(3,1,3)
plt.plot(t_dec, decimated)
plt.title("Decimated ECG Signal")

plt.tight_layout()
plt.show()
```
---
### OUTPUT
<img width="755" height="844" alt="Screenshot 2026-03-26 221628" src="https://github.com/user-attachments/assets/0a80f95c-64c2-4638-a431-c536e233eab6" />

<img width="437" height="361" alt="Screenshot 2026-03-26 221713" src="https://github.com/user-attachments/assets/30a0012a-8907-4176-8bc7-b476e7808cba" />

---
### RESULT
Thus the output is successfully generated
