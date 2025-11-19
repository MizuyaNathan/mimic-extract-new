# Running Instruction

## Step 0: Required software and prereqs

Your local system should have the following executables on the PATH:

* conda
* psql (PostgreSQL 9.4 or higher)
* git
* MIMIC-iii psql relational database (Refer to [MIT-LCP Repo](https://github.com/MIT-LCP/mimic-code))
* [MIMIC-iii dataset](https://physionet.org/content/mimiciii/1.4/)

## Step 1: Create conda environment
Please create in WSL!!!

Next, make a new conda environment from [mimic_extract_env_py36.yml](../mimic_extract_env_py36.yml) and
activate that environment.

```
conda env create --force -f ../mimic_extract_new.yml
```

This step will _report failure on the pip installation stage_. This is not the end of the world. Instead,
simply activate the environment (which should work despite the former "failure"):

```
conda activate mimic_data_extraction
```

And then install any failed packages with pip (e.g., `pip install [package]`). This may include, in
particular, packages: `scispacy`, `matplotlib`, `datapackage` and `scispacy`.
You will also then need to install the english language model for spacy, via:
`python -m spacy download en_core_web_sm`

#### Expected Outcome

The desired enviroment will be created and activated.

## Step 2: load data into psql
1. Use below command to start psql server in your WSL terminal

`sudo service postgresql start`

2. Clone [MIT-LCP Repo](https://github.com/MIT-LCP/mimic-code) and run the scripts in `mimic-iii/buildmimic` and `mimic-iii/concepts_postgres` folders to load data and build concepts in psql.

## step 3: generate data
1. cd into utils folder and then run postgres_make_extended_concepts.sh

2. run setup_user_env.sh to export the env variables, feel free to change based on your configuration

3. run build_curated_from_psql.sh to generate data into `data/curated` folder

# Commands
sudo service postgresql start

sudo service postgresql status

conda env create -f mimic-extract-new.yml

conda activate mimic_data_extraction

psql -U postgres -d mimic -h localhost -c "SET search_path TO mimiciii,public;" -f postgres-functions.sql

bash build_curated_from_psql.sh
