# Jupyter Notebook


## Launching RStudio

* Navigate to the Interactive Apps section.
* Select RStudio from the list of available applications.

## Loading the R Environment

* By default, `R 4.2.2` is loaded. If you want to use this version, you can proceed without any additional commands.
* To use a different version or environment, enter the necessary commands:
For example, to use a Conda environment, enter:
`module load Anaconda3/2023.09-0; source conda.sh; conda activate my_conda_r_env`
* To use a different R environment, enter the following commands: `module load GCC/11.2.0 OpenMPI/4.1.1 R/4.2.0`

## Configuring Resources

* Specify your Slurm account/partition/qos.
* Set the maximum wall time requested.
* Choose the number of cores you need.
* If required, specify the number of GPUs.

![Rstudio1](../../assets/ondemand/Rstudio1.png)

![Rstudio2](../../assets/ondemand/Rstudio2.png)

![Rstudio3](../../assets/ondemand/Rstudio3.png)

![Rstudio4](../../assets/ondemand/Rstudio4.png)

![Rstudio5](../../assets/ondemand/Rstudio5.png)