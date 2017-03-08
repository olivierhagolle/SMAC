SMAC
----
# Description

The Simplified Model for Atmospheric Correction (SMAC) is the perfect model to perform easy, quick and not too dirty atmospheric corrections. It is based on very simple analytic formulas, based on the 5S model. The 49 coefficients of this model are fitted using a large number of radiative transfer simulations with the 6S model (the old historic version, not the recent vector version). This software is not very accurate (much less than MACCS), and it requires in-situ measurements for the aerosol optical thickness, and weather analyses for ozone and water vapour. If these data are available,  in most cases, its accuracy is within 2 and 3 percent, if we do not account for adjacency effects and slope effects, and it may be worse for large viewing and solar angles (above 70°) or within strong absorption bands.

# Usage

The "main"  routine of [smac.py](http://tully.ups-tlse.fr/olivier/smac-python/blob/master/smac.py) provides an example of how to use SMAC.

`
   
    #read the 49 coefficients in smac_soefs table
    nom_smac ='COEFS/coef_FORMOSAT2_B1_CONT.dat'
    coefs=coeff(nom_smac)
 
    #read the TOA reflectance image in r_toa variable
    #depends on the file format
 
    #read the angle values in the image metadata
    theta_s=30 #solar zenith angle
    phi_s=180  #solar azimuth angle
    theta_v=0  #viewing zenith angle
    phi_v=0    #viewing azimuth
    
    # compute pressure at pixel altitude (in m)
    pressure=PdeZ(1300)
 
    #find the values of AOT, UO3, UH2O
    AOT550=0.1 # AOT at 550 nm
    UO3=0.3    # Ozone content (cm)  0.3 cm= 300 Dobson Units
    UH2O=3     # Water vapour (g/cm2)
 
    #compute the atmospheric correction
    r_surf=smac_inv(r_toa,theta_s,phi_s,theta_v,phi_v,pressure,AOT,UO3,UH2O,coefs)
`



# Coefficients

The SMAC coefficients, computed for a  large number of satellites are available  here : http://tully.ups-tlse.fr/olivier/smac-python/tree/master

# Credits

The SMAC model was developed by Rahman et Dedieu in 1994. The present version comes from  further works from Berthelot et Dedieu, which were not published. The code to compute coefficients was industrialised  by Beatrice Berthelot, under CNES funding. The available coefficients were computed by Béatrice Berthelot, François Cabot, Olivier Hagolle, Sophie Lacherade, Sebastien Marcq ou Manuel Grizonnet.

The python routine is a translation of François Cabot's Matlab version of SMAC. 

# Reference

Rahman, H., & Dedieu, G. (1994). SMAC: a simplified method for the atmospheric correction of satellite measurements in the solar spectrum. REMOTE SENSING, 15(1), 123-143.
