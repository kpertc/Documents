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
python3 -m venv project_env

# venv naming convention → "venv"
python3 -m venv myproject/venv
# venv path should be added to gitignore

# use the venv
source project_env/bin/activate

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