+++
weight = 30
+++
{{% section %}}

# Containers



<p class="fragment fade-in-then-semi-out">A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. That includes: files, environment variables, dependencies and libraries</p>

<p class="fragment"><b>Gold-standard for reproducibility</b></p>

<a href="https://www.docker.com/"><img src="images/docker.png" height="200" style="border: none;"></a>
<a href="https://sylabs.io/"><img src="images/singularity.png" height="200" style="border: none;"></a>

---

For those who would like more detailed information about what containers are, please refer to [this fantastic slide deck from Josep Moscardo](https://github.com/titansmc/singularity-training-2019/raw/master/1.-singularity-training-what-are-containers.odp).

---

# [Singularity](https://sylabs.io)

<p class="fragment fade-in-then-semi-out">Much easier to use than Docker</p>
<p class="fragment fade-in-then-semi-out">Can seamlessly use Docker images</p>
<p class="fragment fade-in-then-semi-out">We have it on the cluster</p>
<p class="fragment">Supported by major workflow management systems</p>

---

## What can I do with a container?

In it's most basic form, you can execute a software program, via a container, even though you may not have that program installed on the system you are running it on.

---

## Example on EBI cluster

```shell
$ module load singularity/3.5.0

$ wget https://github.com/mbhall88/eipp-2019-singularity/raw/master/data/toy.bam

$ img="docker://quay.io/biocontainers/samtools:1.9--h10a08f8_12"

$ singularity -s exec "$img" samtools view -h toy.bam
```


<p class="fragment fade-in-then-semi-out"><a href="https://sylabs.io/guides/3.5/user-guide/quick_start.html#executing-commands"><code>singularity -s exec</code></a> tells Singularity to execute a given command inside a
    given container (and only print errors).</p>
<p class="fragment fade-in-then-semi-out"><code>"$img"</code> specifies the container for Singularity to operate on. We will look at this component in more detail soon.</p>
<p class="fragment"><code>samtools view -h data/toy.bam</code> is the command we want Singularity to execute inside the container. Notice how we can specify files that exist on our local file system?!</p>

---

## How do I get a container image?

<p class="fragment fade-in-then-semi-out">Remote container registries</p>
<p class="fragment fade-in-then-semi-out">Build one locally</p>
<p class="fragment">See <a href="https://github.com/mbhall88/eipp-2019-singularity#how-do-i-get-a-container">this tutorial</a> I ran for some predocs for a more detailed explanation of the above options</p>

---

# BioContainers

<https://biocontainers.pro>

BioContainers is a project that provides the infrastructure and basic guidelines to create, manage and distribute bioinformatics packages (e.g conda) and containers (e.g docker, singularity). BioContainers is based on the popular frameworks Conda, Docker and Singularity.


---

### Retrieving a Biocontainer

All Bioconda packages automagically get a Biocontainer built on <https://quay.io>

<img src="images/quay-search-ggplot.png" height="300" style="border: none;">
<img src="images/quay-search-spades.png" height="300" style="border: none;">


---

### Retrieving a Biocontainer

<img src="images/quay-search-bwa.png" height="500" style="border: none;">

---

### Retrieving a Biocontainer

<img src="images/quay-tag.png" height="400" style="border: none;">

<pre class="bash"><code data-trim>
tool="bwa"
tag="0.7.3a--h84994c4_4"
URI="docker://quay.io/biocontainers/${tool}:${tag}"
</code></pre>

{{% /section %}}
