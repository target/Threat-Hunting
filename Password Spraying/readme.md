## Password Spraying
This folder contains notebooks that look through authentication data, and try to find evidence of password spraying attacks.

### hunt_password_spray_with_fourier
This notebook accepts a CSV file of timestamped authentication failures, from any auth portal.  It then applies a Fast Fourier
transform, per login account, to try to find any metronomic logon failures that could be consistent with a password spraying script.
Prerequisite: Jupyter Notebook (https://jupyter.org/install), plus a .csv file of authentication failure data.

#### Example
The following examples show an instance of a strong periodic signal at around 0.0033Hz in the frequency domain, which corresponds 
to a period of 300sec when converted to the time domain. 
![frequency domain](frequencydomain.png)
![time domain](timedomain.png)
