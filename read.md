# To run copy paste the raw data below into an application or online website capable of running python 
# If the necsasary library are not installed, type pip install then the name of the missing libary in the console below
# For PyCharm to install packages, go to the menu at the top click view -> tool windows -> Python Packages and type the names of the packages in the search bar below

# the following program solves the ODE Amdahlâ€™s Law

# import required libraries
import numpy as np
from scipy.integrate import odeint
import matplotlib.pyplot as plt

# function that returns ds/dt
def model(s,n,f):
    dsdn = f/(((-f * n) + n + f) * ((-f * n) + n + f))
    #print(dsdn)
    return dsdn

# initial condition
s0 = 1

# x values increasing from 1 to 50
n = np.linspace(1,50, 1000)
# solve ODEs
f = 1
y1 = odeint(model,s0,n,args=(f,))
f = 0.95
y2 = odeint(model,s0,n,args=(f,))
f = 0.90
y3 = odeint(model,s0,n,args=(f,))
f = 0.75
y4 = odeint(model,s0,n,args=(f,))
f = 0.50
y5 = odeint(model, s0, n, args=(f,))

# plot results
plt.plot(n,y1,'r-',linewidth=2,label='p=1.00')
plt.plot(n,y2,'b--',linewidth=2,label='p=0.95')
plt.plot(n,y3,'g:',linewidth=2,label='p=0.90')
plt.plot(n,y4,'y+',linewidth=2,label='p=0.75')
plt.plot(n,y5,'md',linewidth=2,label='p=0.50')
plt.xlabel('Number of Processors (n)')
plt.ylabel('Speedup')
plt.legend()
plt.show()

