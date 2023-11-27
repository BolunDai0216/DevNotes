# Installing OMPL's Python Bindings

## Ubuntu

First install `CastXML` and `pygccxml` using

```bash
sudo apt-get install -y castxml
python3 -m pip install pygccxml
```

Then clone `pyplusplus` and install it from source

```bash
https://github.com/ompl/pyplusplus.git
cd pyplusplus
python3 -m pip install .
```

Then clone `OMPL` and install it from source

```bash
git clone https://github.com/ompl/ompl.git
cd ompl
mkdir build && cd build
```

Then configure and build OMPL

```bash
cmake ..
make clean_bindings
make -j 16 update_bindings 
make -j 16 py_ompl
```

Finally add the following lines to you `.bashrc` or `.zshrc` file

```bash
export PYTHONPATH=$PYTHONPATH:/path/to/ompl/build/lib:/path/to/ompl/py-bindings
```

Then you should be able to successfully import `ompl` in Python

```python
from ompl import geometric as og
from ompl import base as ob
```