# Installation of Theano on Windows 7 for Visual Studio 2010 for Academic use
========================================
* Install [visual studio 2010](https://www.dreamspark.com/)
* Download and install [CUDA 7.0](https://developer.nvidia.com/cuda-downloads)
* Install [TDM GCC](http://tdm-gcc.tdragon.net/)

  Theano C code compiler currently requires a GCC installation. We have used the build TDM GCC which is provided for both 32- and 64-bit platforms. A few caveats to watch for during installation:

   1. Install to a directory without spaces (we have placed it in C:\SciSoft\TDM-GCC-64)
   2. If you don’t want to clutter your system PATH un-check add to path option.
   3. Enable OpenMP support by checking the option openmp support option.

* create virtual env for deep learn python, so it will not mess up your current python
  open Anaconda Command Prompt
  conda create --name dl_python python=2

* Install [Anaconda](https://store.continuum.io/cshop/anaconda/) with [Anaconda Accelerate](https://store.continuum.io/cshop/academicanaconda), which is Fast Python for GPUs and multi-core with NumbaPro and MKL Optimizations)

~~~~bat
activate dl_python
conda install mkl
conda install accelerate
conda install mingw libpython
conda install pydot-ng
conda install scikit-learn
~~~~  

* Create .theanorc.txt under %USERPROFILE% folder. Copy following into file.
~~~~bat
[global]
floatX = float32
device = gpu
[nvcc]
flags = --use-local-env  --cl-version=2010
~~~~

* Create a batch file setenv.bat to set the following environment

~~~~bat

REM configuration of paths
set VSFORPYTHON="C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC"
set SCISOFT=%~dp0

REM add tdm gcc stuff
set PATH=c:\TDM-GCC-64\bin;c:\TDM-GCC-64\x86_64-w64-mingw32\bin;%PATH%

REM add anaconda env
CALL C:\Users\simuser\Anaconda\Scripts\anaconda.bat

REM configure path for msvc compilers
REM for a 32 bit installation change this line to
REM CALL %VSFORPYTHON%\vcvarsall.bat
CALL %VSFORPYTHON%\vcvarsall.bat amd64
CALL activate dl_python
REM return a shell
cmd.exe /k

~~~~
* Run the setenv.bat and install Theano

~~~~bat
conda install pydot-ng
pip install git+https://github.com/Theano/Theano.git
~~~~

* In setenv.bat: Run python check1.py and you should see that you python script are using gpu.

~~~~bat
python check1.py
  Using gpu device 0: Quadro 4000
  [GpuElemwise{exp,no_inplace}(<CudaNdarrayType(float32, vector)>), HostFromGpu(GpuElemwise{exp,no_inplace}.0)]
  Looping 1000 times took 0.910000085831 seconds
  Result is [ 1.23178029  1.61879349  1.52278066 ...,  2.20771813  2.29967761
    1.62323296]
  Used the gpu
~~~~
* Run the setenv.bat and install Lasagne

~~~~bat
  pip install https://github.com/Lasagne/Lasagne/archive/master.zip
  conda install matplotlib
  python mnist.py
~~~~

* Run python mnist.py to test installation of lasagne, you should see output information after several nvcc compile information

~~~~bat
python mnist.py

Starting training...
Epoch 1 of 50 took 2.630s
  training loss:                1.230027
  validation loss:              0.410091
  validation accuracy:          88.64 %

~~~~

* Run the setenv.bat and install pandas, scikit-learn, nolearn

~~~~bat
  conda install pandas
  pip install git+https://github.com/dnouri/nolearn.git@master#egg=nolearn==0.7.git
~~~~

* Run python mnist_nolearn.py to test installation of nolearn

~~~~bat
python mnist_nolearn.py

Using gpu device 0: Quadro 4000 (CNMeM is disabled)
Loading data...
DEBUG: nvcc STDOUT mod.cu
   Creating library C:/Users/simuser/AppData/Local/Theano/compiledir_Windows-7-6.1.7601-SP1-Intel64_Family_6_Model_44_St
epping_2_GenuineIntel-2.7.10-64/tmpozxlxp/88b4f8c09b81504243de03738d23d308.lib and object C:/Users/simuser/AppData/Local
/Theano/compiledir_Windows-7-6.1.7601-SP1-Intel64_Family_6_Model_44_Stepping_2_GenuineIntel-2.7.10-64/tmpozxlxp/88b4f8c0
9b81504243de03738d23d308.exp

# Neural Network with 1276810 learnable parameters

## Layer information

  #  name         size
---  -----------  -------
  0  input        1x28x28
  1  inputDrop    1x28x28
  2  hidden1      800
  3  hidden1Drop  800
  4  hidden2      800
  5  hidden2Drop  800
  6  output       10

  epoch    train loss    valid loss    train/val    valid acc  dur
-------  ------------  ------------  -----------  -----------  -----
      1       ←[36m0.69431←[0m       ←[32m0.24281←[0m      2.85946      0.92890  4.79s
      2       ←[36m0.35514←[0m       ←[32m0.17866←[0m      1.98783      0.94858  4.86s
      3       ←[36m0.28206←[0m       ←[32m0.14359←[0m      1.96431      0.96064  4.79s
      4       ←[36m0.23673←[0m       ←[32m0.12444←[0m      1.90238      0.96598  4.88s
      5       ←[36m0.21256←[0m       ←[32m0.11248←[0m      1.88966      0.96954  4.91s
      6       ←[36m0.19146←[0m       ←[32m0.10138←[0m      1.88847      0.97093  4.83s
      7       ←[36m0.17600←[0m       ←[32m0.09579←[0m      1.83726      0.97231  4.91s
      8       ←[36m0.16370←[0m       ←[32m0.08897←[0m      1.83999      0.97439  4.77s
      9       ←[36m0.15022←[0m       ←[32m0.08424←[0m      1.78316      0.97488  4.78s
     10       ←[36m0.14097←[0m       ←[32m0.08132←[0m      1.73363      0.97528  4.93s
     11       ←[36m0.13568←[0m       ←[32m0.07851←[0m      1.72806      0.97696  4.86s
     12       ←[36m0.13062←[0m       ←[32m0.07406←[0m      1.76359      0.97785  4.89s
~~~~

* Run the setenv.bat and install keras
```bat
pip install keras
```
* Configure pycharm to run keras

  1. Run the setenv.bat
  2. echo %PATH%
  3. echo %lib%
  4. echo %include%
  5. copy these three variable values into pycharm run env vaiables
