# Abductive Learning for Handwritten Equation Decipherment

This is an anonymous repository for holding the sample code of the abductive
learning framework for handwritten equation decipherment experiments in
_Bridging Machine Learning and Logical Reasoning by Abductive Learning_
submitted to NeurIPS 2019.

## Environment dependency

**This code is only tested in Linux environment.**

1. Swi-Prolog
2. Python3 with Numpy, Tensorflow and Keras
3. ZOOpt (as a submodule)

### Install Swipl
[http://www.swi-prolog.org/build/unix.html](http://www.swi-prolog.org/build/unix.html)


### Install python3

<https://wiki.python.org/moin/BeginnersGuide/Download>

#### Install required package

```shell
#install numpy tensorflow keras
pip3 install numpy
pip3 install tensorflow
pip3 intall keras
```

**Set environment variables(Should change file path according to your situation)**

```Shell
# cd to ABL-HED
git submodule update --init --recursive

export ABL_HOME=$PWD
cp /usr/local/lib/swipl/lib/x86_64-linux/libswipl.so $ABL_HOME/src/logic/lib/
export LD_LIBRARY_PATH=$ABL_HOME/src/logic/lib
export SWI_HOME_DIR=/usr/local/lib/swipl/

# for GPU user
export LD_LIBRARY_PATH=$ABL_HOME/src/logic/lib:/usr/local/cuda:$LD_LIBRARY_PATH

```


#### Install Abductive Learning code

**First change the `swipl_include_dir` and `swipl_lib_dir` in `setup.py` to your own SWI-Prolog path.**

```Shell
cd src/logic/prolog
python3 setup.py install
```

**Build ZOOpt**
```Shell
cd src/logic/lib/ZOOpt
python3 setup.py build
cp -r build/lib/zoopt ../
```


## Demo for arithmetic addition learning

Change directory to `ABL-HED`, and run equaiton generator to get the training data

```shell
cd src/
python3 equation_generator.py
```

Run abductive learning code

```shell
cd src/
python3 main.py
```

or
```shell
python3 main.py --help
```

To test the RBA example, please specify the `src_data_name` and `src_data_file`
together, e.g.,

```shell
python main.py --src_data_name random_images --src_data_file random_equation_data_train_len_26_test_len_26_sys_2_.pk
```
## Remark

1. It is possible that the logic abduction finds a __trivial__ but __consistent__
   solution: all equations are `0000+0000=0000` with the only rule
   `my_op([0],[0],[0])`. If it happens, don't hesitate and __kill__ the program, just
   re-run it and give it another chance :)
2. The mapping from CNN to symbolic primitive symbols are learned, so it is fine
   if ABL learns `0+0=01` and `1+1=1`, it just swaps the semantics of `0` and `1`.
