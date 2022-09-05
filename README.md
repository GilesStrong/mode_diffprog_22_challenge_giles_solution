[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7050685.svg)](https://doi.org/10.5281/zenodo.7050685)

# MODE '22 workshop data challenge - Giles Solution

My solution to: https://github.com/GilesStrong/mode_diffprog_22_challenge

Final score: private IOU = 0.824

See included PDF for details.

## Notebooks

The notebooks contain all the specific code for the problem, and all the data processing starting from the original challenge data.

- 0_unet-pixelshuffle_depth-encode_data-aug_se-net_f8r2_full.ipynb
  - A pure UNet model with a score of ~0.812
- 1_unet-pixelshuffle_depth-encode_data-aug_gravnet_osa_f32_full.ipynb
  - Extends the model to replace the centre of the UNet with a GravNet based network, IOU ~= 0.818
- 2_unet-pixelshuffle_depth-encode_data-aug_gravnet_osa_f32_full-long_ensemble5.ipynb
  - Trains an ensemble of 5 models over 100 epochs each, IOU ~= 0.821
- 3_unet-pixelshuffle_depth-encode_data-aug_gravnet_osa_f64_full-long_studentval_ensemble5-GPU1.ipynb
  - Uses pseudo-labels for the test data, generated by the predictions of the previous ensemble, and trains an ensemble of 10 models over 200 epochs.
  - IOU ~= 0.822
  - The notebook by default trains 5 models, and so either needs to be either copied two train models over 2 GPUs in parallel, or set to train 10 models sequntially

## Setup

For GPU usage, I'd recommend installing PyTorch yourself, based on driver versions, etc. See https://pytorch.org/get-started/locally/ for pip and conda commands.

The solutions rely on the [LUMIN](https://lumin.readthedocs.io/en/stable/) front-end to PyTorch.
Due to various bug-fixes and changes, these solutions require the current bleeding-edge version.
For now (close to 2022/0905), install from source with:

```bash
git clone git@github.com:GilesStrong/lumin.git
cd lumin
pip install .
```

But hopefully later, this will be enough:

```bash
pip install lumin==0.8.1
```

if that doesn't work, try:

```bash
pip install lumin==0.9.0
```

Additionally, you'll need:

```bash
pip install sparse
```

Any problems, open an issue.

