#python 

```shell
pip --help

pip help install # show help for install command

pip search 

pip list # list all installed packages

# check packages need upgrade
pip list --outdated
pip list -o
pip install -u packageName # upgrade the package

pip install packageName
pip uninstall packageName
```

### VENV (Virtual Environment)

```shell
pip list
pip3 list
```

> [!info]
> use VSCode to create venv
> ![[python-create-venv-VSCode.gif]]


```shell
# create a venv and also create a folder
python3 -m venv venvName
python3 -m venv venv
python3 -m venv project_env

# venv naming convention → "venv"
python3 -m venv myproject/venv
# venv path should be added to gitignore

# use the venv
source project_env/bin/activate

./venv/Scripts/activate # Windows
./venv/bin/activate # Mac

# deactivate the vene
deactivate

# delete the vene files
rm rf project_env/
```

![[activate-venv.png|400]]

`which python` will show current python is at the venv path
![[which-python.png|400]]
  
Output exact version
```shell
pip freeze
pip freeze --local # (venv local packages)

pip freeze > requirement.txt

# install the same pip install by requirement.txt
pip install -r requirement.txt
```

let the venv to have global packages

```shell
# with replicate of gloable packages
python3 -m venv venv --system-site-packages

# list packages only in the vene, not in the global
pip list --local
pip freeze # also only show the local packages
```

### UV

https://docs.astral.sh/uv/guides/install-python/

100x faster than pip, written in rust
handle virtual environment

run script
``` sh
# run script
uv run main.py
uv run --python 3.9 main.py # run use python 3.9
uv run --with packageName --python 3.9 main.py # install dependency and run

uv run main.py
↓ in the file
#/// script
# requires-python = "==3.9"
# dependencies = ["rich"]
#///
```

project
```sh
uv init
uv init . # create a project

# add pacakge
# automatically create virtual environment
uv add langchain-openai langgraph python-dotenv
uv add requests==2.2.3

# remove package
uv remove requests


uv sync # npm i
```

Python
```sh
# manage python
uv python list

# install a python 3.8
uv python install 3.8
uv python uninstall 

# 
uv python find 3.8
```

Checking typing error
```sh
uvx mypy main.py
```