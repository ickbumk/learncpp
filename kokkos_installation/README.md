# How to install kokkos

First install prerequisites

```bash

sudo apt update 
sudo apt install build-essential dkms 

```

Then you can download the CUDA toolkit for GPU utilization. For example, for Ubuntu 22.04:

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /"
sudo apt update
sudo apt install cuda

```

You may need different wget address for different versions of Ubuntu. Now you can add CUDA to your path. Open your bashrc:

```bash
vim ~/.bashrc
```

and paste the following in the last line:

```bash
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

Then you can source it

```bash
source ~/.bashrc
```

You can verify installation by:
```bash
nvcc --version
nvidia-smi
```

# Installing Kokkos

Install basic tools and CMake:

```bash
sudo apt update
sudo apt install git cmake g++ build-essential
```

Clone the Kokkos repo:
```bash
git clone https://github.com/kokkos/kokkos.git
cd kokkos
git checkout tags/4.6.00
```
The last checkout version needs to change depending on your needs.

```bash
mkdir build
cd build
```

Then Configure the build with CMake for CUDA support:
```bash
cmake .. -DCMAKE_CXX_COMPILER=/path/to/kokkos/bin/nvcc_wrapper \
         -DKokkos_ENABLE_CUDA=ON \
         -DCMAKE_INSTALL_PREFIX=$HOME/kokkos-install
make -j$(nproc)
make install
```

You can add NVCC WRAPPER to your Path :
```bash
export PATH=/your/path/to/kokkos/bin:$PATH
```
By pasting above in your bashrc.
Then run
```bash
source ~/.bashrc
```

# After installation

You can use the installed kokkos in your projects by adding this to your project's CMake:
```bash
find_package(Kokkos REQUIRED PATHS $ENV{HOME}/kokkos-install)
target_link_libraries(your_target PRIVATE Kokkos::kokkos)
```




