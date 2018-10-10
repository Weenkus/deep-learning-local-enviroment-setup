# Deeplearning Local Environment Setup (GPU)

A tutorial how to setup a local deep learning environment. I tend to forget things, therefore this is a remainder how I like doing it. The general gist is that instead of installing CUDA and playing with local enviroments we will use [docker](https://www.docker.com/) and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) which installs CUDA for us making our job pasting one line of code.

# Dependencies

* [docker](https://docs.docker.com/install/)
* [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)

# Setup

### 1. Install Dependencies
### 2. Verify Install

Run this to verify first step (probably need to restart terminal if docker was added to sudo users, heck just restart your whole machine) 
```bash
  docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
```

### 3. Create a Deep Learning Container
Create a docker container (the `-v` maps your local file sytem to docker one `/workspace` so that you can access those files from inside docker.

    * [PyTorch](https://pytorch.org/)
    ```bash
    nvidia-docker run -it -p 8888:8888 --name=pytorch --ipc=host -v /path_to_your_project_dir:/workspace pytorch/pytorch:latest
    ```
    
    * [TensorFlow](https://www.tensorflow.org/)
    ```bash
    nvidia-docker run -it -p 8888:8888 --name=tensorflow --ipc=host -v /path_to_your_project_dir:/workspace gcr.io/tensorflow/tensorflow:latest-gpu-py3

  
### 4. Install Libraries
Now that you are inside the shell you can install anything you want. First we need to shell into the container than run install commands.
  * Shell into a docker container
  ```bash
  docker exec -it container_name bash
  ```

  * [Jupyter](https://jupyter.org/install)
  ```bash
  python3 -m pip install --upgrade pip
  python3 -m pip install jupyter
  ```

  * General purpose scientific compute libs and utilities
  ```bash
  python3 -m pip install tqdm keras scipy matplotlib numpy scipy nltk
  ```
  
### 5. Docker Container Basics
Basic commands to help you start with docker.

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
 
# Author

Have any questions, ping me on vinko.kodzoman@yahoo.com
