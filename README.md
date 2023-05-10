# Bias on Demand

Biasondemand is a Python package that generates synthetic datasets with different types of bias. This package is based on the research paper "[Bias on Demand: A Modelling Framework That Generates Synthetic Data With Bias](https://doi.org/10.1145/3593013.3594058)" published at the ACM Conference on Fairness, Accountability, and Transparency (ACM FAccT) 2023.

## Authors & Contributors

Joachim Baumann, Alessandro Castelnovo, Riccardo Crupi, Nicole Inverardi, Daniele Regoli

## Installation

To use biasondemand, run:

```
pip install biasondemand
```

## Usage

### Generating Synthetic Datasets

To generate a synthetic dataset with no bias, use the following python script:
```
import biasondemand
biasondemand.generate_dataset(path='my_unbiased_dataset', dim=1000)
```

Alternatively, you can also run it directly from the command line using the following command:
```
bias_on_demand_generate_dataset -p my_unbiased_dataset -dim 1000
```

This will generate a dataset with 1000 rows and save it in the directory `datasets/my_unbiased_dataset/`.

You can introduce different types of bias into the dataset by specifying command line arguments. For example, to generate a dataset with measurement bias on the label Y (magnitude: 1.5) and historical bias on the feature R (magnitude: 2), use the following command:
```
import biasondemand
biasondemand.generate_dataset(path='my_biased_dataset', dim=1000, l_m_y=1.5, l_h_r=2)
```

Or, again, if you prefer the command line, just use:
```
bias_on_demand_generate_dataset -p my_biased_dataset -dim 1000 -l_m_y 1.5 -l_h_r 2
```

This will generate a biased dataset with 1000 rows and save it in the directory `datasets/my_biased_dataset/`.

The following command line arguments are available to specify properties of the dataset:
- **dim**: Dimension of the dataset
- **sy**: Standard deviation of the noise of Y
- **l_q**: Lambda coefficient for importance of Q for Y
- **l_r_q**: Lambda coefficient that quantifies the influence from R to Q
- **thr_supp**: Threshold correlation for discarding features too much correlated with s

Furthermore, the following command line arguments are available to specify the types of biases to be introduced in the dataset:
- **l_y**: Lambda coefficient for historical bias on the target y
- **l_m_y**: Lambda coefficient for measurement bias on the target y
- **l_h_r**: Lambda coefficient for historical bias on R
- **l_h_q**: Lambda coefficient for historical bias on Q
- **l_m**: Lambda coefficient for measurement bias on the feature R. If l_m!=0 P substitutes R.
- **p_u**: Percentage of undersampling instance with A=1
- **l_r**: Boolean for inducing representation bias, that is undersampling conditioning on a variable, e.g. R
- **l_o**: Boolean variable for excluding an important variable (ommited variable bias), e.g. R (or its proxy)
- **l_y_b**: Lambda coefficient for interaction proxy bias, i.e., historical bias on the label y with lower values of y for individuals in group A=1 with high values for the feature R

Notice that the biases are introduced w.r.t. idividuals in the group A=1.
For most types of bias, larger values mean more bias. The only exceptions are undersampling and representation bias (which can be seen as a specific type of undersampling conditional on the feature R) where smaller values correspond to more (conditional) undersampling, i.e., more bias.

### Run experiments using biasondemand

In the repo [https://github.com/rcrupiISP/BiasOnDemand](https://github.com/rcrupiISP/BiasOnDemand) we provide the code and instructions to run a set of experiments for investigating bias, fairness, and mitigation techniques.
You can also check out [our paper](https://doi.org/10.1145/3593013.3594058) for more details on this topic.

### Python version

Biasondemand requires Python 3.7 or later.

## Citation

If you use biasondemand in your research, please cite our paper:

```
@inproceedings{baumann2023bias,
  title={Bias on Demand: A Modelling Framework That Generates Synthetic Data With Bias},
  author={Baumann, Joachim and Castelnovo, Alessandro and Crupi, Riccardo and Inverardi, Nicole and Regoli, Daniele},
  booktitle={Proceedings of the 2023 ACM Conference on Fairness, Accountability, and Transparency},
  doi={https://doi.org/10.1145/3593013.3594058},
  year={2023}
}
```
