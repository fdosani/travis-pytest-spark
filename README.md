# travis-pytest-spark

A Minimal setup of tests (using `pytest`) with `pyspark`.

The tests just creates a simple Spark DataFrame and assets things on it.
The main portion is the Travis CI setup located in the `.travis.yml` file.

The key section is as follows:

```yaml
before_install:
  - mkdir -p /opt
  - wget -q -O /opt/spark.tgz http://www.gtlib.gatech.edu/pub/apache/spark/spark-2.4.3/spark-2.4.3-bin-hadoop2.7.tgz
  - tar xzf /opt/spark.tgz -C /opt/
  - rm /opt/spark.tgz
  - export SPARK_HOME=/opt/spark-2.4.3-bin-hadoop2.7
  - export PATH=$PATH:/opt/spark-2.4.3-bin-hadoop2.7/bin
```

Setting up `SPARK_HOME` environment variable allows pytest-spark
to find the Spark JARs and actually execute a standalone Spark
instance.


## Running locally
You will need Spark install on your machine with it in your `PATH` and also its
location set under `SPARK_HOME` (for pytest)

```bash
# create env
conda create -n travis-spark python=3.6

# clone and go to folder`
git clone https://github.com/fdosani/travis-pytest-spark.git`
cd travis-pytest-spark

# install deps
pip install -r requirements.txt

#run tests
pytest
```
