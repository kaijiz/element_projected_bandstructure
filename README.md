# element_projected_bandstructure
a code to draw bandstructure based on VASP output with colors representing the contribution of specific element. 
To use this code, you need to change the source code of Pymatgen, becasue one function in Pymatgen we use will skip the duplicate Kpoints (always the Gamma Point) but another function won't skip the Kpoint which will casue errors. It really easy to change the code.
First, find the location of your source code. (/opt/anaconda3/envs/chgnet/lib/python3.11/site-packages/pymatgen/io/vasp/outputs.py) or (/scratch/user/kaijiz/.conda/envs/pydefect/lib/python3.11/site-packages/pymatgen/io/vasp//outputs.py).
search "skipping_kpoint", you will find a place:  

else:  # skip ahead to next kpoint:

                        skipping_kpoint = True'
                        
                        continue.
                
Change this to :

else:  # skip ahead to next kpoint:

                        skipping_kpoint = False
                        
                        if spin == Spin.up:
                        
                            kpoints.append(kvec)  # only add once
                            
                        continue

Then, save and exit and you can use this code.


### the name of the kpoints and element you need to set by yourself.
