# HSAGN_with_SLE
This is an implementation of simple combination of [SAGN+SLE](https://github.com/skepsun/SAGN_with_SLE) and [NARS](https://github.com/facebookresearch/NARS).

## Requirements
```
ogb=1.3.1
pytorch=1.8.1
dgl=latest
```
For training transE embedding and preprocessing oag dataset, create a new conda environment with `dgl=0.4.3` and `dglke`.

## Methods
We simply adapt relation-subsets sampling method from NARS.
`hsagn` is a naive heterogeneous version of SAGN.
`nars_sagn` replaces SIGN component with SAGN in NARS.
`nars_sign` is exactly origin NARS.

## Preprocessing
You can generate all neccessary pretrained embeddings using scripts from [NARS](https://github.com/facebookresearch/NARS). 

For example, suppose that we want to train models on MAG. 

Firstly we train transE following instructions in NARS/graph_embed.  

Then we can train our model with `main.py`.
Randomly generating relations subsets is included in `main.py`. 


By setting argument `fixed-subsets` we can directly use the example subsets from [NARS/sample_relation_subsets/examples](https://github.com/facebookresearch/NARS/tree/main/sample_relation_subsets).

## Arguments
These arguments should be modified:

`root`: The root directory for ogb datasets.

`embedding-path`: The directory of TransE embedding.

`example-subsets-path`: The directory of example relations subsets (only used when `fixed-subsets` is True).

## Results
We provide example scripts for experiments on ACM, MAG, OAG_venue and OAG_L1. For now, these experiments have not been fully conducted.
To reproduce best results on MAG, run script `mag_sagn_use_labels_fixed.sh`.
|Relation size|Model|Dataset|Test acc|Val acc|
|----|----|----|----|----|
|fixed 8|NARS_SAGN+SLE-0|MAG|0.5232±0.0025|0.5412±0.0015|
|fixed 8|NARS_SAGN+SLE-1|MAG|0.5395±0.0014|0.5552±0.0016|
|fixed 8|NARS_SAGN+SLE-2|MAG|**0.5440±0.0015**|0.5591±0.0017|
|8|NARS_SIGN+SE-0|MAG|0.5173±0.0032|0.5323±0.0050|
|8|NARS_SIGN+SE-1|MAG|0.5230±0.0067|0.5319±0.0076|
|8|NARS_SIGN+SE-2|MAG|0.5218±0.0087|0.5312±0.0088|
|8|NARS_SAGN+SE-0|MAG|0.5052±0.0033|0.5205±0.0037|
|8|NARS_SAGN+SE-1|MAG|0.5204±0.0040|0.5311±0.0054|
|8|NARS_SAGN+SE-2|MAG|0.5224±0.0050|0.5327±0.0058|
|8|NARS_SIGN+SLE-0|MAG|0.5232±0.0024|0.5411±0.0032|
|8|NARS_SIGN+SLE-1|MAG|0.5347±0.0049|0.5508±0.0052|
|8|NARS_SIGN+SLE-2|MAG|0.5382±0.0051|0.5546±0.0046|
|8|NARS_SAGN+SLE-0|MAG|0.5207±0.0039|0.5400±0.0028|
|8|NARS_SAGN+SLE-1|MAG|0.5370±0.0038|0.5544±0.0037|
|8|NARS_SAGN+SLE-2|MAG|0.5408±0.0042|0.5577±0.0034|

|Relation size|Model|Dataset|Test acc|Val acc|
|----|----|----|----|----|
|2|NARS_SIGN+SE-0|ACM|0.9230±0.0062|0.9289±0.0106|
|2|NARS_SIGN+SE-1|ACM|0.9341±0.0031|0.9476±0.0090|
|2|NARS_SIGN+SE-2|ACM|0.9391±0.0050|0.9392±0.0136|
|2|NARS_SAGN+SE-0|ACM|0.9166±0.0054|0.9279±0.0092|
|2|NARS_SAGN+SE-1|ACM|0.9358±0.0062|0.9481±0.0098|
|2|NARS_SAGN+SE-2|ACM|**0.9415±0.0061**|0.9414±0.0144|
|2|NARS_SIGN+SLE-0|ACM|0.9216±0.0043|0.9279±0.0089|
|2|NARS_SIGN+SLE-1|ACM|0.9324±0.0062|0.9439±0.0060|
|2|NARS_SIGN+SLE-2|ACM|0.9387±0.0040|0.9392±0.0152|
|2|NARS_SAGN+SLE-0|ACM|0.9173±0.0044|0.9279±0.0078|
|2|NARS_SAGN+SLE-1|ACM|0.9324±0.0051|0.9471±0.0096|
|2|NARS_SAGN+SLE-2|ACM|0.9394±0.0090|0.9419±0.0135|

|Relation size|Model|Dataset|Test MRR|Val MRR|Test NDCG| Val NDCG|
|----|----|----|----|----|----|----|
|8|NARS_SIGN+SE-0|OAG_venue|0.3612±0.0052|0.4293±0.0046|0.5380±0.0047|0.6051±0.0039|
|8|NARS_SIGN+SE-1|OAG_venue|0.3736±0.0053|0.4362±0.0040|0.5499±0.0046|0.6107±0.0034|
|8|NARS_SIGN+SE-2|OAG_venue|0.3745±0.0050|0.4358±0.0041|0.5498±0.0042|0.6093±0.0032|
|8|NARS_SAGN+SE-0|OAG_venue|-|-|-|-|
|8|NARS_SAGN+SE-1|OAG_venue|-|-|-|-|
|8|NARS_SAGN+SE-2|OAG_venue|-|-|-|-|
|8|NARS_SIGN+SLE-0|OAG_venue|-|-|-|-|
|8|NARS_SIGN+SLE-1|OAG_venue|-|-|-|-|
|8|NARS_SIGN+SLE-2|OAG_venue|-|-|-|-|
|8|NARS_SAGN+SLE-0|OAG_venue|-|-|-|-|
|8|NARS_SAGN+SLE-1|OAG_venue|-|-|-|-|
|8|NARS_SAGN+SLE-2|OAG_venue|-|-|-|-|