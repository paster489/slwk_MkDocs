# Jupyter

### Instaltion

Check that <span style="color:red">python</span>, <span style="color:red">ipython</span>,
<span style="color:red">ipykernel</span> (interactive python shell used for Jupyter kernel) and <span style="color:red">jupyterlab</span> packages are installed in your environment (see Conda Environment section for details about the installation).

### Batch File Submission

Submit Batch File with the next executions in the end of the file:     

      module load anaconda
      source activate <env-name> running the job
      jupyter lab

### URL for Jupyter web access

After the job was successfully submitted and has the status of running, wait for 1 minute and then open output log file of the job and copy 2<sup>nd</sup>  token: `https://132/72.x.x.` and paste it into your web browser’s address bar. In the open Jupyter notebook check that the correct environment name is chosen (upper right corner).
