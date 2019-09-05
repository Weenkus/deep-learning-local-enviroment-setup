# Deep Learning Local Environment Setup (GPU)

A tutorial for how to set up a local deep learning environment. I tend to forget things, so this is a reminder of how I like to do it. The gist of it is that, instead of installing CUDA and playing with local enviroments, we will use [docker](https://www.docker.com/) and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) which will install CUDA for us, so that our job comes down to just copying and pasting a single line of code.

# Dependencies

* [docker](https://docs.docker.com/install/)
* [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)

# Setup

### 1. Install Dependencies
### 2. Verify Install

Run this to verify the first step (you will probably need to restart the terminal if docker was added to sudo users. Heck, just restart your whole machine).
  ```bash
  docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
  ```

### 3. Create a Deep Learning Container
Create a docker container (the `-v` maps your local file sytem to docker one `/workspace` so that you can access those files from inside docker).

  * [TensorFlow](https://www.tensorflow.org/)
     ```bash 
    nvidia-docker run -it -p 127.0.0.1:8888:8888 --name=tensorflow --ipc=host -v /path_to_your_project_dir:/notebooks/workspace tensorflow/tensorflow:latest-gpu-py3
    ```
    
  * [PyTorch](https://pytorch.org/)
    ```bash
    nvidia-docker run -it -p 8888:8888 --name=pytorch --ipc=host -v /path_to_your_project_dir:/notebooks/workspace pytorch/pytorch:latest
    ```

  
### 4. Install Libraries
Now that you are inside the shell, you can install anything you want. First, we need to shell into the container, then run the install commands.
  * Shell into a docker container
  ```bash
  docker exec -it container_name bash
  ```

  * General purpose scientific compute libraries and utilities
  ```bash
  python3 -m pip install --upgrade pip
  python3 -m pip install jupyter tqdm keras scipy matplotlib numpy scipy nltk sklearn lightgbm kaggle h5py xgboost gensim spacy requests pandas
  ```
  
### 5. Docker Container Basics
Basic commands to help you get started with docker.

  * Start a container
    ```bash
    docker start container_name
    ```
  
  * Stop a container
     ```bash
     docker start container_name
     ```
  
  * Show images
    ```bash
    docker images
    ```
  
  * Show processes
    ```bash
    docker ps
    ```
  
  * Show all processes
    ```bash
    docker ps -a
    ```
  
  * Delete all stopped containers
    ```bash
    docker container prune
    ```
    
### 6. Jupyter
To run Jupyter Notebooks:
```bash
jupyter notebook --port=8888 --ip=127.0.0.1 --allow-root
```
 
# Author

If you have any questions, ping me on vinko.kodzoman@yahoo.com
