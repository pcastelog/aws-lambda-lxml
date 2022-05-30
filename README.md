# aws-lambda-lxml

AWS Lambda precomiled binaries for lxml built for python 2.7 and python 3.6 runtimes.

`libxml2-dev` and `libxslt-dev` are not needed as they are included by default in the machines that run lambdas.

## Example usage

1. Put the lxml directory in the root of your lambda package
1. Import lxml and use as usual

```python
from lxml import etree


def handle(event, context):
    return etree.fromstring(event)

```

## Build it yourself

The lxml library is os dependent thus we need to have precompiled copy. Below are the steps.

Create a docker container.
```docker run -it lambci/lambda:build-python3.8 bash```

Create a dir named ‘lib'(anything you want) and Install lxml into it.
mkdir lib
```pip install lxml -t ./lib --no-deps```

Open another cmd and run
```docker ps```

copy the containerid

Copy the files from container to host.
```
mkdir /home/libraries/opt/python/lib/python3.8/site-packages/
docker cp <containerid>:/var/task/lib /home/libraries/opt/python/lib/python3.8/site-packages/
```

Steps taken from https://codeutility.org/python-aws-lambda-not-importing-lxml-stack-overflow/


Once you run this, you'll have a folder called `lxml` (you can ignore the other one
with the dist-info), which is the one you are going to place in the root of the
lambda package as specified in the [example](#example-usage)
