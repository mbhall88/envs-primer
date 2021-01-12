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

### `venv` example

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
    import numpy as np
ModuleNotFoundError: No module named 'numpy'
```

So we have a clean python environment with no packages (aside from the standard library)

```shell
$ pip install numpy==1.19.5
$ python3 np.py
1.19.5
```

{{% /section %}}
