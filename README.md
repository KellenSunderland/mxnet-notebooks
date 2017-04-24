# MXNet Notebooks

This repo contains various notebooks ranging from basic usages of MXNet to
state-of-the-art deep learning applications.

## How to use

### Python

The python notebooks are written in [Jupyter](http://jupyter.org/).

- **View** We can view the notebooks on either
  [github](https://github.com/dmlc/mxnet-notebooks/blob/master/python/outline.ipynb)
  or
  [nbviewer](http://nbviewer.jupyter.org/github/dmlc/mxnet-notebooks/blob/master/python/outline.ipynb). But
  note that the former may be failed to render a page, while the latter has
  delays to view the recent changes.

- **Run** We can run and modify these notebooks if both [mxnet](http://mxnet.io/get_started/index.html#setup-and-installation) and [jupyter](http://jupyter.org/) are
  installed. Here is an [example script](https://gist.github.com/mli/b64322f446b2043e3350ddcbfa5957be) to install all these packages on Ubuntu.

  If you have a AWS account, here is an easier way to run the notebooks:

  1.  Launch a p2.xlarge instance by using AMI `ami-6e5d6808` on Ireland (eu-west-1). The Deep Learning AMI v2.0 for Amazon Linux is designed to continue to provide a stable, secure, and high performance execution environment for deep learning applications running on Amazon EC2.

#### Linux and OSX Users:
  2.  Once launch has succeeded we'll setup a few variables with the proper hostnames, and then connect via SSH.  At the same time we'll enable port 8888 to be tunneled over our connection so that we can eventually access our jupyter notebooks with a local browser.

    ```bash
      export HOSTNAME=ec2-107-22-159-132.compute-1.amazonaws.com
      export PERM=~/Downloads/my.pem
      chmod 400 $PERM
      ssh -i $PERM -L 8888:localhost:8888 ec2-user@HOSTNAME
    ```
    
#### Windows Users:
  2.  Unfortunately getting connected with Windows requires a few additional steps.  You'll need to install Putty and then follow two sections of [this guide](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html).  First follow the 'Converting Your Private Key Using PuTTYgen' and then follow the 'Starting a PuTTY Session' section.  **Important**:  Before opening a connection there's one last setting to set which will allow you to connect locally to your jupyter notebook. Open the setting under Connection->SSH->Tunnels and add a tunnel from source port 8888 to local port 8888.  Now you can proceed to connect and get a shell the the EC2 instance.

   4. Clone this repo on the EC2 machine and run jupyter

      ```bash
        sudo yum install -y graphviz
        sudo mkdir /efs
        sudo chown ec2-user:ec2-user /efs
        cd /efs
        git clone https://github.com/dmlc/mxnet-notebooks
        jupyter notebook
      ```
   	  Leave this ssh session open and connected while using the python notebooks.

   5. Now we are able to view and edit the notebooks on the browser using the URL: http://localhost:8888/tree/mxnet-notebooks/python/outline.ipynb

   6. Finally you may want to connect another ssh session and run the following command to keep track of GPU memory and core usage
        ```bash
        ssh -i $PERM ec2-user@$HOSTNAME
        watch -n 1 nvidia-smi
        ```
## How to develop

Some general guidelines

- A notebook covers a single concept or application
- Try to be as basic as possible. Put advanced usages at the end, and allow reader to skip it.
- Keep the cell outputs on the notebooks so that readers can see the results without running
