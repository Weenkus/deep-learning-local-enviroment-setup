# Deeplearning Local Environment Setup (GPU)

A tutorial how to setup a local deep learning environment. I tend to forget things, therefore this is a remainder how I like doing it. The general gist is that instead of installing CUDA and playing with local enviroments we will use [docker](https://www.docker.com/) and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) which installs CUDA for us making our job pasting one line of code.

# Dependencies

* [docker](https://docs.docker.com/install/)
* [nvidia-docker](https://github.com/NVIDIA/nvidia-docker)

# Setup

1. Install dependencies
2. Run this to verify first step (probably need to restart terminal if docker was added to sudo users, heck just restart your whole machine) 
```bash
  docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
```

3. Create a docker container (the `-v` maps your local file sytem to docker one `/workspace` so that you can access those files from inside docker.

    * [PyTorch](https://pytorch.org/)
    ```bash
    nvidia-docker run -it -p 8888:8888 --name=pytorch --ipc=host -v /path_to_your_project_dir:/workspace pytorch/pytorch:latest
    ```
    
    * [TensorFlow](https://www.tensorflow.org/)
    ```bash
    nvidia-docker run -it -p 8888:8888 --name=tensorflow --ipc=host -v /path_to_your_project_dir:/workspace gcr.io/tensorflow/tensorflow:latest-gpu-py3

    ```
    
4. Shell into your container and install everything you need
  ```bash
  docker exec -it container_name bash
  ```
Now that you are inside the shell you can install anything you want.
  * [Jupyter](https://jupyter.org/install)
  ```bash
  python3 -m pip install --upgrade pip
  python3 -m pip install jupyter
  ```

  * General purpose scientific compute libs and utilities
  ```bash
  python3 -m pip install tqdm keras scipy matplotlib numpy scipy nltk
  ```
  
5. Docker container basics

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
