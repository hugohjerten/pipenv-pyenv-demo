# KDay 20th September 2019
This file will give a quick walkthrough and demo of how you can setup and use pyenv and pipenv, to make your python development life a little easier.

## 0.1 Installing pyenv & pipenv

```
# On mac. Otherwise follow official installation guides.

brew install pyenv
brew install pipenv
```

### 0.2 In case of chaos
If pyenv installation chaos on macos, export the below flags for temporarily allowing to install specific python versions. (Check this [link](https://github.com/jiansoung/issues-list/issues/13).)

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
pyenv local anaconda3-2019.03
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
pipenv --python 3.7.0
```

`Pipfile` provides the overview of the virtual environment, whilst `Pipfile.lock` provides the specification for all packages needed (including dependecnies), with corresponding versions.

```
less Pipfile
less Pipfile.lock
```

Install packages

```
pipenv install numpy bokeh
```

Install specific version of package. Will install version `1.2`, and any minor updates, but not `2.0`

```
pipenv install requests~=1.2
```

Uninstall package.

```
uninstall requests
```

Install exact version of package. Will never update.

```
pipenv install requests==1.2
```

Alternative to uninstalling a package is using clean.

```
# Delete specific package from Pipfile (requests)
# and then
pipenv clean
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
pipenv python plot_figure.py

exit
```

### Copying environment using `Pipfile.lock`

When multiple people are working on the same project, it becomes even more important that the environment is set up the same way on different local devices.
The `Pipfile.lock` file helps with that.

```
copy
```


### Update packages


```
pipenv update --outdated
```

```
pipenv update --outdated
```