## Installation 
### Host
```
# create environment
conda create -n ldm python=3.10
# https://pytorch.org/get-started/previous-versions/ 
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 numpy==1.26.3 -c pytorch -c nvidia
pip install -r requirements.xtx

# compress environment 
conda-pack -n ldm -o ldm.tar.gz

# compress all code and environment
cd .. & zip -r latent-diffusion.zip latent-diffusion
```

## Bigdata
```
# decompress
unzip latent-diffusion.zip && rm latent-diffusion.zip
cd latent-diffusion 
mkdir env && tar -xvf ldm.tar.gz -C env && rm ldm.tar.gz

# install clip and taming-transformers
cd src/CLIP && python setup.py develop 
cd src/taming-transformers && python setup.py develop

# set torch hub directory
export TORCH_HOME=./torch_home
```

## Train
### Autoencoder
```
python main.py --base configs/autoencoder/autoencoder_kl_64x64x3.yaml -t --gpus [gpus]
```
