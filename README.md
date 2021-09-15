import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
import sympy as sp



def Rot2D(X, Y, Alpha):
    RX = X*np.cos(Alpha) - Y*np.sin(Alpha)
    RY = X*np.sin(Alpha) + Y*np.cos(Alpha)
    return RX, RY

t = sp.Symbol('t')
phi = 6.5 * t + 1.2 * sp.cos(6 * t)
x = 2 + 6 * sp.sin(6 * t) * sp.cos(phi)
y = 2 + 6 * sp.sin(6 * t) * sp.sin(phi)

Vx = sp.diff(x, t)
print(Vx)

Vy = sp.diff(y, t)
print(Vy)

Vmod = sp.sqrt(Vx * Vx + Vy * Vy)
Wx = sp.diff(Vx, t)
print(Wx)
Wy = sp.diff(Vy, t)
print(Wy)
Wmod = sp.sqrt(Wx * Wx + Wy * Wy)
Wtau = sp.diff(Vmod,t)
rho = (Vmod*Vmod)/sp.sqrt(Wmod*Wmod-Wtau*Wtau)


T = np.linspace(0, 10, 1000)
X = np.zeros_like(T)
Y = np.zeros_like(T)
VX = np.zeros_like(T)
VY = np.zeros_like(T)
WY=np.zeros_like(T)
WX=np.zeros_like(T)
Rho=np.zeros_like(T)
Phi=np.zeros_like(T)


for i in np.arange(len(T)):
    X[i] = sp.Subs(x, t, T[i])
    Y[i] = sp.Subs(y, t, T[i])
    VX[i] = sp.Subs(Vx, t, T[i])
    VY[i] = sp.Subs(Vy, t, T[i])
    WY[i]=sp.Subs(Wy,t,T[i])
    WX[i] = sp.Subs(Wx, t, T[i])
    Rho[i]=sp.Subs(rho,t,T[i])
    Phi[i]=sp.Subs(phi,t,T[i])

fig = plt.figure()

ax1 = fig.add_subplot(1, 1, 1)
ax1.axis('equal')


ax1.plot(X, Y)

