sudo service postgresql start

sudo service postgresql status

conda env create -f mimic-extract-new.yml

conda activate mimic_data_extraction

psql -U postgres -d mimic -h localhost -c "SET search_path TO mimiciii,public;" -f postgres-functions.sql
