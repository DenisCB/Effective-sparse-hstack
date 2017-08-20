# Effective sparse horizontal stacking
This repository contains function for stacking sparse and sparse or sparse and dense matrices horizontally (column wise) with resulting matrix in CSR format. In notebook you’ll find function itself, examples of it’s use and performance tests that compare stacking time on data of different sizes and formats for present function and default scipy.sparse.hstack.

# Overview
Whenever you build features for machine learning model, you might end with sparse and dense features. In this case you’ll have to stack them horizontally and convert into compressed sparse rows (CSR) format, since compressed sparse rows (CSC) and compressed coordinate (COO) formats do not support row-wise slicing. Unfortunately, stacking sparse matrices horizontally works best with CSC matrices, and if applied to CSR matrices it’s non-linear complexity could be prohibitively expensive. 

One way to overcome this limitation is to apply horizontal stacking on small batches of data, producing a number of small CSR matrices, that then will be stacked vertically into a single large matrix. Complexity of vertical stacking of CSR matrices is negligible. 

# Performance 
Method was first tested during Quora competition on Kaggle, where I had to stack horizontally dense matrix of (2KK x 300) and CSR matrix of (2KK x 60K). Scipy sparse hstacking was crashing after 70-90 minutes of computations. Batched function given in this repository successfully completed the same task within 10 minutes. 

On datasets of significant sizes batched version of hstacking completes stacking 3-5 times faster than scipy default version. However, on the small datasets timing is almost identical. Refer to notebook for exact details.
