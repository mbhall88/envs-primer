+++
weight = 20
+++
{{% section %}}

## Conda

<https://conda.io>

> Package, dependency and environment management for any language—Python, R, Ruby, Lua, Scala, Java, JavaScript, C/ C++, FORTRAN, and more.

---

## Conda advantages

<p class="fragment grow">Why should I use it over virtual envs?</p>

<p class="fragment fade-in-then-semi-out">
Support for languages other than Python - it's probably more like <code>apt</code> than <code>pip</code>
</p>
<p class="fragment fade-in-then-semi-out">
You want to use newer language standards, such as C++17
</p>

<p class="fragment fade-in-then-semi-out">
Ability to install pre-compiled software - i.e. nodejs, curl etc.
</p>

<p class="fragment fade-in-then-semi-out">
<a href="https://bioconda.github.io/>">Bioconda</a> - i.e. samtools, minimap2 etc.
</p>

<p class="fragment">
You use Windows...
</p>

---

## Conda disadvantages

<p class="fragment fade-in-then-semi-out">
Not all of PyPI is available (mostly obscure packages though)
</p>

<p class="fragment fade-in-then-semi-out">
"Heavier" way of managing Python environments/packages
</p>

<p class="fragment fade-in-then-semi-out">
Dependency resolution <a href="https://github.com/bioconda/bioconda-recipes/issues/13774">can be slow</a>
</p>

<p class="fragment fade-in-then-semi-out">
More limited in Python version flexibility
</p>

<p class="fragment">
Not isolated from your OS - C compiler can sometimes cause problems (see containers in the next section)
</p>


---

## Setup

Non-`pyenv` installation can be found in [the docs](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)

Or, install with `pyenv`

```shell
$ pyenv install miniconda3-4.7.10
```


---

## Usage

```shell
$ mkdir condaproj && cd condaproj

$ pyenv local miniconda3-4.7.10
$ conda config --add channels defaults
$ conda config --add channels bioconda
$ conda config --add channels conda-forge

$ conda create --name snp_paper samtools bcftools

$ conda activate snp_paper

$ bcftools --version
bcftools 1.9
...

$ conda info --envs
# conda environments:
base                     /home/vagrant/.pyenv/versions/miniconda3-4.7.10
snp_paper             *  /home/vagrant/.pyenv/versions/miniconda3-4.7.10/envs/snp_paper

$ conda search snakemake

$ conda install snakemake=5.30.2

$ snakemake --version
5.30.2
```

Note: Channel order is **very** important

{{% /section %}}
