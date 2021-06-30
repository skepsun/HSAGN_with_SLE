# HSAGN_with_SLE
This is an implementation of simple combination of [SAGN+SLE](https://github.com/skepsun/SAGN_with_SLE) and [NARS](https://github.com/facebookresearch/NARS).

## Methods
We simply adapt relation-subsets sampling method from NARS.
`hsagn` is a naive heterogeneous version of SAGN.
`nars_sagn` replaces SIGN component with SAGN in NARS.
`nars_sign` is exactly original NARS.

## Results
We provide example scripts for experiments on ACM, MAG, OAG_venue and OAG_L1. For now, these experiments have not been fully conducted.
We can offer a fast MAG result with using example subsets from NARS:
|Model|Dataset|Metrics|
|----|----|----|
|NARS_SAGN+SLE-2|MAG|0.5440±0.0015|

To reproduce this result, run script `mag_sagn_use_labels_fixed.sh`.