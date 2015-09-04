# Installation of Theano on Windows 7 for Visual Studio 2010 for Academic use
========================================
* Install [visual studio 2010](https://www.dreamspark.com/)
* Download and install [CUDA 7.0](https://developer.nvidia.com/cuda-downloads)
* Install [TDM GCC](http://tdm-gcc.tdragon.net/)

  Theano C code compiler currently requires a GCC installation. We have used the build TDM GCC which is provided for both 32- and 64-bit platforms. A few caveats to watch for during installation:

   1. Install to a directory without spaces (we have placed it in C:\SciSoft\TDM-GCC-64)
   2. If you don’t want to clutter your system PATH un-check add to path option.
   3. Enable OpenMP support by checking the option openmp support option.

* Install [Anaconda](https://store.continuum.io/cshop/anaconda/) with [Anaconda Accelerate](https://store.continuum.io/cshop/academicanaconda), which is Fast Python for GPUs and multi-core with NumbaPro and MKL Optimizations)

* Goto anaconda command prompt and pip install Theano

* Set the following environment
 1. add C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin\amd64; to PATH for 64bit Windows
 2. set VSFORPYTHON = C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC

* Create .theanorc.txt under %USERPROFILE% folder. Copy following into file.

~~~~
[global]
floatX = float32
device = gpu

[nvcc]
flags = --use-local-env  --cl-version=2010
~~~~

* Goto anaconda command prompt and Run python check1.py and you should see that you python script are using gpu.

~~~~
Using gpu device 0: Quadro 4000
[GpuElemwise{exp,no_inplace}(<CudaNdarrayType(float32, vector)>), HostFromGpu(GpuElemwise{exp,no_inplace}.0)]
Looping 1000 times took 0.910000085831 seconds
Result is [ 1.23178029  1.61879349  1.52278066 ...,  2.20771813  2.29967761
  1.62323296]
Used the gpu
~~~~
