# Project to analyze and model Traum-Ferienwohnungen's data

this repo has to notebooks and other materials we used to analyze and model Traum-Ferienwohnungen's data

Data used was provided by TFW, and is not to be disclosed.

The EDA folder contains notebooks used for various aspects of the EDA

The Modeling folder contains code used to develop our models. 



## Requirements and Setup

Use the requirements file in this repo to create a new environment.

```BASH
make setup

#or

pyenv local 3.8.5
python -m venv .venv
pip install --upgrade pip
pip install -r requirements_dev.txt
```

The requirements.txt file contains the libraries needed for running the notebooks and MLFlow.

### Notes on MLFlow

The MLFLOW URI should not be stored on git, you have two options, to save it locally in the .mlflow_uri file:

```BASH
echo http://127.0.0.1:5000/ > .mlflow_uri
```

this will create a local file where the uri is stored. Alternatively you can export it as an environment variable with

```bash
export MLFLOW_URI=http://127.0.0.1:5000/
```

This links to your local mlflow, if you want to use a different one, then change the set uri.

The code in the [config.py](modeling/config.py) will try to read it locally and if the file doesn't exist will look in the env var.. IF that is not set the URI will be empty in your code.

#### Creating an MLFlow experiment

You can do it via the GUI or via [command line](https://www.mlflow.org/docs/latest/tracking.html#managing-experiments-and-runs-with-the-tracking-service-api) if you use the local mlflow:

```bash
mlflow experiments create --experiment-name 0-template-ds-modeling
```

Check your local mlflow

```bash
mlflow ui
```

and open the link [http://127.0.0.1:5000](http://127.0.0.1:5000)

This will throw an error if the experiment already exists. Save the experiment name in the [config file](modeling/config.py)

In order to train the model and store test data in the data folder and the model in models run:

```bash
#activate env
source .venv/bin/activate

python -m modeling.train
```

In order to test that predict works on a test set you created run:

```bash
python modeling/predict.py models/linear data/X_test.csv data/y_test.csv
```


