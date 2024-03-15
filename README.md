# 20240318
This repository contains programs used in the study 

"Symbolic-numeric and classic-quantum hybrid computation of Hartree-Fock equations" 

by Ichio Kikuchi, Akihito Kikuchi

## How to run the programs

(1) SZ-SYM-HF.py
 
 This Python script yields the objective function ( the total energy of HeH+ ) as a multivariate polynomial.

 $ python SZ-SYM-HF.py

 The variables stand for the following physical qualities.

 (x,y) : the wave function

 e  : the orbital energy

 R : the bond length (fixed at 1.46)

(2) Script-Singular.txt

 This script conducts the symbolic computations and generate the matrices mx, my, me, and mr.

 We use Singular (a CAS package).
 
  $ Singular < Script_Singular.txt

  The eigenvalues of those matrices give the electronic wavefunction (x, y), the orbital energy e, and the bond length R

(3) save_mx.txt, save_my.txt, save_me.txt

These three files contain the raw data of the matrices of mx, my, and me.

The raw data are transformed to Python numpy arrays by the following function.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

import numpy as np

import csv

def getmat(filename):

    rowmx=list()
    
    with open(filename, 'r') as file:
    
        reader = csv.reader(file)
        
        for t in reader:

            rowmx.append(t)

    x=rowmx[0]
    
    y=np.array([eval(t) for t in x])
    
    return np.array(np.array_split(y,8))

mx=getmat('save_mx.txt')    

my=getmat('save_my.txt')    

me=getmat('save_me.txt')    

mx=mx.transpose()

my=my.transpose()

me=me.transpose()

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

