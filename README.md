# IIR-FILTER-DESIGN

# EXP 3 B: DESIGN OF LOW PASS CHEBYSHEV IIR FILTER USING BILINEAR TRANSFORMATION

## AIM: 

 To a design of low pass Chebyshev IIR filter using Bilinear Transformation.

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM: 
```
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
 
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');

//Order of the filter  
N=acosh(sqrt(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1)))/(acosh(omegas/omegap)); 
disp(N,'N='); 
N=ceil(N); 
disp(N,'Round off value of N=');
 
//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac=');
Epsilon = sqrt ((10^(0.1*alphap))-1);
disp(Epsilon,'Epsilon='); 
[pols ,gn] = zpch1(N, Epsilon,omegap ); 
disp(gn,'Gain'); 
disp(pols,'Poles'); 
hs=poly(gn,'s','coeff')/real(poly(pols,'s')); 
disp(hs,'Analog Low pass Chebyshev Filter Transfer function');
z=poly(0,'z');//Defining variable z 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp(Hz,'Digital LPF Transfer function H(Z)='); 
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude '); 
title(' Frequency Response of Chebyshev IIR LPF');
```
## CALCUATION:

<img width="941" height="1600" alt="image" src="https://github.com/user-attachments/assets/da78074d-62ad-40b3-8d6e-e973c194371d" />

<img width="981" height="1600" alt="image" src="https://github.com/user-attachments/assets/d25a04a7-0a7e-4642-a7ea-3d9477ee2ec3" />

<img width="1119" height="1415" alt="image" src="https://github.com/user-attachments/assets/2cdefcaf-ff0f-478c-b3fc-d46cd4d1456e" />
## OUTPUT: 



<img width="826" height="995" alt="image" src="https://github.com/user-attachments/assets/807dedb3-d7b6-4bc2-a57b-19bff34c22b2" />
<img width="757" height="706" alt="image" src="https://github.com/user-attachments/assets/69ff0397-206a-456f-a7f2-84d1773e0fbb" />

## RESULT: 
Thus design of Chebyshev Low pass IIR filter waveforms were plotted and output was
verified.
