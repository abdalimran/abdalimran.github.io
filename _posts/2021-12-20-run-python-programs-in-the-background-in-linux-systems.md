---
layout: post
title: Run python programs in the background in Linux Systems
category: 
    - "Development"
---

Firstly, you need to add the [shebang line](https://en.wikipedia.org/wiki/Shebang_(Unix)) in the Python script which looks like the following:

```shell
#!/usr/bin/env python3
```
    
This path is necessary if you have multiple versions of Python installed and `/usr/bin/env` will ensure that the first Python interpreter in your `$$PATH` environment variable is taken. You can also hardcode the path of your Python interpreter (e.g. `#!/usr/bin/python3`), but this is not flexible and not portable on other machines. Next, you'll need to set the permissions of the file to allow execution:

```shell
chmod +x test.py
```
    
Now you can create a new session with `setsid` and run the script with [nohup](https://en.wikipedia.org/wiki/Nohup) which ignores the hangup signal. This means that you can close the terminal without stopping the execution. Also, don't forget to add `&` so the script runs in the background. `setsid` is used to run a program in a new session.

```shell
setsid nohup /path/to/test.py &
```
    
If you did not add a shebang to the file you can instead run the script with this command:

```shell
nohup python /path/to/test.py &
```
    
The output will be saved in the `nohup.out` file, unless you specify the output file like here:

```shell
setsid nohup /path/to/test.py > output.log &
setsid nohup python /path/to/test.py > output.log &
```

You can find the process and its process Id with this command:

```shell
ps ax | grep test.py
```
    
If you want to stop the execution, you can kill it with the [kill](https://en.wikipedia.org/wiki/Kill_(command)) command:

```shell
kill -9 PID
```
    
    
## Output Buffering    
    
If you check the output file `nohup.out` during execution you might notice that the outputs are not written into this file until the execution is finished. This happens because of output buffering. If you add the `-u` flag you can avoid output buffering like this:

```shell
setsid nohup python -u ./test.py &
```
    
Or by specifying a log file:

```shell
setsid nohup python -u ./test.py > output.log &
```
