# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)


# Program :

import numpy as np
import math
import scipy.stats
L=[int(i) for i in input().split()]
N=len(L)
M=max(L) 
X=[]
f=[]
for i in range (M+1):
    c = 0
    for j in range(N):
        if L[j]==i:
            c=c+1
    f.append(c)
    X.append(i)
Sff=np.sum(f)
p=[]
for i in range(M+1):
    p.append(f[i]/Sff) 
mean=np.inner(X,p)
p=[]
E=[]
xi=[]
print("X P(X=x) Obs.Fr Exp.Fr xi")
print("--------------------------")
for x in range(M+1):
    p.append(math.exp(-mean)*mean**x/math.factorial(x))
    E.append(p[x]*Sff)
    xi.append((f[x]-E[x])**2/E[x])
    print("%2.2f %2.3f %4.2f %3.2f %3.2f"%(x,p[x],f[x],E[x],xi[x]))
print("--------------------------")
cal_chi2_sq=np.sum(xi)
print(f"Calculated value of Chi square is {cal_chi2_sq:.2f}")
table_chi2=scipy.stats.chi2.ppf(1-.01,df=M)
print(f"Table value of chi square at 1 level is {table_chi2:.2f}")
if cal_chi2_sq<table_chi2:
    print("The given data can be fitted in poisson Distribution at 1% LOS")
else:
    print("The given data cannot be fitted in Poisson Distribution at 1% LOS")
 

# Output : 
1 2 3 4 5 6 7 8 9 10
X P(X=x) Obs.Fr Exp.Fr xi
--------------------------
0.00 0.004 0.00 0.04 0.04
1.00 0.022 1.00 0.22 2.67
2.00 0.062 1.00 0.62 0.24
3.00 0.113 1.00 1.13 0.02
4.00 0.156 1.00 1.56 0.20
5.00 0.171 1.00 1.71 0.30
6.00 0.157 1.00 1.57 0.21
7.00 0.123 1.00 1.23 0.04
8.00 0.085 1.00 0.85 0.03
9.00 0.052 1.00 0.52 0.45
10.00 0.029 1.00 0.29 1.79
--------------------------
Calculated value of Chi square is 5.98
Table value of chi square at 1 level is 23.21
The given data can be fitted in poisson Distribution at 1% LOS


# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
