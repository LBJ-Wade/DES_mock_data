DES 1YR mock data for MGCosmoMC
==================================

The code in this repo is used to produce the Dark Energy Survey (DES) 1 YR mock data  (in the format of [CosmoMC](https://github.com/cmbant/CosmoMC)) .

To use this code, you need to have the code [MGCosmoMC](https://github.com/sfu-cosmo/MGCosmoMC). 

## 1. Installing:
To install this code on your machine, type the following commands on the terminal
```bash
git clone https://github.com/alexzucca90/DES_linear_data
```

## 2. Running the code:
To create the DES mock dataset, first run MGCosmoMC using the  files provided in the folder [```mgcosmomc```](/mgcosmomc/). To do so, copy/paste (and replace if needed) the MGCosmoMC file with the one provided in this repo. Then recompile MGCosmoMC using 
```bash
make cosmomc
```
from your MGCosmoMC directory.
You can now run MGCosmoMC with the  [```DES_mock.ini```](/mgcosmomc/DES_mock.ini) initializing file. Type 
```bash
./cosmomc DES_mock.ini
```
MGCosmoMC will run a likelihood test and will return a set of output files. 

```bash
cd DES_linear_data
python DES_linear_cutoff.py -t threshold -c name_of_cutoff
```
where ```threshold``` is a float that defines the threshold to remove the data and ```name_cutoff``` is a string that names the cutoff.

## 3. Outputs:
The code produces a file ```./output/DES_1YR_final_name_of_cutoff_cut.dat``` that contains the used bins and the angular separation range for the correltaion function.

It also outputs a set of plots (in png and pdf formats) that can be used for visual inspection of the data cuts.


## 4. Examples:

### Standard cutoff
To generate the *standard* DES linear data cut (see our paper), run
```bash
python DES_linear_cutoff.py -t 5.0 -c standard
```
The code starts elimintaning the point that contributes the most to the Delta Chi^2, then recomputes the Delta Chi^2 and repeats the procedure. The improvement in the Delta Chi^2 is shown in the following plot
<p align="center">
<img src="img/chi2_improvement_standard.png" width="350" title="delta chi 2 improvement" />
</p>

and eliminates the data points in the shaded regions below

<p align="center">
<img src="img/m1standard.png" width="350" title="standard m 1" />
<img src="img/m2standard.png" width="350" title="standard m 2" />
</p>
<p align="center">
<img src="img/m3standard.png" width="350" title="standard m 3" />
<img src="img/m4standard.png" width="350" title="standard m 4" />
</p>

## 5. References:
Papers illustrating the method to remove the non-linear data:

*  *Dark Energy Survey Year 1 Results: Constraints on Extended Cosmological Models from Galaxy Clustering and Weak Lensing*   
    DES Collaboration  
    [arXiv:1810.02499 [astro-ph.CO]](https://arxiv.org/abs/1810.02499)
    
*   *Planck 2015 results. XIV. Dark energy and modified gravity*  
    Planck Collaboration   
    [arXiv:1502.01590 [astro-ph.CO]](https://arxiv.org/abs/1502.01590)
    


