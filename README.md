# HG-means

Source code of HG-means clustering, an efficient hybrid genetic algorithm proposed for minimum sum-of-squares clustering (MSSC). This population-based metaheuristic uses K-means as a local search in combination with crossover, mutation, and diversification operators. As HG-means algorithm uses K-means, we included the fundamental source files of the fast K-means implementation of Greg Hamerly (to whom we are grateful to make available the source code) in this repository.

Original files and complete source code of Greg Hamerly K-means can be found at: https://github.com/ghamerly/fast-kmeans

## Related Article

*HG-means: A scalable hybrid genetic algorithm for minimum sum-of-squares clustering*. D. Gribel and T. Vidal. Pattern Recognition, https://doi.org/10.1016/j.patcog.2018.12.022

https://authors.elsevier.com/c/1YIIy77nKSc2q

## Run

Firstly, make sure that the dataset is placed in `/data` folder.

To run the algorithm, try the following sequence of commands:

`> make`

`> ./hgmeans "Dataset_Path" Pi_min N2 Evaluate [M]`

### Example

`> make`

`> ./hgmeans "data/iris.txt" 10 5000 0 2 5 10`

This script executes HG-means algorithm for "iris" dataset, with 10 solutions in population, a maximum of 5000 iterations, no external evaluation; and 2, 5 and 10 clusters.

After the execution of the algorithm, output files will be saved in `/out` folder.

### Parameters of the algorithm

`Dataset_Path`: The path of dataset. Datasets should be placed in `/data` folder.

`Pi_min` (default=10): Population size. Determines the size of the population in the genetic algorithm.

`N2` (default=5000): Maximum number of iterations. Determines the total number of iterations the algorithm will take.

`Evaluate` (default=0): External clustering evaluation. Boolean parameter {0,1} for calculating external clustering measures. **Important:** If this parameter is set to 1, make sure that the ground-truth file is provided in `/labels` folder with the same name of the dataset.

`[M]`: The list of number of clusters m (1 <= m <= n). You can pass multiple values for m, separated by a single space.

## Data format

**Dataset files.** In the first line of a dataset file, the number of data points (n) and the dimensionality of the data (d) is set, separated by a single space. The remaining lines correspond to the coordinates of data points. Each line contains the values of the d features of a sample, where x_ij correspond to the j-th feature of the i-th sample of the data. Each feature value is separated by a single space, as depicted in the scheme below:

|  n   |   d  |      |     |      |
|------|------|------|-----|------|
| x_11 | x_12 | x_13 | ... | x_1d |
| x_21 | x_22 | x_23 | ... | x_2d |
| .... | .... | .... | ... | .... |
| x_n1 | x_n2 | x_n3 | ... | x_nd |

Some datasets are provided in `/data` folder.

**Labels files.** The content of a labels file exhibits the cluster of each sample of the dataset according to ground-truth, where y_i correspond to the label of the i-th sample:

y_1

y_2

...

y_n

For some datasets, labels are provided in `/labels` folder.

## Output file

After the execution of the algorithm, output files are saved in `/out` folder, with the following header:

| Pi_min | N2 | Dataset | m | SolutionCost | Time(s) |

If external clustering evaluation is done, the following header is produced:

| Pi_min | N2 | Dataset | m | SolutionCost | Time(s) | C-Rand | NMI | CentroidIndex