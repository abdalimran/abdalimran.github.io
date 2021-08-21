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
mamba repoquery search <package>
{% endhighlight %}

### Searching for dependencies
{% highlight python %}
mamba repoquery depends -a <package>
{% endhighlight %}

### Creating an environment
{% highlight python %}
mamba create -n <env_name> <package>
{% endhighlight %}

### Adding/Updating software
{% highlight python %}
mamba install -n <env_name> <package>
mamba update -n <env_name> --all
{% endhighlight %}

### Removing a package
{% highlight python %}
mamba remove -n <env_name> <package>
{% endhighlight %}

### Undoing changes to an environment
{% highlight python %}
mamba list -n <env_name> --revisions
mamba install -n <env_name> --revision 1
{% endhighlight %}

### Show environment
{% highlight python %}
conda env export --no-builds
{% endhighlight %}

### Clone an existing environment
{% highlight python %}
conda create --name <clone_envname> --clone <env_name>
{% endhighlight %}

### Removing an environment
{% highlight python %}
mamba env remove -n <env_name>
conda remove --name <env_name> --all
{% endhighlight %}

### Exporting an environment
{% highlight python %}
mamba env export -n <env_name> > <env_name>.yaml
conda list -e > <env_name>.txt
{% endhighlight %}

* **Windows**: {% highlight python %}conda env export -n <env_name> | findstr -v "prefix" > <env_name>.yaml{% endhighlight %}
* **Linux**: {% highlight python %}conda env export -n <env_name> --no-builds | grep -v "prefix" > <env_name>.yaml{% endhighlight %}

### Importing an environment
{% highlight python %}
mamba env create --file <env_name>.yaml
conda env create --file <env_name>.yaml
conda create -n <env_name> --file <env_name>.txt
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