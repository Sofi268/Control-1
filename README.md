# Practico 1
# Resumen Ejercicios 1 Parcial practico

1) Dada una señal de entrada y salida determinar polos y valor de regimen

<img width="400" alt="image" src="https://github.com/user-attachments/assets/f4d5acfe-b086-46e4-98f4-334a917430aa" />

<img width="400" alt="image" src="https://github.com/user-attachments/assets/ba1c0cf6-9c49-4e4a-ad10-5676b8ae0f82" />

## Código Octave ejemplo:

```
clear all; clc; close all; 
pkg load control; 
pkg load symbolic; 
 
syms U C Y A F s X E D B real 
eq1=U-C*Y==A*X+F*s*X; 
eq2=E*s*Y-D*X+B*Y==0; 
Sol=solve(eq1,eq2,U,Y); 
disp('Función de Transferencia del Sistema: ') 
G=factor(Sol.Y/Sol.U,s,'s') 
 
%Valores: 
A=81; 
B=3; 
C=19; 
D=24; 
E=89; 
F=3; 
%Función de Transferencia con valores: 
G=eval(G) 
s=tf('s'); 
G=24/(267*s^2+7218*s+699) 
pole(G) %Polos: 
%Para una entrada escalón unitario: TVF 
disp('Valor Regimen:') 
Vf=24/699 
step(G); %Graficamos
                                                   
                24 
 y1:  ---------------------- 
      267 s^2 + 7218 s + 699 
 
Continuous-time model. 
ans = 
 
  -2.6937e+01     Polo NO dominante 
  -9.7191e-02      Polo dominante 
 
>> %Para una entrada escalón unitario: 
TVF 
disp('Valor Regimen:') 
Vf=24/699 
step(G); %Graficamos 
Valor Regimen: 
Vf = 0.034335 
>> 

```

## Mason
1. 
<img width="1539" height="380" alt="image" src="https://github.com/user-attachments/assets/9be5e979-3190-4f98-a896-51d226edba26" />

```
pkg load symbolic; 
syms M1 M2 l1 l2 D1 D D2 s real; 
 
# Caminos directos de mi sistema 
M1 = 8*(1/s)*((s+10)/(s+100))*(1/s)*4; 
M2 = 8*(10)*(1/s)*(1/s)*4; 
 
# Lazos de mi grafo 
l1 = -1/s; 
l2 = -2*(1/s); 
 
# Determinante y Dk de mi sistema 
D = 1 - (l1+l2) + (l1*l2); 
D1 = 1; 
D2 = 1; 
 
# FdT de mi sistema por algoritmo de Mason 
Y_R = (M1*D1 + M2*D2) / D 
Y_R = simplify(Y_R) 
Y_R = (sym) 
 
      32*(11*s + 1010) 
  ------------------------ 
            / 2          \ 
  (s + 100)*\s  + 3*s + 2/ 
 
>> 
```
 
LUEGO hice distributiva y me dio  D 
no se si estara bien 

<img width="400" alt="image" src="https://github.com/user-attachments/assets/935ea169-75b5-4631-b88e-da8a08e69fe7" />


<img width="400" alt="image" src="https://github.com/user-attachments/assets/482f1489-6f67-4202-b005-b1ed68a33b04" />


## Parametros de rta temporal de primer orden

<img width="500" alt="image" src="https://github.com/user-attachments/assets/80254749-8e11-4bd6-aa6f-235003f49c72" />

<img width="443" height="64" alt="image" src="https://github.com/user-attachments/assets/61cd3579-d22e-438d-8075-8363ff853eec" />

```
 pkg load symbolic 
syms s real 
s=tf('s'); 
K=6 
te=137 %te en banda de +-2% 
T=te/4 %si usara el te cuando se establece 
al 100% divido te/5 
%FUNCIÓN SISTEMA DE PRIMER 
ORDEN 
G=K/(T*s+1) 
%GRÁFICO PARA VERIFICAR 
step(G,350);grid 
ylim([0 6]) 
k = 6 
te = 137 
T = 34.250
```
