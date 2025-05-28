# Workflow

## First step: benchmark aggregation
The first notebooks to run are the following two:

- benchmark_aggregation.ipynb
- benchmark_aggregation_validation_matrices.ipynb

Each notebook aggregates results in two files, one containing all benchmarks (all different formats) and one containing only the best performing format for each matrix. As an example, the synthetic matrices final csv files will be:

- synthetic_benchmarks_all-devices_all.csv
- synthetic_benchmarks_all-devices_best-of.csv

Another pair of "all" and "best-of" CSVs will be generated for the validation (real) matrices, as well as for the synthetic matrices that are "friends" of validation (synthetic matrices with similar features to the real ones, used for validation of synthetic matrices methodology).

These csv files will be stored in this directory.

## Second step: synthetic and validation notebooks

These are the main notebooks, used for plot production and analysis of the results.

They first read the "all" and "best-of" CSV files that contain the aggregated results from the first step. The important features of these dataframes are the following:

- matrix_name: useful for real matrices; for artificial matrices, it is always "synthetic"
- nr_rows, nr_cols, nr_nzeros: the dimensions of the sparse matrix
- mem_footprint: memory footprint of sparse matrix in CSR format (in MBs)
- avg_nnz_per_row, std_nnz_per_row: average and standard deviation of row size (how many nonzeros there are per row)
- avg_bw_scaled, std_bw_scaled: average and standard deviation of bandwidth (distance between first and last nonzero in a row), scaled by the number of columns
- skew: imbalance of row length (max_nnz_per_row - avg_nnz_per_row)/avg_nnz_per_row
- avg_num_neighbours, cross_row_similarity: a metric that measures distance between neighboring nonzero elements (intra-row and inter-row respectively)
- format_name: name of the SpMV format tested
- gflops: performance of SpMV in GFLOP/s 
- System: name of the device
- Arch: CPU or GPU
