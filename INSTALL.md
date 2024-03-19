### Set up the python environment

```shell
conda create -n animatable_nerf python=3.7
conda activate animatable_nerf

# make sure that the pytorch cuda is consistent with the system cuda
# e.g., if your system cuda is 10.0, install torch 1.4 built from cuda 10.1
conda install pytorch==1.4.0 cudatoolkit=10.1 -c pytorch

pip install -r requirements.txt
```

If someone wants to run the baseline methods `NHR` and `NT`, please install the libraries:

```shell
# install poinetnet2
ROOT=/path/to/animatable_nerf
cd $ROOT/lib/csrc/pointnet2
python setup.py build_ext --inplace

# install PCPR
cd ~
git clone https://github.com/wuminye/PCPR.git
cd PCPR
python setup.py install

# install pytorch3d
cd ~
git clone https://github.com/facebookresearch/pytorch3d.git
cd pytorch3d
git checkout tags/v0.4.0
echo "edit pytorch3d/csrc/pulsar/global.h file by adding '#include <vector_functions.h>' in header, and comment make_float3 function"
python setup.py install
```

### Set up data

The `data` folder should contain `trained_model/deform`, `zju_mocap` and `h36m`. Other datasets include `monocap`, `synthetichuman`, `deepcap`, `loose_cloth` and `light_stage`

You can download the trained models [here](https://drive.google.com/drive/folders/1XH5zUMkguUW64GKulWTo8oOWZra6Dnzy?usp=sharing) and request datasets in the following instructions:

#### Human3.6M dataset

1. Since the license of Human3.6M dataset does not allow us to distribute its data, we cannot release the processed Human3.6M dataset publicly. If someone is interested at the processed data, please email me.
2. If someone wants to run the baseline method `NT`, please run the script:

    ```shell
    python tools/render_h36m_uvmaps_pytorch3d.py
    ```

#### ZJU-Mocap dataset

If someone wants to download the ZJU-Mocap dataset, please fill the [form](https://docs.google.com/forms/d/1QcTp5qIbIBn8PCT-EQgG-fOB4HZ9khpRkT3q2OnH2bs) to obtain the download link. Another way is filling in the [agreement](https://pengsida.net/project_page_assets/files/ZJU-MoCap_Agreement.pdf) and emailing me (pengsida@zju.edu.cn) and cc Xiaowei Zhou (xwzhou@zju.edu.cn) to request the download link.

#### MonoCap Dataset

1. MonoCap is a dataset composed by authors of [animatable sdf](https://zju3dv.github.io/animatable_sdf/) from [DeepCap](https://people.mpi-inf.mpg.de/~mhaberma/projects/2020-cvpr-deepcap/) and [DynaCap](https://people.mpi-inf.mpg.de/~mhaberma/projects/2021-ddc/).
2. Since the license of [DeepCap](https://people.mpi-inf.mpg.de/~mhaberma/projects/2020-cvpr-deepcap/) and [DynaCap](https://people.mpi-inf.mpg.de/~mhaberma/projects/2021-ddc/) dataset does not allow us to distribute its data, we cannot release the processed MonoCap dataset publicly. If you are interested in the processed data, please download the raw data from [here](https://gvv-assets.mpi-inf.mpg.de/) and email me for instructions on how to process the data.

#### SyntheticHuman Dataset

1. SyntheticHuman is a dataset created by authors of [animatable sdf](https://zju3dv.github.io/animatable_sdf/). It contains multi-view videos of 3D human rendered from characters in the [RenderPeople](https://renderpeople.com/) dataset along with the groud truth 3D models.
2. Since the license of the [RenderPeople](https://renderpeople.com/) dataset does not allow distribution of the 3D models, we cannot realease the processed SyntheticHuman dataset publicly. If you are interested in this dataset, please email me for instructions on how to generate the data.
