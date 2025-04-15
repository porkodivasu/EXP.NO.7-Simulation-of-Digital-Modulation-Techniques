# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques
7. Simulation of Digital Modulation Techniques Such as
   i) Amplitude Shift Keying (ASK)
   ii) Frequency Shift Keying (FSK)
   iii) Phase Shift Keying (PSK)

# AIM
The objective of this experiment is to simulate and analyze three fundamental digital modulation techniques:
Amplitude Shift Keying (ASK)
Frequency Shift Keying (FSK)
Phase Shift Keying (PSK)
By implementing these techniques, you will gain practical insights into how digital data can be transmitted over communication channels using variations in amplitude, frequency, or phase of a carrier signal.​


# SOFTWARE REQUIRED
personal computer
python
# ALGORITHMS
1. Amplitude Shift Keying (ASK)
Modulation Algorithm (ASK)
Input: Digital bit stream: b[n] where n is the bit index.

Carrier Signal: Generate a high-frequency carrier signal: c(t) = A_c * cos(2πf_c t) where A_c is the carrier amplitude and f_c is the carrier frequency.

Modulation: For each bit b[n]:

If b[n] = 1: Set the amplitude of the carrier to A_c.

If b[n] = 0: Set the amplitude of the carrier to 0.

Output: Modulated signal: s(t) = b[n] * A_c * cos(2πf_c t) for each bit b[n].​

Demodulation Algorithm (ASK)
Input: Received modulated signal r(t).

Envelope Detection: Extract the envelope of r(t) to obtain |r(t)|.

Thresholding: Compare |r(t)| with a predefined threshold T:

If |r(t)| > T: Decode as b[n] = 1.

If |r(t)| ≤ T: Decode as b[n] = 0.

Output: Decoded bit stream b[n].​
Wikipedia
+3
Wikipedia
+3
Electronics Coach
+3

2. Frequency Shift Keying (FSK)
Modulation Algorithm (FSK)
Input: Digital bit stream: b[n].

Carrier Frequencies: Define two frequencies:

f_0: Frequency corresponding to bit 0.

f_1: Frequency corresponding to bit 1.

Modulation: For each bit b[n]:

If b[n] = 1: Generate a signal with frequency f_1.

If b[n] = 0: Generate a signal with frequency f_0.

Output: FSK signal: s(t) = cos(2πf_b t) where f_b is either f_0 or f_1 depending on b[n].​

Demodulation Algorithm (FSK)
Input: Received FSK signal r(t).

Frequency Detection: Analyze the frequency components of r(t) to determine the dominant frequency:

If dominant frequency is f_1: Decode as b[n] = 1.

If dominant frequency is f_0: Decode as b[n] = 0.

Output: Decoded bit stream b[n].​
Wikipedia
+3
Wikipedia
+3
GeeksforGeeks
+3

3. Phase Shift Keying (PSK)
Modulation Algorithm (PSK)
Input: Digital bit stream: b[n].

Carrier Signal: Generate a high-frequency carrier signal: c(t) = A_c * cos(2πf_c t) where A_c is the carrier amplitude and f_c is the carrier frequency.

Phase Mapping: Define phase shifts for each bit:

0: Phase shift of 0°.

1: Phase shift of π radians (180°).

Modulation: For each bit b[n]:

If b[n] = 1: Modulate the carrier with a phase shift of π.

If b[n] = 0: Modulate the carrier with no phase shift.

Output: PSK signal: s(t) = A_c * cos(2πf_c t + φ[n]) where φ[n] is the phase shift corresponding to b[n].​

Demodulation Algorithm (PSK)
Input: Received PSK signal r(t).

Phase Detection: Determine the phase of r(t):

If phase is 0°: Decode as b[n] = 0.

If phase is π: Decode as b[n] = 1.

Output: Decoded bit stream b[n].​
# PROGRAM
ASK:

