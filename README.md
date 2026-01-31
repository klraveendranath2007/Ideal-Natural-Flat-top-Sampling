# IDEAL, NATURAL, & FLAT-TOP -SAMPLING
# AIM
To write a simple Python program for the construction and reconstruction of ideal, natural, and flat-top sampling.
# TOOLS REQUIRED
Python IDE with Numpy and Scipy
# PROGRAM
### IDEAL SAMPLING
```import numpy as np
import matplotlib.pyplot as plt

fs = 100
f = 5
t = np.arange(0, 1, 1/fs)
x = np.sin(2*np.pi*f*t)

# Continuous signal
plt.figure(figsize=(10, 3))
plt.plot(t, x)
plt.title("Continuous Signal")
plt.grid()
plt.show()

# Ideal sampling
plt.figure(figsize=(10, 3))
plt.stem(t, x)
plt.title("Ideal Sampling")
plt.grid()
plt.show()

# Reconstruction (Interpolation)
t_rec = np.linspace(0, 1, 1000)
x_rec = np.interp(t_rec, t, x)

plt.figure(figsize=(10, 3))
plt.plot(t_rec, x_rec)
plt.title("Reconstructed Signal")
plt.grid()
plt.show()
```
### NATURAL SAMPLING
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

t = np.linspace(0,1,1000)
x = np.cos(2*np.pi*5*t)

p = ((t*50)%1 < 0.5)        # pulse train
xn = x * p                 # natural sampling

b,a = butter(4, 10/(0.5*1000))   # low-pass filter
xr = lfilter(b, a, xn)           # reconstruction

plt.figure(figsize=(10, 3))
plt.plot(t,x); 
plt.title("Message Signal");
plt.grid(); 
plt.show()

plt.figure(figsize=(10, 3))
plt.plot(t,xn);
plt.title("Natural Sampling");
plt.grid();
plt.show()

plt.figure(figsize=(10, 3))
plt.plot(t,xr);
plt.title("Reconstructed Signal");
plt.grid();
plt.show()
```
### FLAT-TOP SAMPLING
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs = 1000
t = np.linspace(0, 1, fs)
x = np.sin(2*np.pi*5*t)

Ts = fs//50                         # sampling interval
xh = np.repeat(x[::Ts], Ts)[:fs]   # flat-top (sample & hold)

b, a = butter(4, 10/(0.5*fs))      # low-pass filter
xr = filtfilt(b, a, xh)            # reconstruction (zero-phase)

plt.figure(figsize=(10, 3));plt.plot(t, x);
plt.title("Message Signal");
plt.grid(); 
plt.show()

plt.figure(figsize=(10, 3));
plt.plot(t, xh);
plt.title("Flat-Top Sampling");
plt.grid();
plt.show()

plt.figure(figsize=(10, 3));
plt.plot(t, xr);
plt.title("Reconstructed Signal");
plt.grid(); 
plt.show()
```
# OUTPUT WAVEFORM
### IDEAL SAMPLING
<img width="450" height="451" alt="image" src="https://github.com/user-attachments/assets/d0868cda-83f2-4780-a528-a7beafadf7e3" />

### NATURAL SAMPLING
<img width="450" height="451" alt="image" src="https://github.com/user-attachments/assets/b4db140a-b4b0-4785-b172-e68081377b3f" />

### FLAT-TOP SAMPLING
<img width="450" height="453" alt="image" src="https://github.com/user-attachments/assets/86380f08-fd2a-4e8d-895f-8bd9bc1958cc" />

# RESULT
Thus, the python program for ideal sampling, natural sampling and flat-top sampling has been executed and verified successfully.

