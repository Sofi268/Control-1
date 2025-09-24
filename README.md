# Resumen Ejercicios 1 Parcial practico

## Dada una señal de entrada y salida determinar polos y valor de regimen

```
clear all; clc; close all; 
pkg load control; 
pkg load symbolic; 
 
syms U C Y A F s X E D B real 
% Se puede obtener facilmente la funcion de transferencia pasando al dominio de laplace y despejando 
% Despeje
% Y(s)/U(s) = 

% Reemplazo de valores
G = algo

root(G)
%TVF con G

```

## Mason

**Primero:** obtener las ganancias de camino directo
M = ganancias
**Segundo:** determinante
Lazos = ganancias 
Det = 1- lazos indiv + lazos bijuntos ...
**Tercero:** Det k
Parte del det que no comparte nodos con el camino dir
**Cuarto:** Formula
G = (M.Dk)/D

```
clc; clear all; close all; 
pkg load symbolic; 
syms G1 G2 G3 G4 G5 G6 H2 H4 H6 s real; 
 
# Def de FdT
G1 = 
G2 = 
H1 = 

# Caminos directos de mi sistema
M1 = G1*G2*G3*G4*G5; 
M2 = G1*G6*G5; 
 
# Lazos de mi grafo 
l1 = -H2*G2; 
l2 = -H6*G6; 
l3 = -H4*G1*G2*G3*G4; 
l4 = -H4*G1*G6; 
 
# Determinante y Dk de mi sistema 
D = 1 - (l1+l2+l3+l4) + (l1*l2 + l2*l3); 
D1 = 1 - l2; 
D2 = 1; 
 
# FdT de mi sistema por algoritmo de Mason 
G = (M1*D1 + M2*D2) / D 
G = simplify(G)
```

## Parametros de rta temporal de segundo orden:
Solo con ver el grafico estamos

## Parametros de rta temporal de segundo orden:
```
clear all; clc; close all; 
pkg load control; 
pkg load symbolic; 

K = ;         
Vmax = ;    
Tp = ;         
Te = ;   

% Sobrepasamiento maximo 
Mp = (Vmax-K)/(K) 
Mp = 0.2500 
psita = sqrt((log(Mp)^2)/(log(Mp)^2+pi^2)) % Coeficiente de amortiguamiento 
Wn = pi/(Tp*sqrt(1-psita^2)) % Frecuencia natural  

```
--------------------------------------------------------------- Ejemplos ------------------------------------------------------------------------
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
2. 
<img width="922" height="443" alt="image" src="https://github.com/user-attachments/assets/82b28d96-c6d6-4f25-958a-d6db0b1515ef" />

<img width="950" height="369" alt="image" src="https://github.com/user-attachments/assets/6762ca26-05bc-479d-bd04-2b8a745b43cd" />


```
pkg load symbolic; 
syms M1 M2 G1 G2 G3 l1 l2 l3 D1 D D2 s real; 
G1=5; 
G2=1/(s+6); 
G3= 2/(s+1) 
# Caminos directos de mi sistema 
M1 = G1*1*G3; 
M2 = G1*1*G2*(-1)*1*(-1)*G3; 
Y_R = (sym) 
/ 2            
\ 
5*\s  + 13*s + 43/ -------------------------- 
3       
2 
3*s  + 48*s  + 238*s + 348 
# Lazos de mi grafo 
l1 = -G1; 
l2 = -G2; 
l3=-G3; 
# Determinante y Dk de mi sistema 
D = 1 - (l1+l2+l3) + (l1*l2+ l1*l3+ l2*l3); 
>> roots(Y_R) 
```

Lo compile y no me daba asi que lo hice con la 
calculadora y me daba  -2.62        
(este seria el polo dominante) -6 -7.38

## Parametros de rta temporal de primer orden:
K= 6 (valor de regimen)
T = 4/t en que llega al 98% = 31 s

<img width="866" height="517" alt="image" src="https://github.com/user-attachments/assets/4665da63-7df0-4c68-b3a6-efe248dd189f" />

