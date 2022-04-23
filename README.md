#### AWS cluster setup

---

##### Apache Spark

---

Spark can use data stored in a variety of formats:
- HDFS,
- Cassandra,
- AWS S3,
- ...


Resilient Distributed Dataset (RDD)
- distributed collection of data,
- fault-tolerant,
- parallel operation - partioned,
- ability to use many daa sources.

<br>

#### Mac/Linux setup

---

Visit [aws website](https://aws.amazon.com/free)

```
[aws-free-tier]
account="Create a Free Account"
email=<your_address>
new_user="I am a new user"
```

**Amazon EC2**, **750 hours** per month for free (w/ t2.micro instance usage)

```
[profile-information]
# contact, billing info, ID, free support plan.
```

<br>

#### AWS EC2 setup

---

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides compute
capacity in the cloud.

1. Create EC2 instance,
2. SSH to connect to EC2 remotely,
3. SetUp Java, Scala, Spark, Jupyter on EC2.

```
[aws-amazon]
# afer signing up
login="Sign In to the Console"
service="Compute[EC2]"
setup_instance="Launch Instance"
amazon_machine_image="Ubuntu"  # Free for eligible
instance_type="t2.micro"       # Free for eligible

[instance_details]
number_of_instance=1           # Free for eligible

[storage]
size=8

[tag_instance]
key=<your_tag>
value=<your_value>

[security_group]
type="all_traffic"             # only for the educational purposes

[create-a-new-key-pair]
key_pair_name=<keyname>
```

**Download Key Pair** this option would not be available later! You need to
get the `.pem` file.


After finishing your work with your instance, you should **terminate**
the instance.

<br>

#### PySpark setup in the AWS instance

---

```
[anaconda-setup]
# wget URL

[anaconda-installation]
location="/home/ubuntu/anaconda3"

[prepending PATH]
PATH="/home/ubuntu/.bashrc"

[python-env]
# setup up-to-date version Python (not the default version)
source .bashrc

which python
# /home/ubuntu/anaconda3/bin/python

[jupyter-notebook]
# generate config file
jupyter notebook --generate-config
# Writing default config to ...

# create DIR for the cert
mkdir certs && cd certs
sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
```

Edit the Jupyter configuration file created before:
```
cd ~/.jupyter/
vi jupyter_notebook_config.py

c = get_config()
c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem'
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888
```

Run the notebook:
```
jupyter notebook
```

Check the browser:
```
https://ec2-...aws.amazon.com:8888  # /w Public DNS
```

PySpark installation:
```
sudo apt-get update -y

[Java-installation]
sudo apt-get install -y default-jre

$ java -version
# java version ...

[Scala-installation]
sudo apt-get install -y scala

$ scala -version
# Scala code runner version ...

[spark-installation]
# setup PATH for the conda binary file
export PATH=$PATH:$HOME/anaconda3/bin
conda install pip

$ which pip
# /home/ubuntu/anaconda3/bin/pip

$ pip install py4j

$ wget http://archive.apache.org/dist/spark/spark-2.0.0/spark-2.0.0-bin-hadoop2.7.tgz
$ sudo tar -zxvf spark-2.0.0-bin-hadoop2.7.tgz

$ export SPARK_HOME='/home/ubuntu/spark-2.0.0-bin-hadoop2.7'
$ export PATH=$SPARK_HOME:$PATH
$ export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
```

In the Jupyter notebook run in the column:
```python
from pyspark import SparkContent

sc = SparkContent()
```

<br>

#### Closing the AWS instance

---

In your browser:
```
[aws-instances]
Actions="Terminate"
```

