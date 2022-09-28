<p align="center">
  <img width="900" src="https://raw.githubusercontent.com/farakiko/xai4hep/dev/docs/_static/images/mlpf_rscores.png" />
</p>

# xai4hep

XAI toolbox for interpreting state-of-the-art ML algorithms for high energy physics.

xai4hep provides necessary implementations of explainable AI (XAI) techniques for state-of-the-art graph neural networks (GNNs) developed for various tasks at the LHC-CERN. Models include: machine-learned particle flow (MLPF), the interaction network (IN), and ParticleNet. Currently, the layerwise-relevance propagation (LRP) technique is implemented for such models, and additional XAI techniques are under development.


## Setup
Have conda installed.
```bash
conda env create -f environment.yml
conda activate xai
```

## Quickstart

Running standard LRP for a simple fully connected network (FCN) on a toy dataset with a highly discriminatory feature:
```bash
python run_lrp_fcn.py
```

Running modified LRP for a trained MLPF model:
```bash
python run_lrp_mlpf.py --run_lrp --make_rmaps --load_model=$model_dir --load_epoch=$epoch --outpath=$path_to_model --loader=$dataloader
```

Running modified LRP for a trained ParticleNet model:
```bash
python run_lrp_particlenet.py --outpath=$path_to_model --model_prefix=$model_name --dataset=$path_to_dataset
```

## ParticleNet training and LRP testing

Get and process the dataset:
```bash
cd particlenet/
./get_data.sh
```
This will automatically create a `data` folder in the repository, with a `toptagging` folder that contains `train`,`val`,`test` folders.

Run a quick training:
```bash
mkdir experiments/
python run_particlenet_training.py --quick --model_prefix=ParticleNet_model
```
This will run a quick training over a small sample of the dataset and store the model under `experiments`.

Run a quick LRP test:
```bash
python run_lrp_particlenet.py --quick --model_prefix=ParticleNet_model
```
