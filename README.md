## Installation

We recommend using python 3.8 or newer. Install all requirements in a virtual environment with:
``` bash
python -m venv env
source env/bin/activate
cd apg_drone_control
pip install -e .
```

### Training

To train a controller for the MSP, we first need to create random polynomial trajectories as train and test data. Run:
``` bash
python scripts/generate_trajectories.py
```

Then, you can start training:
``` bash
python scripts/train_drone.py
```

Similarly, the cartpole or fixed wing drone can be trained (without generating any trajectories) with:
``` bash
python scripts/train_fixed_wing.py
python scripts/train_cartpole.py
```


### Evaluation

The trained models can be evaluated in a similar fashion, by running either of these commands:
``` bash
python scripts/evaluate_drone.py -a 50
python scripts/evaluate_fixed_wing.py -a 50
python scripts/evaluate_cartpole.py -a 50
```

Notes:
* The flag `-a` determines the number of iterations.
* With the animate-flag an animation is shown (`python scripts/evaluate_drone.py --animate` and analogous for fixed wing and cartpole).

**Baseline comparison:**

1) MPC: 
The MPC baseline is integrated in the evaluate-scripts. Simply specify mpc with the model flag, e.g. `python scripts/evaluate_drone.py -m mpc -a 50`.

2) PPO:
PPO models can be trained and evaluated with the script `baselines/ppo_baseline.py` (e.g. `python baselines/ppo_baseline.py -r fixed_wing -a 50`).

3) PETS:
PETS training is done with the [mbrl](https://github.com/facebookresearch/mbrl-lib) library provided by Facebook Research. Our code can be found in the script `baselines/pets_baseline.py`.

