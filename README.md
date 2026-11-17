# HIVE-COTE 2.0: a new meta ensemble for time series classification

Results for the paper "HIVE-COTE 2.0: a new meta ensemble for time series
classification" published in Machine Learning, which introduces the HIVE-COTE 2.0
(HC2) ensemble of four classifiers: the Temporal Dictionary Ensemble (TDE), the Diverse
Representation Canonical Interval Forest (DrCIF), the Arsenal and the Shapelet
Transform Classifier (STC). HC2 is compared to the state of the art on 112 univariate
UCR datasets and 26 multivariate UEA datasets.

The paper is available from
[Springer](https://doi.org/10.1007/s10994-021-06057-9).

## Contents

| Path | Description |
|---|---|
| [results/univariate/SOTA-AverageOver30.csv](results/univariate/SOTA-AverageOver30.csv) | Test accuracy of HC2 and eight other classifiers on 112 UCR datasets, averaged over 30 resamples (Figures 5 and 8) |
| [results/univariate/SOTA-DefaultTrainTest.csv](results/univariate/SOTA-DefaultTrainTest.csv) | As above, on the default train/test split |
| [results/univariate/AllClassifiers](results/univariate/AllClassifiers) | Test accuracy on each resample for 17 classifiers, including the dictionary (Figure 3) and interval (Figure 4) based comparisons |
| [results/univariate/AblativeStudy](results/univariate/AblativeStudy) | Test accuracy of the HC2 variants in Table 7 (Figure 16) |
| [results/univariate/EnsemblingCompare](results/univariate/EnsemblingCompare) | Test accuracy of alternative ensembling schemes for HC2 (Figure 17) |
| [results/multivariate/MTSC-SOTA-AverageOver30.csv](results/multivariate/MTSC-SOTA-AverageOver30.csv) | Test accuracy of HC2 and eight other classifiers on 26 UEA datasets, averaged over 30 resamples (Figures 10 and 13) |
| [results/multivariate/MTSC-SOTA-DefaultTrainTest.csv](results/multivariate/MTSC-SOTA-DefaultTrainTest.csv) | As above, on the default train/test split |
| [results/multivariate/AllClassifiers](results/multivariate/AllClassifiers) | Test accuracy on each resample for nine classifiers |
| [hivecote2.ipynb](hivecote2.ipynb) | Example of using HC2 from `aeon` |

The `SOTA` files have one row per dataset and one column per classifier. The
`_TESTFOLDS.csv` files have one row per dataset and one column per resample, with 30
resamples in total. Resample 0 is the default train/test split. In the ensembling
comparison, `HC2_RandfProbs` is the random forest stacking scheme shown in Figure 17.

The test predictions of every classifier on every resample, which also give the other
performance measures in the paper, are available from timeseriesclassification.com:

- [Univariate predictions](https://www.timeseriesclassification.com/results/HC2/FullUnivariateResults.zip)
  (1.7 GB)
- [Multivariate predictions](https://www.timeseriesclassification.com/results/HC2/FullMultivariateResults.zip)
  (263 MB)

## Datasets

The 112 equal length univariate datasets without missing values are from the
[UCR Time Series Classification Archive 2018](https://doi.org/10.5281/zenodo.11198697),
and the 26 multivariate datasets are from the
[UEA Multivariate Time Series Classification Archive](https://www.timeseriesclassification.com/dataset.php).
More information on the datasets is available at
[timeseriesclassification.com](http://www.timeseriesclassification.com).

## Running HC2

### aeon

HC2 and its components are available in the
[aeon](https://github.com/aeon-toolkit/aeon) Python package as `HIVECOTEV2`,
`TemporalDictionaryEnsemble`, `DrCIFClassifier`, `Arsenal` and
`ShapeletTransformClassifier`. They follow the `scikit-learn` interface:

    pip install -r requirements.txt

See [hivecote2.ipynb](hivecote2.ipynb) for an example, which can be run online using
Binder:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/time-series-machine-learning/hivecote2-2021/main?filepath=hivecote2.ipynb)

The example was last checked in November 2026 with `aeon` 1.5.0 on Python 3.12.

### As published

The paper used the Java implementation in the
[tsml](https://github.com/time-series-machine-learning/tsml-java) toolkit. The version
used at the time of publication is the
[`paper/HC2` branch](https://github.com/time-series-machine-learning/tsml-java/tree/paper/HC2).
The branch is a Gradle project for Java 8 with `experiments.Experiments` as its main
class, which runs HC2 with the classifier name `HIVE-COTEv2`:

    ./gradlew run --args="-dp=data/ -rp=results/ -dn=GunPoint -cn=HIVE-COTEv2 -f=1 -nt=2 -s=0"

where `-dp` and `-rp` are the data and results directories, `-dn` is the dataset name,
`-f` is the fold (starting at 1 for the default train/test split), `-nt` is the number
of threads and `-s` is the random seed. The arguments are described in the
`ExperimentalArguments` class in `Experiments.java`. The dataset files must be in
`data/<dataset>/<dataset>_TRAIN.ts` and `data/<dataset>/<dataset>_TEST.ts` (or `.arff`).
tsml uses nd4j for the Arsenal, so set the `OMP_NUM_THREADS` environment variable to the
same number of threads.

## Citation

If you use this work, please cite the paper:

```bibtex
@article{middlehurst2021hive,
  title={{HIVE-COTE} 2.0: a new meta ensemble for time series classification},
  author={Middlehurst, Matthew and Large, James and Flynn, Michael and Lines, Jason and Bostrom, Aaron and Bagnall, Anthony},
  journal={Machine Learning},
  volume={110},
  number={11},
  pages={3211--3243},
  year={2021},
  publisher={Springer},
  doi={10.1007/s10994-021-06057-9}
}
```

## Contact

For questions about the paper or this repository, feel free to contact any of the
authors. Matthew Middlehurst can be reached at
[m.b.middlehurst@bradford.ac.uk](mailto:m.b.middlehurst@bradford.ac.uk) or on the
[aeon Discord](https://discord.gg/D6rzqHGKRJ) (`matthewmiddlehurst`).
