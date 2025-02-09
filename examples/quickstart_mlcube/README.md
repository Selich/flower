# Flower Example using TensorFlow/Keras + MLCube

**Status: experimental**

This introductory example to Flower uses MLCube together with Keras but deep knowledge of Keras is not necessarily required to run the example. However, it will help you understanding how to adapt Flower to your use-cases with MLCube.
Running this example in itself is quite easy.

## Project Setup

Start by cloning the example project. We prepared a single-line command that you can copy into your shell which will checkout the example for you:

```shell
git clone --depth=1 https://github.com/adap/flower.git && mv flower/examples/quickstart_mlcube . && rm -rf flower && cd quickstart_mlcube
```

Project dependencies (such as `tensorflow` and `flwr`) are defined in `pyproject.toml`. We recommend [Poetry](https://python-poetry.org/docs/) to install those dependencies and manage your virtual environment ([Poetry installation](https://python-poetry.org/docs/#installation)), but feel free to use a different way of installing dependencies and managing virtual environments if you have other preferences.

```shell
poetry install
poetry shell
```

Poetry will install all your dependencies in a newly created virtual environment. To verify that everything works correctly you can run the following command:

```shell
poetry run python3 -c "import flwr"
```

For the MLCube setup you will need to install Docker on your system. Please refer to the [Docker install guide](https://docs.docker.com/get-docker/) on how to do that.

If you don't see any errors you're good to go!

## MLCube setup

For the MLCube setup we have prepared a script which you can execute in your shell using:

```shell
./dev/setup.sh
```

# Run Federated Learning with TensorFlow/Keras in MLCube with Flower

Afterwards you are ready to start the Flower server as well as the clients. You can simply start the server in a terminal as follows:

```shell
./dev/server.sh
```

Now you are ready to start the clients. We have prepared a simple script called `client.sh` which accepts a CLIENT_ID and can be execute as in:

```shell
# Shell 1
./client.sh 1
```


```shell
# Shell 2
./client.sh 2
```

Congrats! You have just run a Federated Learning experiment using TensorFlow/Keras in MLCube using Flower for federation.

# Background

Wondering how this works? Most of the interaction with MLCube happens in `mlcube_utils.py` which reads and writes to the file system. It also provides a function called `run_task` which invokes `mlcube_docker run ...` to execute the appropriate task. The custom client we have implemented in `client.py` will run the MLCube 'download' task when its instantiated. fit and evaluate also interface through the `mlcube_utils.py` helpers for reading and writing to disk and calling the appropriate MLCube tasks.
