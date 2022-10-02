# something_for_preclass
record the problems that may be met during the completion of prehomework, please forgive that some of them are really easy 

I choose a cloud server as my development machine.

```
[root@VM-0-7-centos ~]# uname
Linux
[root@VM-0-7-centos ~]# uname -r
4.18.0-348.7.1.el8_5.x86_64
```

----git----
So follow the guide, we need install git, and I choose to build from source which is located at https://mirrors.edge.kernel.org/pub/software/scm/git/.

```
wget -c https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.4.tar.gz
tar -zxvf git-2.9.4.tar.gz
cd git-2.9.4
./configure
make
make install
```

Make sure you have 
```
yum install perl-devel
```
or you can't make it, for example: https://stackoverflow.com/questions/48931247/cant-locate-extutils-makemaker-pm-in-inc-during-git-build

Make sure you have 
```
yum install curl-devel
```
or you will unable to find remote helper for 'https', for example: https://stackoverflow.com/questions/8329485/unable-to-find-remote-helper-for-https-during-git-clone

then you get a git.

```
[root@VM-0-7-centos ~]# git --version
git version 2.9.4
```

----Anaconda----
We also need Anaconda to create a new conda environment, I also build it from source.

```
bash Anaconda3-2022.05-Linux-x86_64.sh
```

You can choose the location during the process of inatllation.

```
Anaconda3 will now be installed into this location:
/root/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/root/anaconda3] >>> 
PREFIX=/root/anaconda3
```

It is important that you'd better choose 'yes', when 

```
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
```

Because it is recommended by developers. And you can get:

```
(base) [root@VM-0-7-centos icl]# 
```

Or you have to run a command:

```
source /root/anaconda3/bin/activate
```

Please notice that 'root/anaconda3' is the PREFIX, yours may be different.

```
(base) [root@VM-0-7-centos prepython]# ls
introduction-to-python
(base) [root@VM-0-7-centos prepython]# cd introduction-to-python/
(base) [root@VM-0-7-centos introduction-to-python]# ls
environment.yml  index.ipynb  lecture1  lecture2  lecture3  lecture4  LICENSE  README.md
(base) [root@VM-0-7-centos introduction-to-python]# conda env create -f environment.yml
(base) [root@VM-0-7-centos introduction-to-python]# conda activate introduction-to-python
(introduction-to-python) [root@VM-0-7-centos introduction-to-python]# 
```

----jupterbook----

```
(introduction-to-python) [root@VM-0-7-centos introduction-to-python]# jupyter notebook &
[1] 1232803
(introduction-to-python) [root@VM-0-7-centos introduction-to-python]# [I 12:30:17.754 NotebookApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
[I 2022-09-06 12:30:18.142 LabApp] JupyterLab extension loaded from /root/anaconda3/envs/introduction-to-python/lib/python3.9/site-packages/jupyterlab
[I 2022-09-06 12:30:18.142 LabApp] JupyterLab application directory is /root/anaconda3/envs/introduction-to-python/share/jupyter/lab
[C 12:30:18.147 NotebookApp] Running as root is not recommended. Use --allow-root to bypass.
```

It is a problem I met, 'Running as root is not recommended', so I use a special command to continue my exploration.

```
jupyter notebook --allow-root &
```

Because I use a cloud server, so I need to change the config file.

```
jupyter notebook --generate-config
```

Then you will have a config file in prompt message.

What you have to change 4 as below:

```
## The port the notebook server will listen on (env: JUPYTER_PORT).
#  Default: 8888
c.NotebookApp.port = 8888

## The IP address the notebook server will listen on.
#  Default: 'localhost'
c.NotebookApp.ip = '*'

## Whether to open in a browser after starting.
#                          The specific browser used is platform dependent and
#                          determined by the python standard library `webbrowser`
#                          module, unless it is overridden using the --browser
#                          (NotebookApp.browser) configuration option.
#  Default: True
c.NotebookApp.open_browser = False

## Allow requests where the Host header doesn't point to a local server
#  
#         By default, requests get a 403 forbidden response if the 'Host' header
#         shows that the browser thinks it's on a non-local domain.
#         Setting this option to True disables this check.
#  
#         This protects against 'DNS rebinding' attacks, where a remote web server
#         serves you a page and then changes its DNS to send later requests to a
#         local IP, bypassing same-origin checks.
#  
#         Local IP addresses (such as 127.0.0.1 and ::1) are allowed as local,
#         along with hostnames configured in local_hostnames.
#  Default: False
c.NotebookApp.allow_remote_access = True
```

then you can use the link with token at any browser in any place open your jupyter notebook. 

I upload my answer here, the code all passed oktest.
Some of them fail the pybryt test:
1.15 1.18
2.2 2.10 2.11 2.12
4.1 4.4 4.9
