# Assignments for [Berkeley CS 285: Deep Reinforcement Learning, Decision Making, and Control](http://rail.eecs.berkeley.edu/deeprlcourse/).

# Setup
This fork is intented to be run from a linux environment or in WSL2 (Windows Subsytem for Linux).
1. Turn on Windows features Hyper-V, Virtual Machine Platform, Windows Hypervisor Platform, Windows Subsystem for Linux. If you are on Windows 10, you may need to register to be a developer. On Windows 11, there should not be a problem.
2. Install Ubuntu (just Ubuntu, not Ubuntu-22.04 or something) from Windows Store.
3. Install `terminal` from Windows Store, it enables easy access to wsl environments by clicking the button next `+` sign in the tabs menu.
4. Install Mujoco 2.1.0
    ```
    wget https://github.com/deepmind/mujoco/releases/download/2.1.0/mujoco210-linux-x86_64.tar.gz
    tar -xvf mujoco210-linux-x86_64.tar.gz
    mkdir ~/.mujoco
    sudo cp mujoco210 ~/.mujoco/
    echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/darkness/.mujoco/mujoco210/bin' >> ~/.bashrc
    ```
5. Install the requirements
    ```
    sudo apt install sudo apt-get install python3 python3-dev libosmesa6-dev patchelf
    pip3 install requirements.txt
    echo 'export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0 #GWSL' >> ~/.bashrc
    echo 'export PULSE_SERVER=tcp:$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}') #GWSL' >> ~/.bashrc
    echo 'export LIBGL_ALWAYS_INDIRECT=1 #GWSL' >> ~/.bashrc
    ```
6. (Optional) Installing PyTorch with Nvidia GPU Support (Assumes you have a CUDA enabled GPU)
    * Installing Cuda 11.7
    ```
    wget https://developer.download.nvidia.com/compute/cuda/11.7.0/local_installers/cuda_11.7.0_515.43.04_linux.run
    sudo sh cuda_11.7.0_515.43.04_linux.run
    ```
    * May need to choose to install the driver.
    * Adding necessary paths to the .bashrc file
    ```
    echo 'export PATH=/usr/local/cuda-11.7/bin:$PATH' >> ~/.bashrc
    echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
    echo 'export LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
    echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
    ```
    * Go [here](https://developer.nvidia.com/cudnn) and download cudnn (you may need to create an nvidia account). Untar and copy the contents to their respective locations:
    ```
    sudo cp <name-of-the-untarred-folder>/include/cudnn*.h /usr/local/cuda/include
    sudo cp <name-of-the-untarred-folder>/lib/libcudnn* /usr/local/cuda/lib
    sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
    ```
    * Install PyTorch
    ```
    pip3 install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cu113
    ```
Hopefully, now you should be able to run the homeworks with GPU support as well.