//Python Code 
import numpy as np 
import matplotlib.pyplot as plt 
# Parameters 
data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted 
bit_duration = 1  # Duration of each bit in seconds 
fc = 10  # Carrier frequency in Hz 
amplitude = 2  # Carrier amplitude 
sampling_rate = 1000  # Number of samples per second 
# Time vector 
t = np.arange(0, bit_duration * len(data), 1/sampling_rate) 
# Message signal 
message_signal = np.repeat(data, sampling_rate * bit_duration) 
# Carrier signal 
carrier_signal = amplitude * np.sin(2 * np.pi * fc * t) 
# ASK modulation 
ask_signal = amplitude * message_signal * np.sin(2 * np.pi * fc * t) 
# Plotting 
plt.figure(figsize=(12, 8)) 
plt.subplot(3, 1, 1) 
plt.plot(t, message_signal) 
plt.title('Message Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 2) 
plt.plot(t, carrier_signal) 
plt.title('Carrier Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 3) 
plt.plot(t, ask_signal) 
plt.title('ASK Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.tight_layout() 
plt.show()

FSK:

import numpy as np 
import matplotlib.pyplot as plt 
# Parameters 
data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted 
bit_duration = 1  # Duration of each bit in seconds 
fc1 = 15  # Frequency for binary 1 in Hz 
fc0 = 10  # Frequency for binary 0 in Hz 
amplitude = 2  # Carrier amplitude 
sampling_rate = 1000  # Number of samples per second 
# Time vector 
t = np.arange(0, bit_duration * len(data), 1/sampling_rate) 
# Message signal 
message_signal = np.repeat(data, sampling_rate * bit_duration) 
# FSK modulation 
fsk_signal = [] 
for bit in data: 
if bit == 1: 
fsk_signal.extend(amplitude * np.sin(2 * np.pi * fc1 * np.arange(0, bit_duration, 1/sampling_rate))) 
else: 
fsk_signal.extend(amplitude * np.sin(2 * np.pi * fc0 * np.arange(0, bit_duration, 1/sampling_rate))) 
fsk_signal = np.array(fsk_signal) 
# Plotting 
plt.figure(figsize=(12, 8)) 
plt.subplot(3, 1, 1) 
plt.plot(t, message_signal) 
plt.title('Message Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 2) 
plt.plot(t, amplitude * np.sin(2 * np.pi * fc1 * t), label='Carrier for 1') 
plt.plot(t, amplitude * np.sin(2 * np.pi * fc0 * t), label='Carrier for 0') 
plt.title('Carrier Signals') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.legend() 
plt.subplot(3, 1, 3) 
plt.plot(t, fsk_signal) 
plt.title('FSK Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.tight_layout() 
plt.show()

PSK:

import numpy as np 
import matplotlib.pyplot as plt 
# Parameters 
data = [1, 0, 1, 0, 1, 1, 0, 1]  # Binary data to be transmitted 
bit_duration = 1  # Duration of each bit in seconds 
fc = 10  # Carrier frequency in Hz 
amplitude = 2  # Carrier amplitude 
sampling_rate = 1000  # Number of samples per second 
# Time vector 
t = np.arange(0, bit_duration * len(data), 1/sampling_rate) 
# Message signal 
message_signal = np.repeat(data, sampling_rate * bit_duration) 
# PSK modulation 
psk_signal = [] 
for bit in data: 
if bit == 1: 
psk_signal.extend(amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate))) 
else: 
psk_signal.extend(amplitude * np.sin(2 * np.pi * fc * np.arange(0, bit_duration, 1/sampling_rate) + 
np.pi)) 
psk_signal = np.array(psk_signal) 
# Plotting 
plt.figure(figsize=(12, 8)) 
plt.subplot(3, 1, 1) 
plt.plot(t, message_signal) 
plt.title('Message Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 2) 
plt.plot(t, amplitude * np.sin(2 * np.pi * fc * t)) 
plt.title('Carrier Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.subplot(3, 1, 3) 
plt.plot(t, psk_signal) 
plt.title('PSK Signal') 
plt.xlabel('Time') 
plt.ylabel('Amplitude') 
plt.tight_layout() 
plt.show()
# OUTPUT
ASK:
 ![Screenshot (14)](https://github.com/user-attachments/assets/b1070409-cc25-41c1-94e7-5f9933e53c6b)
FSK:
![Screenshot 2025-04-15 141658](https://github.com/user-attachments/assets/bf956c1f-de57-40e5-9ce5-02aedff85b3b)
PSK:
![Screenshot (45)](https://github.com/user-attachments/assets/9d973518-ad64-4891-aeea-3a04191ba280)

# RESULT / CONCLUSIONS
