---
layout: post
title: Conda and Mamba Commands for Managing Virtual Environments
category: Data Science
---

### Installing Mamba
{% highlight python %}
conda install -n base -c conda-forge mamba
{% endhighlight %}

### Adding channels
{% highlight python %}
conda config --add channels conda-forge
{% endhighlight %}

### Updating Mamba
{% highlight python %}
mamba update -n base mamba
{% endhighlight %}

### Finding a Package
{% highlight python %}
mamba repoquery search PACKAGE
{% endhighlight %}

### Searching for dependencies
{% highlight python %}
mamba repoquery depends -a PACKAGE
{% endhighlight %}

### Creating an environment
{% highlight python %}
mamba create -n ENV_NAME PACKAGE
{% endhighlight %}

### Adding/Updating software
{% highlight python %}
mamba install -n ENV_NAME PACKAGE
mamba update -n ENV_NAME --all
{% endhighlight %}

### Removing a package
{% highlight python %}
mamba remove -n ENV_NAME PACKAGE
{% endhighlight %}

### Undoing changes to an environment
{% highlight python %}
mamba list -n ENV_NAME --revisions
mamba install -n ENV_NAME --revision 1
{% endhighlight %}

### Show environment
{% highlight python %}
conda env export --no-builds
{% endhighlight %}

### Clone an existing environment
{% highlight python %}
conda create --name CLONE_ENV_NAME --clone ENV_NAME
{% endhighlight %}

### Removing an environment
{% highlight python %}
mamba env remove -n ENV_NAME
conda remove --name ENV_NAME --all
{% endhighlight %}

### Exporting an environment
{% highlight python %}
mamba env export -n ENV_NAME > ENV_NAME.yaml
conda list -e > ENV_NAME.txt
{% endhighlight %}

* **Windows**: {% highlight python %}conda env export -n ENV_NAME | findstr -v "prefix" > ENV_NAME.yaml{% endhighlight %}
* **Linux**: {% highlight python %}conda env export -n ENV_NAME --no-builds | grep -v "prefix" > ENV_NAME.yaml{% endhighlight %}

### Importing an environment
{% highlight python %}
mamba env create --file ENV_NAME.yaml
conda env create --file ENV_NAME.yaml
conda create -n ENV_NAME --file ENV_NAME.txt
{% endhighlight %}

### Deactivate the Environment
{% highlight python %}
conda deactivate
{% endhighlight %}

### Viewing a list of your environments
{% highlight python %}
conda info --envs
conda env list
{% endhighlight %}