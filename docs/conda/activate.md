# Activate conda envs

After you have created a conda environment, conda tells you the following:

```
#
# To activate this environment, use:
# > source activate D_mkdocs
#
# To deactivate this environment, use:
# > source deactivate D_mkdocs
#
```

## Production and stage

We have two special conda environments with special configurations: production, called `P_main` and stage, called `S_main`.

`P_main` is the main environment in which not surprisingly, our production tools are running. `S_main` is a recent copy of `P_main` used for testing of your latest feature branch and to test deployment.

What is so special about `P_main` or `S_main`? They come with all tools already pointing to their configurations and need to be activated using a shell script.

To activate `P_main` environment, type:
```
up
```
or
```
useprod
```

To activate `S_main` environment, type:
```
us
```
or
```
usestage
```

### I want to know more

`us` and `usestage` are aliases pointing to a script:

```
alias usestage='source ${HOME}/servers/resources/usestage.sh'
```
