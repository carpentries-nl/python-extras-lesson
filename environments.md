# Conda environments

Often packages we're using depend on different versions of other packages or
even worse different versions of python. Conda provides the way to work in isolated environments with different versions of python and/or packages.
To learn more about conda environments run `conda env --help`

## Listing environments
It's easy to loose track of all environments we have created. We can list all
available environments with:

```sh
$ conda info --envs
# conda environments:
#
cornflakes               ~/anaconda/envs/cornflakes
py27                     ~/anaconda/envs/py27
snowflakes            *  ~/anaconda/envs/snowflakes
root                     ~/anaconda
```

This will list all installed environments and paths where they can be found
in the file system. An Asterisk points to active environment. The other way
to achieve the same result is:

```
$ conda env list
# conda environments:
#
cornflakes               ~/anaconda/envs/cornflakes
py27                     ~/anaconda/envs/py27
snowflakes            *  ~/anaconda/envs/snowflakes
root                     ~/anaconda
```

## Creating an environment
To create a new environment we need to specify a name for it and a name of
the package that we want to install inside this environment.

```
$ conda create --name marsmission astropy
Fetching package metadata: ....
Solving package specifications: .........

Package plan for installation in environment ~/anaconda/envs/marsmission:

The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    numpy-1.11.0               |           py35_0         2.7 MB
    astropy-1.1.2              |      np111py35_0         6.1 MB
    ------------------------------------------------------------
                                           Total:         8.8 MB

The following NEW packages will be INSTALLED:

    astropy:    1.1.2-np111py35_0
    mkl:        11.3.1-0
    ...
```

We can also create environment with specific version of python.
```
$ conda create python=2.7 --name marsmission-2.7
```

## Switching between environments
To switch between environment we have to `deactivate` active one and `activate` new one.

```
# on linux and mac
$ source activate marsmission
discarding ~/anaconda/envs/snowflakes/bin from PATH
prepending ~/anaconda/envs/marsmission/bin to PATH

# on windows
$ activate marsmission
```

We can also `deactivate` an environment without activating new one.

```
$ source deactivate
discarding ~/anaconda/envs/marsmission/bin from PATH
```

## Installing packages
When installing the package, it will be installed into environment
currently active.
```
$ conda install pyflakes
Fetching package metadata: ....
Solving package specifications: .........

Package plan for installation in environment ~/anaconda:

The following NEW packages will be INSTALLED:

    pyflakes: 1.1.0-py35_0

Proceed ([y]/n)?
```

## Reproducible environments
We might want to save the list of all packages that are needed in our environment. Lets first list all packages.

```
$ conda list -e
# This file may be used to create an environment using:
# $ conda create --name <env> --file <this file>
# platform: osx-64
appnope=0.1.0=py35_0
decorator=4.0.9=py35_0
ipython=4.1.2=py35_2
ipython_genutils=0.1.0=py35_0
openssl=1.0.2g=0
path.py=8.2=py35_0
readline=6.2=2
setuptools=20.7.0=py35_0
simplegeneric=0.8.1=py35_0
sqlite=3.9.2=0
tk=8.5.18=0
sqlite=3.9.2=0
tk=8.5.18=0
traitlets=4.2.1=py35_0
wheel=0.29.0=py35_0
xz=5.0.5=1
zlib=1.2.8=0
```

We can reuse it if we save it to the file.
```
$ conda list -e > requirements.txt
# This file may be used to create an environment using:
# $ conda create --name <env> --file <this file>
# platform: osx-64
```

Now as suggested in the output of previous comment we can create a new environment based on created file.

```
$ conda create --name mission2 --file requirements.txt
Fetching package metadata: ....
.Solving package specifications: ....
```

# Removing environments
Environments can take up a lot of space. We can remove any environment.
```
$ conda remove --name cornflakes --all
Fetching package metadata: ....

Package plan for package removal in environment ~/anaconda/envs/cornflakes:

The following packages will be REMOVED:

    appnope:          0.1.0-py35_0
    decorator:        4.0.9-py35_0
    ipython:          4.1.2-py35_2
...
```
