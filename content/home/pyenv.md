+++
weight = 10
+++
{{% section %}}

### (Python) virtual environments

<p class="fragment fade-in-then-semi-out">
Create an isolated environment where you effectively get a "clean" python installation
</p>
<p class="fragment fade-in-then-semi-out">
<a href="https://docs.python.org/3/library/venv.html"><code>venv</code></a> module in the standard library creates virtual environments
</p>
<p class="fragment">Read the <a href="https://www.python.org/dev/peps/pep-0405/">PEP</a> for the gory details</p>


---

### (Python) virtual environments

```py
# np.py
import numpy

print(numpy.__version__)
```


```shell
$ mkdir paranoid && cd paranoid

$ vim np.py  # insert the contents from the above python snippet

$ python3 np.py
1.18.3 # i.e. whatever is installed in the system wide python

$ python3 -m venv .venv  # create new env

$ which python3  # shows the location of our system python

$ source .venv/bin/activate  # makes our new env the "active" python

$ which python3  # shows the location of our environment python

$ python3 np.py  # use our new env to run the python code
Traceback (most recent call last):
  File "np.py", line 2, in <module>
    import numpy
ModuleNotFoundError: No module named 'numpy'

$ pip install numpy==1.19.3

$ python3 np.py
1.19.3
$ deactivate
```

---

### Simple Python Version Management: pyenv

<https://github.com/pyenv/pyenv>

<img src="images/pyenv.png"  style="border: none;">


---

### pyenv

<p class="fragment fade-in-then-semi-out">
Allows you to change the <em>per-user</em> global python version
</p>
<p class="fragment fade-in-then-semi-out">
Allows you to set a <em>per-project</em> python version
</p>
<p class="fragment fade-in-then-semi-out">Ridiculously easy installation of any python version</p>
<p class="fragment">Automatic activation of virtual environments</p>

---

## Install - local

For local machine installation, refer to   
<https://github.com/pyenv/pyenv#installation>

---

## Install - cluster

```shell
$ export PYENV_INSTALL=/path/to/install/dir  # suggest NOT $HOME

$ export PYENV_ROOT=${PYENV_INSTALL}/.pyenv

$ git clone https://github.com/pyenv/pyenv.git "$PYENV_ROOT"

$ git clone https://github.com/pyenv/pyenv-virtualenv.git ${PYENV_ROOT}/plugins/pyenv-virtualenv
```

Add the following to the **end** of your shell configuration file (i.e. `~/.bashrc`)

```sh
export PYENV_INSTALL=/path/to/install/dir
export PYENV_ROOT=${PYENV_INSTALL}/.pyenv
# add pyenv to path
export PATH="$PYENV_ROOT/bin:$PATH"

if command -v pyenv 1>/dev/null 2>&1; then
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
fi
```

Log out and then back in

---

## Basic Usage

```shell
$ pyenv versions
* system (set by /home/vagrant/.pyenv/version)
$ pyenv install --list
Available versions:
  2.1.3
  2.2.3
  2.3.7
  2.4.0
  2.4.1
  ...
$ pyenv install 3.9.1
Downloading Python-3.9.1.tar.xz...
...
Installed Python-3.9.1 to /home/vagrant/.pyenv/versions/3.9.1
$ pyenv versions
* system (set by /home/vagrant/.pyenv/version)
  3.9.1
$ python -V
Python 2.7.17
$ pyenv global 3.9.1  # log out and back in
$ python -V
Python 3.9.1
```

---

## Real Usage

```shell
$ pyenv install 3.5.10

$ mkdir foo && cd foo && ls -la

$ python -V
3.9.1

$ pyenv local 3.5.10

$ python -V
3.5.10

$ ls -la
drwxrwxr-x 2 vagrant vagrant 4096 Jan 13 04:53 .
drwxrwxr-x 4 vagrant vagrant 4096 Jan 13 04:53 ..
-rw-rw-r-- 1 vagrant vagrant    7 Jan 13 04:53 .python-version

$ cat .python-version
3.5.10
```

---

## Virtual Env Usage

```shell
$ mkdir myproject && cd myproject

$ pyenv virtualenv myproject

$ pyenv versions
system
3.5.10
* 3.9.1 (set by /home/vagrant/.pyenv/version)
3.9.1/envs/myproject
myproject

$ pyenv local myproject  # or 3.9.1/envs/myproject

$ cat .python-version
myproject

$ pyenv versions
system
3.5.10
3.9.1
3.9.1/envs/myproject
* myproject (set by /home/vagrant/tmp/myproject/.python-version)

$ pip install pyjokes

$ pyjoke
There are 10 types of people: those who understand binary and those who don't.

$ cd .. && pyjoke
pyenv: pyjoke: command not found

The `pyjoke' command exists in these Python versions:
  3.9.1/envs/myproject
  myproject

Note: See 'pyenv help global' for tips on allowing both
      python2 and python3 to be found.
```

---

## Poetry

<https://python-poetry.org/>

<p class="fragment fade-in-then-semi-out">
Python packaging and dependency management
</p>

<p class="fragment fade-in-then-semi-out">
<b>Strongly</b> recommended if developing a python package
</p>


{{% /section %}}
