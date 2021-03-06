## Technical Considerations 

- Hardware:
     - Ideally, you will use a strong GPU with at least 8GB memory such as the [NVIDIA GeForce 1080 Ti](https://www.nvidia.com/en-us/geforce/products/10series/geforce-gtx-1080/). There are no other hardware requirements. Such consumer electronics cards have a very good price point and will become increasingly more affordable. In particular, the software is very robust to track data from pretty much any camera (grayscale, color, or graysale captured under infrared light etc.). A GPU is not necessary, but on a CPU the (training and evaluation) code is considerably slower (100x). You might also consider using cloud computing services like [Google cloud/amazon web services](https://github.com/AlexEMG/DeepLabCut/issues/47).


- Software: 
     - We recommend using the supplied [Docker container](https://github.com/AlexEMG/Docker4DeepLabCut). NOTE: [this container does not work on windows hosts!](https://github.com/NVIDIA/nvidia-docker/issues/43)
     - The toolbox is written in [Python 3](https://www.python.org/). You will need [TensorFlow](https://www.tensorflow.org/) (we used 1.0 for figures in papers, later versions also work with the provided code (we tested **TensorFlow versions 1.0 to 1.4 and 1.8**) for Python 3 with GPU support. 
     - To note, is it possible to run DeepLabCut on your CPU, but it will be VERY slow. However, this is the preferred path if you want to test DeepLabCut on your data before purchasing a GPU, with the added benefit of a straightforward installation. 

For reference, we use e.g. Dell workstations (79xx series) with Ubuntu 16.04 LTS and run a Docker container that has TensorFlow, etc. installed (https://github.com/AlexEMG/Docker4DeepLabCut). The DeepLabCut code also runs on Windows (thanks to  [Richard Warren](https://github.com/rwarren2163) for checking it) or MacOS (some users have already successfully done so). 


## Simplified installation with conda environments including TensorFlow for a CPU:

[Anaconda](https://anaconda.org/anaconda/python) is perhaps the easiest way to install Python and additional packages across various operating systems. With anaconda just create all the dependencies in an [environment](https://conda.io/docs/user-guide/tasks/manage-environments.html) on your machine by running in a terminal:
```
git clone https://github.com/AlexEMG/DeepLabCut.git
cd DeepLabCut/conda-files
conda env create -f dlcdependencieswTF1.2.yml
```

Some conda channels are different for Windows and Rick Warren contributed the following yml file for **Windows** which actually features TensorFlow 1.8:

```
conda env create -f dlcDependenciesFORWINDOWSwTF.yaml
```

Note that these environment yaml file [might not work across platforms (other versions of Windows, MacOS, ...)](https://stackoverflow.com/questions/39280638/how-to-share-conda-environments-across-platforms). Installing TensorTlow on your CPU is easy on any platform, if the environment yaml with TensorFlow does not work for you, then install the one without (see below) and then follow the instructions here for installing [Tensorflow](https://www.tensorflow.org/versions/r1.2/install/). 

Again, DeepLabCut (like all large DeepNeuralNetworks) is rather slow on CPU architectures, which is why we recommend using a GPU (then skip this previous step). 

Once you installed the environment you can activate it, by typing on Linux/MacOS: 
```
source activate DLCdependencies
```
and on Windows do: 
```
activate DLCdependencies
```

Then you can work with all DLC functionalities inside this environment. 

## TensorFlow Installation with GPU support:

- **Docker: We highly recommend to use the supplied [Docker container](https://github.com/AlexEMG/Docker4DeepLabCut), which has everything including TensorFlow for the GPU preinstalled. NOTE: [this container does not work on windows hosts!](https://github.com/NVIDIA/nvidia-docker/issues/43)**

 - If you do not want to use Docker, first create an environment with all dependencies but TensorFlow:
```
git clone https://github.com/AlexEMG/DeepLabCut.git
cd DeepLabCut
conda env create -f dlcdependencies.yml
```
Again on **Windows** use (instead with TensorFlow 1.8):
```
conda env create -f dlcDependenciesFORWINDOWS.yaml
```

Then install [TensorFlow](https://www.tensorflow.org/). Ideally install **TensorFlow 1.0 with CUDA (Cuda 8.0)** (or TensorFlow 1.2, 1.4 or 1.8 / other versions might work too but might require different CUDA versions.). Please check your CUDA and [TensorFlow installation](https://www.tensorflow.org/install/) with this line (below), and you can test that your GPU is being properly engaged with these additional [tips](https://www.tensorflow.org/programmers_guide/using_gpu).

      $ sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
           
      
 Return to [readme](../README.md).

