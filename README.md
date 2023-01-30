# Continuous PDE Dynamics Forecasting with Implicit Neural Representations

Official PyTorch implementation of DINo (Dynamics-aware Implicit Neural Representation) | [Accepted at ICLR 2023 (Notable-Top-25%, Spotlight)](https://openreview.net/forum?id=B73niNjbPs) | [Arxiv](https://arxiv.org/abs/2209.14855) 

[Yuan Yin](https://yuan-yin.github.io/) (equal contribution), [Matthieu Kirchmeyer](https://mkirchmeyer.github.io/) (equal contribution), [Jean-Yves Franceschi](https://jyfranceschi.fr) (equal contribution), [Alain Rakotomamonjy](http://asi.insa-rouen.fr/enseignants/~arakoto/), [Patrick Gallinari](http://www-connex.lip6.fr/~gallinar/gallinari/pmwiki.php)

https://user-images.githubusercontent.com/15007187/194546732-dafb7627-4be3-4e8e-910a-9b08ad375158.mp4

https://user-images.githubusercontent.com/15007187/194546967-557280ff-bde0-4bb4-9650-c9ec1f7bf986.mp4

The `requirements.txt` file lists Python package dependencies.

## Data 

* For `navier_stokes`, `wave`, data is generated as part of our script c.f. `data_pdes.py`.
* For `shallow_water`, data can be found [here](https://doi.org/10.6084/m9.figshare.21298179).
It should be stored in `./results/shallow_water` or in a custom location given as argument to `-f`.

## Pretrained models

We provide the checkpoints [here](https://doi.org/10.6084/m9.figshare.21298251) 
* `NS_100` for `navier_stokes` (100% subsampling rate)
* `Wave_100` for `wave` (100% subsampling rate)
* `SW` for `shallow_water` (c.f. our paper)

They should be stored in `./results/<DATASET>` and can be used for:
* warm start via `train.py`; the path of the model should be given as argument via `-c`. 
* inference via `test.py`.

We do not control the behavior of the checkpoints on other datasets than those generated by our code.

## Training

```
python3 train.py -d <DATASET> -g 0 -r <RATE>
```

* `-c`: checkpoint location for warm-start with a pretrained model (default: no warmstart)
* `-d`: input dataset (`navier_stokes`, `wave`, `shallow_water`)
* `-f`: home path (defaults to `"./results"`)
* `-g`: gpu id (defaults to `0`)
* `-r`: subsampling rate (defaults to `1.0`)

By running the train script, it will generate an unique id of each run, called the run_id.

Logs are available in `./results/<RUN_ID>/log` and display the result over In/Out-s + In/Out-t for both train and test trajectories (cf the Figure below where red represents observed data and our paper for more details). 
These are the numbers reported in Table 2.

![task](https://user-images.githubusercontent.com/15007187/215505653-843c1b0e-f7e1-41ce-819b-a16aec1d09d5.png)

## Inference on new conditions

The run_id can also be used to run the inference script on test trajectories for the following settings:
* Evaluation on a new grid for `navier_stokes`, `wave` (Table 3.a).
* Super-resolution for `shallow_water` (Figure 5).

```
python3 test.py -d <DATASET> -p <RUN_ID> -g 0 -r <RATE> -s <SEED>
```

* `-d`: input dataset (`navier_stokes`, `wave`, `shallow_water_hr`)
* `-f`: home path (defaults to `"./results"`)
* `-g`: gpu id (defaults to `0`)
* `-p`: run id
* `-r`: subsampling rate (defaults to `1.0`)
* `-s`: subsampling seed (defaults to `1` the train subsampling seed; for Table 3.a. we chose `-s 2`)

https://user-images.githubusercontent.com/15007187/194547306-e0f151cf-a4fc-43be-a907-35816124020d.mp4

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
