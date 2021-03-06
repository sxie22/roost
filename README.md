# RooSt &nbsp; [![Tests](https://github.com/CompRhys/roost/workflows/Tests/badge.svg)](https://github.com/CompRhys/roost/actions)

**R**epresentati**o**n Learning fr**o**m **St**oichiometry

## Premise

In materials discovery applications often we know the composition of trial materials but have little knowledge about the structure.

Many current SOTA results within the field of machine learning for materials discovery are reliant on knowledge of the structure of the material. This means that such models can only be applied to systems that have undergone structural characterisation. As structural characterisation is a time-consuming process whether done experimentally or via the use of ab-initio methods the use of structures as our model inputs is a prohibitive bottleneck to many materials screening applications we would like to pursue.

One approach for avoiding the structure bottleneck is to develop models that learn from the stoichiometry alone. In this work, we show that via a novel recasting of how we view the stoichiometry of a material we can leverage a message-passing neural network to learn materials properties whilst remaining agnostic to the structure. The proposed model exhibits increased sample efficiency compared to more widely used descriptor-based approaches. This work draws inspiration from recent progress in using graph-based methods for the study of small molecules and crystalline materials.

## Environment Setup

To use `roost` you need to create an environment with the correct dependencies. Using `Anaconda` this can be accomplished with the follow commands:

```bash
conda create --name roost python=3.6
conda activate roost
pip install torch==1.5.0+${CUDA} -f https://download.pytorch.org/whl/torch_stable.html
pip install torch-scatter==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-1.5.0.html
pip install scikit-learn tqdm pandas tensorboard
```

`${CUDA}` Should be replaced by either `cpu`, `cu92`, `cu101` or `cu102` depending on your system CUDA version. (You can find your CUDA version via `nvidia-smi`)

You may encounter issues getting the correct installation of either `PyTorch` or `PyTorch_Scatter` for your system requirements if so please check the following pages [PyTorch](https://pytorch.org/get-started/locally/), [PyTorch-Scatter](https://github.com/rusty1s/pytorch_scatter).

The was developed and tested on Linux Mint 19.1 Tessa. The code should work on with other Operating Systems but it has not been tested for such use.  

## Roost Setup

Once you have setup an environment with the correct dependencies you can install `roost` using the following commands:

```bash
conda activate roost
git clone https://github.com/CompRhys/roost
cd roost
python setup.py sdist
pip install -e .
```

This will install the library in an editable state allowing for advanced users to make changes as desired.

## Example Use

In order to test your installation you can do so by running the following example from the top of your `roost` directory:

```sh
cd /path/to/roost/
python examples/roost-example.py --train --evaluate --epochs 10
```

This command runs a default task for 10 epochs -- experimental band gap regression using the data from Zhou et al. (See `data/` folder for reference). This default task has been set up to work out of the box without any changes and to give a flavour of how the model can be used. The demo task should take less than a minute when a GPU is available are give a test set MAE of 0.42-0.45 eV after 10 epochs.

If you want to use your own data set on a regression task this can be done with:

```sh
python examples/roost-example.py --data-path /path/to/your/data/data.csv --train
```

You can then test your model with:

```sh
python examples/roost-example.py --test-path /path/to/testset.csv --evaluate
```

The model takes input in the form csv files with materials-ids, composition strings and target values as the columns.

| material-id | composition | target |
| ----------- | ----------- | ------ |
| foo-1       | Fe2O3       | 2.3    |
| foo-2       | La2CuO4     | 4.3    |

Basic hints about more advanced use of the model (i.e. classification, robust losses, ensembles, tensorboard logging etc..)
are available via the command:

```sh
python examples/roost-example.py --help
```

This will output the various command-line flags that can be used to control the code.

## Cite This Work

If you use this code please cite our work for which this model was built:

[Predicting materials properties without crystal structure: Deep representation learning from stoichiometry](https://doi.org/10.1038/s41467-020-19964-7) [[arXiv](https://arxiv.org/abs/1910.00617)]

```tex
@article{goodall2020predicting,
  title={Predicting materials properties without crystal structure: Deep representation learning from stoichiometry},
  author={Goodall, Rhys EA and Lee, Alpha A},
  journal={Nature Communications},
  volume={11},
  number={1},
  pages={1--9},
  year={2020},
  publisher={Nature Publishing Group}
}
```

## Work Using Roost

A critical examination of compound stability predictions from machine-learned formation energies [[Paper]](https://www.nature.com/articles/s41524-020-00362-y) [[arXiv]](https://arxiv.org/abs/2001.10591)

If you have used Roost in your work please contact me and I will add your paper here.

## Acknowledgements

The open-source implementation of `cgcnn` available [here](https://github.com/txie-93/cgcnn) provided significant initial inspiration for how to structure this code-base.

## Disclaimer

This is research code shared without support or any guarantee on its quality. However, please do raise an issue or submit a pull request if you spot something wrong or that could be improved and I will try my best to solve it.
