# How to easily update your tool?

You will want to create two scripts, at least:

- One to update your tool on prod: [update-YOUR_TOOL.sh](https://github.com/Clinical-Genomics/servers/resources/update-TEMPLATE-prod.sh)
- One to update your tool on stage: [update-YOUR_TOOL-stage.sh](https://github.com/Clinical-Genomics/servers/resources/update-TEMPLATE-stage.sh)

## Stage CLI update script

Start from the templetes above. Copy to the server-folder where it should be used and rename it according to the naming convention above. 
Replace the word `YOUR_TOOL` with your tool in the file name.
Within the script replace the word `tool` and `server.scilifelab.se` with relevant names e.g. `cg`
 and `hasta.scilifelab.se`

Update stage to a specific branch:
```bash
cd ~/servers/resources/hasta.scilifelab.se
sh update-cg-stage.sh beta
```

### Web update script

For web frontend, one can add everything you need to update a staging env:

```bash
#!/usr/bin/env bash

# exit on error
set -e

# make sure we run as hiseq.clinical
sh ./assert_user.sh hiseq.clinical

# make sure we run on clinical-db
sh ./assert_host.sh clinical-db.scilifelab.se

# One optional argument, prefilled
BRANCH=${1-master}

# make sure we can have access to aliases
shopt -s expand_aliases

# make sure we are closely resembling production
source ~/.bashrc

# go to stage. Yes, this conda env should already exist
source activate stage

# trailblazer-stage is already installed in a predefined location. The repo should already be cloned
cd ~/STAGE/trailblazer
 
# Update!
git fetch
git checkout $BRANCH
git pull

# install and update pip dependencies
pip install -U --editable .

# restart the Flask service
supervisorctl restart trailblazer-stage
supervisorctl restart trailblazer-api-stage

# Drop you back to the initial directory
cd -
```

## Naming of scripts

The suggestion is to name your script: `update-$component-stage.sh`

with $component the name of your component, be it `trailblazer` for the cli or `trailblazer-ui` for the web.

## What about config files?

Premade config files for all packages used in production and stage have been made in the `config` dir of the servers repo. This can be found on hasta and clinical-db in the same location:

```
cd ~/servers/config
```

All config files point to the stage location of the package, if any, to lims-stage, and to the staging databases.

## What about databases?

### MySQL

All databases are located on clinical-db. To make sure you have the latest uncorrupted data, you can make a copy of one or all databases like this:

On clinical-db, copying all databases:
```
cd ~/servers/resources
bash dbcopy-prod-to-stage.sh all
```

On clinical-db, copy one database:
```
cd ~/servers/resources
bash dbcopy-prod-to-stage.sh trailblazer
```

The credentials to the stage databases have already been set in the stage configs.

### Mongo

All mongodbs are located on clinical-db. To copy both scout and loqusdb, you can issue:

```
cd ~/servers/resources
bash dbcopy-mongoprod-to-stage.sh
```

This will reinstate a backuped version of scout (dated: 2018-05-18) and a fresh copy of loqusdb.

Please be aware that this process takes several days to complete!

The mongo-stage server is not running by default. To start the mongo-stage run:

```
cd ~/servers/resources
bash start-mongo-stage.sh &
```
