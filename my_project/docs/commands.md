# Commands

For the summary of Slurm commands please see the link - [summary](https://slurm.schedmd.com/pdfs/summary.pdf).


### Jobs

Report status of submitted job:

    $ squeue -l -u$USER
    or
    $ squeue -l -u<user-name>


Report status of submitted job every 60 seconds:

    $ squeue -i60 -l -u$USER

Details of submitted job:  

    $ scontrol show job <job-id>

The maximal memory used for the _completed_ job:  

    $ sacct -j <job-id> --format=MaxRSS

Maximal memory used for the _running_ job:

    $ sstat -j <job-id> --format=MaxRSS

To see all format options:  

    $ sacct -e
    or
    $ sstat -e


To see when the submitted job will start:

    $ squeue --start



In addition, you can use the script "jobinfo" from GitHub [slurm-util](https://github.com/birc-aeh/slurm-utils) site for monitoring your jobs. To run the script, save it in your directory and write the command:

    $ <path-to-file>/jobinfo <job-id>

### Resources

To see cluster partitioning:

    $ sinfo

More details about cluster partitioning:

    $ sinfo -Nel
    or
    $ scontrol show partition

See availible GPUs:

    $ sres

See Slurm account information:

    $ sacctmgr show <option>  

Options: "Account", "Association", "Cluster", "Configuration",
"Event", "Federation", "Problem", "QOS", "Resource", "Reservation",
"RunAwayJobs", "Stats", "Transaction", "TRES", "User", or "WCKey".  
See help for details.

### Limits

See resource limit configuration:

    $ sacctmgr show assoc_mgr

See the limit of tasks which user can run:

    $ sacctmgr show qos|grep <partition-name>


### Priority

To see how defined your QOS priority:

    $ sacctmgr list assoc user=<user-name> format=Cluster,Account,User,QOS,defaultqos


See account and fair-share parameters:

    $ sshare -l

Run the job with QOS priority privilege:

    $ sbatch --qos=<priority-user-name> <path-to-file>/<sbatch-file-name>

### Piping

Start job after <other-job> started:

    $ sbatch --depend=after:<other-job-id> <path-to-file>/<sbatch-file-name>

Start job after <other-job> ends with ok status (the options can be (ok|notok|any):

    $ sbatch --depend=afterok:<other_job_id> <path-to-file>/<sbatch-file-name>

Start after both job 77 and 79 have finished:

    $ sbatch --depend=afterok:77:79 <path-to-file>/<sbatch-file-name>
