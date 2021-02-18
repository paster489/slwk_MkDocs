# SBATCH
  The syntax for the SLURM directive in a script is  "<span style="color:purple">#SBATCH</span> < flag >".  Some of the flags are used with the srun and salloc commands, as well as the fisbatch wrapper script for interactive jobs. Sbatch configuration parameters must start with #SBATCH and must precede any other command.
  <span style="color:purple">#SBATCH</span> - Bash "sees" this as comment.<br/>
  <span style="color:purple">#SBATCH</span> - Slurm "takes" this as parameter.   
  Use ## to close <span style="color:purple">#SBATCH</span> as comment.<br/>


### Example of SBatch Submition Script (Batch File):

  **NOTE**: the term "Batch File" is used throughout this documentation to mean an executable file that you create and submit to the job scheduler to run on a node or collection of nodes.  This script will include a list of Slurm directives (or commands) to tell the job scheduler what to do.  

  ![Screenshot](img/sbatch_example.png)

### Additional Flags' Description

| **Flag** <div style="width:350px">property</div> | **Description** <div style="width:100px">property</div> | **Default** |
|:----------------|:-------------|:---------------|
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">partition</span>=<ins>TBD</ins> | Partition name.  | <ins>TBD</ins> |  
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">time</span>=0-12:00:00 | Limit the time of job running. Format: D-H:MM:SS.  | <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">job-name</span>=my_job | Name of the job. Replace my_job with your desired job name. | |   
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">output</span>=%a_my_name-%J.out| Output log for running job, %J – job #, %a – run #.| |    
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">mail-user</span>=username@post.bgu.ac.il| Users email for sending job status notifications.| |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">mail-type</span>=BEGIN,END,FAIL| Conditions when to send the email. ALL,BEGIN,END,FAIL, REQUEU, NONE.| |  
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">nodelist</span>=<ins>TBD</ins>  | Specify the computer to run the job. | <ins>TBD</ins> |  
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">array</span>=1-10  | Run parallel 10 times. | <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">mem</span>=72G  | Allocate extra memory. | <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">gres</span>=gpu:1  | Number of GPUs (can't exceed 8 gpus for now) ask for more than 1 only if you can parallelize your code for multi GPU. | <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">nodes</span>=1-1 | Allocate 1 node. | <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">ntasks</span>=12  |Allocate 12 tasks| <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">cpus-per-task</span>=32  |Allocate extra CPU: 32 CPU per task.| <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">requeue</span>=32  |Re-run the task if it was preempted.| <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">dependency</span>=after(ok/notok/any):<job_ids>  |Ordering of jobs.| <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> --<span style="color:red">exclusive</span>=<user>  |To reserve a whole node for yourself, slurm will reserve a full node for the first job to start in the array, and then will schedule all the others on the same machine as only your jobs will be allowed there.| <ins>TBD</ins> |
| | | |
| <span style="color:purple">#SBATCH</span> <span style="color:red">%j</span>  |Job #.| |
| | | |
| <span style="color:purple">#SBATCH</span> <span style="color:red">%A</span>  |Value of SLURM_ARRAY_JOB_ID.| |
| | | |
| <span style="color:purple">#SBATCH</span> <span style="color:red">%a</span>  |Value of SLURM_ARRAY_TASK_ID.| |

<br/>


### Submit Job

    $ sbatch <path-to-file>/<sbatch-file-name>

If you have QOS privileges, you can use:

    $ sbatch --qos=<priority-user-name> <path-to-file>/<sbatch-file-name>

After job submission, Slurm gives the JobID, to see it use:

    $ ls -lrt

### Cancel Job
Cancel the specific job:

    $ scancel <job-id>
or

    $ scancel --name <job-name>  

Cancel all jobs of the user:

    $ scancel -u<user-name>
    or
    $ scancel -u$USER


Cancel pending jobs of the user:

    $ scancel -t PENDING -u <user-name>


### View Job ID and it's Status

    $ squeue -l -u$USER  
or  

    $ squeue -l -u<user-name>  

For codes of job state description please use:

    $ man squeue

Some of them are:  

   * R  - running  
   * PD - pending    
   * CA - canceled  
   * CD - completed  
   * F  - failed  
