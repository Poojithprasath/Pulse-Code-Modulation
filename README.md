# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM, and DM.
# Software required
Google Collab
# Program
# Pulse Code Modulation
```sci
#PCM
import numpy as np, matplotlib.pyplot as plt

fs,f,d,q=5000,50,0.1,16
t=np.linspace(0,d,int(fs*d),0)
m=np.sin(2*np.pi*f*t)
c=np.sign(np.sin(2*np.pi*200*t))

s=(m.max()-m.min())/q
qm=np.round(m/s)*s

ttl=["Message Signal (Analog)",
     "Clock Signal (Increased Frequency)",
     "PCM Modulated Signal (Quantized)",
     "PCM Demodulation Signal"]

sig=[m,c,qm,qm]

plt.figure(figsize=(12,10))

for i in range(4):
    plt.subplot(4,1,i+1)
    plt.step(t,sig[i]) if i==2 else plt.plot(t,sig[i],linestyle='--'if i==3 else '-')
    plt.title(ttl[i])
    plt.xlabel("Time [s]")
    plt.ylabel("Amplitude")
    plt.grid()

plt.tight_layout()
plt.show()


```
# Delta Modulation
```sci
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs, f, T, d = 10000, 10, 1, 0.1

t = np.arange(0, T, 1/fs)
m = np.sin(2*np.pi*f*t)

e, dm, p = [], [0], 0

for s in m:
    b = 1 if s > p else 0
    e.append(b)
    p += d if b else -d
    dm.append(p)

x = [0]
for b in e:
    x.append(x[-1] + d if b else x[-1] - d)

b, a = butter(4, 20/(0.5*fs), 'low')
y = filtfilt(b, a, x)

titles = ['Original Signal',
          'Delta Modulated Signal',
          'Demodulated & Filtered Signal']

signals = [m, dm[:-1], y[:-1]]

plt.figure(figsize=(12,6))

for i in range(3):
    plt.subplot(3,1,i+1)
    
    if i == 1:
        plt.step(t, signals[i], where='mid')
    else:
        plt.plot(t, signals[i],
                 linestyle='dotted' if i==2 else '-')
    
    plt.legend([titles[i]])
    plt.grid()

plt.tight_layout()
plt.show()

```
# Output Waveform

# Pulse-code-Modulation
<img width="1233" height="1024" alt="image" src="https://github.com/user-attachments/assets/b35799b3-bf33-442e-9e9b-575b7b4a1ffc" />

# Delta-Modulation

<img width="1499" height="730" alt="image" src="https://github.com/user-attachments/assets/2aa20500-4db8-4853-98cd-2f9908123584" />


# Results
The analog signal was successfully encoded and reconstructed using PCM and DM techniques in Python, verifying their working principles..
