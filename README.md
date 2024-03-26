# Koopman Operator Implicit Neural Representation

As always, research is built from the shoulders of giants. My sincerest thanks to [Yuan Yin](https://yuan-yin.github.io/), [Matthieu Kirchmeyer](https://mkirchmeyer.github.io/), [Jean-Yves Franceschi](https://jyfranceschi.fr), [Alain Rakotomamonjy](http://asi.insa-rouen.fr/enseignants/~arakoto/), and [Patrick Gallinari](http://www-connex.lip6.fr/~gallinar/gallinari/pmwiki.php) for allowing me to use their amazing work, [DINo](https://github.com/mkirchmeyer/DINo), as a foundation for my research.

The `requirements.txt` file lists Python package dependencies.

## Data 

* For `navier_stokes`, `wave`, data is generated as part of the script c.f. `data_pdes.py`.


## Training

```
python3 train.py -d <DATASET> -g 0 -r <RATE>
```

* `-c`: checkpoint location for warm-start with a pretrained model (default: no warmstart)
* `-d`: input dataset (`navier_stokes`, `wave`)
* `-f`: home path (defaults to `"./results"`)
* `-g`: gpu id (defaults to `0`)
* `-r`: subsampling rate (defaults to `1.0`)

By running the train script, it will generate an unique id of each run, called the run_id.

Logs are available in `./results/<RUN_ID>/log` and display the result over In/Out-s + In/Out-t for both train and test trajectories 
(cf the Figure below where red represents observed data and our paper for more details). 

![task](https://user-images.githubusercontent.com/15007187/215505653-843c1b0e-f7e1-41ce-819b-a16aec1d09d5.png)

## Inference on new conditions

The run_id can also be used to run the inference script on test trajectories for the following settings:
* Evaluation on a new grid for `navier_stokes`, `wave` (Table 3.a).

```
python3 test.py -d <DATASET> -p <RUN_ID> -g 0 -r <RATE> -s <SEED>
```

* `-d`: input dataset (`navier_stokes`, `wave`, `shallow_water_hr`)
* `-f`: home path (defaults to `"./results"`)
* `-g`: gpu id (defaults to `0`)
* `-p`: run id
* `-r`: subsampling rate (defaults to `1.0`)
* `-s`: subsampling seed (defaults to `1` the train subsampling seed; for Table 3.a. we chose `-s 2`)


## Citation

```
@inproceedings{Yin2023,
title={Continuous PDE Dynamics Forecasting with Implicit Neural Representations},
author={Yin, Yuan and Kirchmeyer, Matthieu and Franceschi, Jean-Yves and Rakotomamonjy, Alain and Gallinari, Patrick},
booktitle={International Conference on Learning Representations},
year={2023},
url={https://openreview.net/forum?id=B73niNjbPs}
}
```
