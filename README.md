# KoIN: Koopman Operator Implicit Neural Representation

Code outlining and detailing the model featured in my thesis work, Learning Linear Evolution of Partial Differential Equations Through Koopman-Inspired Implicit Neural Representation.  A neural implicit representation framework is employed to reduce spatial complexity into latent representation where the dynamics is governed by a ***linear system***. This framework can be viewed as learning a Koopman operator of the nonlinear systems governed by partial differential equations in a ***mesh-agnostic*** way. Moreover, I leverage auto-encoding to avoid explicit encoding such that full state measurement is avoided. The effectiveness of this framework is validated on several canonical PDE data-sets with a diverse set of initial conditions ranging from 2D wave to incompressible Navier-Stokes equations.



## Data 
The `requirements.txt` file lists Python package dependencies.

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

## Special Thanks
As always, research is built from the shoulders of giants. My sincerest thanks to [Yuan Yin](https://yuan-yin.github.io/), [Matthieu Kirchmeyer](https://mkirchmeyer.github.io/), [Jean-Yves Franceschi](https://jyfranceschi.fr), [Alain Rakotomamonjy](http://asi.insa-rouen.fr/enseignants/~arakoto/), and [Patrick Gallinari](http://www-connex.lip6.fr/~gallinar/gallinari/pmwiki.php) for allowing me to use their amazing work, [DINo](https://github.com/mkirchmeyer/DINo), as a foundation for my research.
```
@inproceedings{Yin2023,
title={Continuous PDE Dynamics Forecasting with Implicit Neural Representations},
author={Yin, Yuan and Kirchmeyer, Matthieu and Franceschi, Jean-Yves and Rakotomamonjy, Alain and Gallinari, Patrick},
booktitle={International Conference on Learning Representations},
year={2023},
url={https://openreview.net/forum?id=B73niNjbPs}
}
```
