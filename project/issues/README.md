# Issue Summary

1. Provide processor number not matching with compiled nPx x nPy. I changed my mind and changed the SIZE.h AFTER compiling the model.

2. Use 'conda init' before 'conda activate'
3. End of file error for exf files
4. Bad data for model boundaries south file

# MITgcm Message

1. I found the number of processor does not match nPx x nPy error in STDERR.0000.

2. I found this error in the slurm.out file

3. I found 'file exf_readparms.f (unit = 11, file = 'scratch1.000000007') Fortran runtime error: End of file' error in slurm.out file

4. 'At line 2694 of file obcs_readparms.f (unit = 11, file = 'scratch1.000000007') Fortran runtime error: Bad data for namelist object ob_jsouth' in
slurm.out file

# Issue Remedy

1. I changed the SIZE.h and recompile the model in build directory
2. I tried adding the conda init before the conda activate lines in the .slm file but the issue persist
3. I think the issue is in the data.exf file as I did not append the data.exf_append content to it. I copied all lines in data.exf_append to 
data.exf and rerun and it worked.
4. My notebook for creating model boundaries did not run properly, which caused bad data