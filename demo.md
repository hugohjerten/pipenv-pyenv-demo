# KDay 20th September 2019
This file will give a quick walkthrough and demo of how you can setup and use pyenv and pipenv, to make your python development life a little easier.

## 0.1 Installing pyenv & pipenv

```
# On mac. Otherwise follow official installation guides.

brew install pyenv
brew install pipenv
```

### 0.2 In case of pyenv chaos
If chaos when installing a pyenv version on macos, export the below flags for temporarily allowing to install specific python versions. (Check this [link](https://github.com/jiansoung/issues-list/issues/13).)

```
export LDFLAGS="${LDFLAGS} -L/usr/local/opt/zlib/lib"
export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/zlib/include"
export LDFLAGS="${LDFLAGS} -L/usr/local/opt/sqlite/lib"
export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/sqlite/include"
export PKG_CONFIG_PATH="${PKG_CONFIG_PATH} /usr/local/opt/zlib/lib/pkgconfig"
export PKG_CONFIG_PATH="${PKG_CONFIG_PATH} /usr/local/opt/sqlite/lib/pkgconfig"
```

## 1. pyenv

pyenv - a python installation manager. Below are some examples.

### Installing python versions
See installed python versions

```
pyenv versions
```

See available python versions

```
pyenv install --list
pyenv install --list | grep "3\.[67]"
```

Install python version

```
pyenv install 3.7-dev
```

Uninstall python version

```
pyenv uninstall 3.7-dev
```

### Specifying python versions

Set local python version (.python-version)

```
pyenv local 3.7.2
python --version
which python
```

Set global python version

```
pyenv global system
```


## 2. pipenv

### Setting up virtual environment

Set up a python virtual environment

```
pipenv --python 3.6.8
```

`Pipfile` provides the overview of the virtual environment. As of yet there is no `Pipfile.lock` file since we havn't specified any packages. We will do that now.

```
pipenv install numpy bokeh
```

Now a `Pipfile.lock` has been created, which provides the specification for all packages needed (including dependecnies), with corresponding versions.

```
less Pipfile
less Pipfile.lock
```

Install specific version of package. Will install version `0.24.1`, and any minor updates, but not `0.25`

```
pipenv install pandas~=0.24.1
```

Uninstall package.

```
pipenv uninstall pandas
```

Install exact version of package. Will never update.

```
pipenv install pandas==0.24.2
```


Install package for development

```
pipenv install --dev pytest pylint

less Pipfile
less Pipfile.lock
```

### Using virtual environment

Spawns a shell within virtualenv

```
# Will fail since module isn't available
python
import numpy as np
from bokeh.plotting import figure
exit()

# Will work
pipenv shell
python
import numpy as np
from bokeh.plotting import figure
exit()

exit
```

Spawn a command within virtualenv

```
# Will fail since module isn't available
python plot_figure.py

# Will work
pipenv run python plot_figure.py
```

### See an overview of dependency resolution

Understand which dependencies that your installed packages have and that have been installed. The below command will also show version of the packages that have been installed, and which versions of the dependant packages that are required.

```
pipen graph
```


### Copying environment using `Pipfile.lock`

When multiple people are working on the same project, it becomes even more important that the environment is set up the same way on different local devices.
The `Pipfile.lock` file helps with that.

```
mkdir project_2
cp project_1/plot_figure project_2/
cp project_1/Pipfile.lock project_2/
cd project_2

pipenv sync
```


### Update packages

Get a list of which packages have updates available.

```
pipenv update --outdated
```

Update a specific package.

```
pipenv update pandas
```
