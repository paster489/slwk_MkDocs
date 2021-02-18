# SGE HPC only: RStudio and sgejobs

Sgejobs is R-program which creates bash script for job submission in HPC.
For more details about sgejobs see the link [Introduction to sgejobs](http://research.libd.org/sgejobs/articles/basics.html).

### Open Rstuio

From any sge you can run the next commands:

    $ firefox
    $ http://172.20.0.212:8787 or http://sge212:8787


### Create bash script (with sgejobs)

Create R-script which is shown below and run it in sge212 (here R-code is written in notepad, but you any other editor as well):

    #!/usr/bin/env Rscript  
    library('sgejobs')  
    job_single(name = <job-name.R>, create_shell = TRUE, task_num = <number-of-running>)

For more complicated examples, please, see the link [Introduction to sgejobs](http://research.libd.org/sgejobs/articles/basics.html).

The output of the script will be bash file **<job-name.R\>.sh** .

### Update bash script

Update **<job-name.R\>.sh** bash script with the next changes.

1.Close the next lines as comments (double #):

 * \##$ -tc 20    
 * \##module load conda_R    
 *  \##module list  

2.Update the line after "## List current modules for reproducibility" with the next command:

* Rscript <job-name.R\>   

This command "says" to bash to run <job-name.R\> as R-code. If you are using Python, you need to replace Rscript with Python word.
This mode of operation allow to submit the job in batch mode and is not interactive run.
If you need the interactive run, please contact HPC team for support.

In addition, you can update the resources which are need to run your job **<job-name.R\>**:

    #!/bin/bash
    #$ -cwd
    #$ -l mem_free=10G,h_vmem=10G,h_fsize=100G
    #$ -N R_test.R
    #$ -o logs/R_test_R.$TASK_ID.txt
    #$ -e logs/R_test_R.$TASK_ID.txt
    #$ -m e
    #$ -t <number-of-running>
    ##$ -tc 20

    echo "**** Job starts ****"
    date

    echo "**** JHPCE info ****"
    echo "User: ${USER}"
    echo "Job id: ${JOB_ID}"
    echo "Job name: ${JOB_NAME}"
    echo "Hostname: ${HOSTNAME}"
    echo "Task id: ${SGE_TASK_ID}"

    ## Load the R module (absent since the JHPCE upgrade to CentOS v7)
    ## module load conda_R

    ## List current modules for reproducibility
    ## module list

    ## Edit with your job command
    Rscript <job-name.R>

    echo "**** Job ends ****"
    date

    ## This script was made using sgejobs version 0.99.1
    ## available from http://research.libd.org/sgejobs/

### Submit bash script

Submit <job-name.R\>.sh bash script using the next commands:

| **Option** <div style="width:200px"> | **Code** <div style="width:300px">|
|:----|:---------------|
| | |
|  1 - without order definition| qsub <job-name.R\>.sh |  
| | |
|  2 - with order definition | qsub <job-name.R\>.sh -q <order-name\>|
| | |  

<br/>
### Delete job

    qdel <job-id>

### Log files location

All error and output files are in current directory (cwd from where the bash script was submitted) -> in log directory.
