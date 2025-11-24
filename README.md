# tkeBudgetsOF
This is a dynamic code to be used with OpenFOAM. It has been tested with OpenFOAM.com v2206, v2312, and v2506.

The purpose is to evaluate the turbulent kinetic energy (TKE) budget terms. 

It's developed to work with the twoLiquidMixingFoam solver; however, it can be easily modified to run with pisoFoam or pimpleFoam. To do so, in the PVTk term, remove the division by rho.

Moreover, the code MUST work in parallel with OpenFoam's _fieldAveraging_ function, as the following fields must be evaluated first:
  1. UMean
  2. UPrime2Mean
  3. pMean or p_rghMean
  4. turbulenceProperties:RMean

The field turbulenceProperties:R is the modelled SGS Reynolds Stresses, and it is obtained using the _turbulenceProperties_ function. 

If one wishes not to include the SGS contribution, delete it from the code. 

The terms EpiK, PVTK, and Tk can be averaged using the attached tkeBudgetsAverage utility.

This code can be implemented directly in your case file. Simply, add both files to the system folder and in the controlDict file, add the following inside functions,

  #include "tkeBudgets"

  #include "tkeBudgetsAverage"

