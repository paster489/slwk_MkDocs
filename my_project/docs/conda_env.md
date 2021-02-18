# Conda Environment

Check that conda is installed

    $ conda -V

Check that conda is up to date

      $ conda update conda

Create virtual environment:

    $ conda create -n <env-name>

Create virtual environment with specific package:

    $ conda create -n <env-name> scipy

Create virtual environment with specific package version:

    $ conda create -n <env-name> python=3.7

View your environment list:

    $ conda env list

Activate your environment:

    $ conda activate <env-name>

Deactivate your environment:

    $ conda deactivate

Install tensorflow-gpu:

    $ conda activate <env-name>
    $ conda install -c anaconda tensorflow-gpu

Install ipykernel:

    $ python -m ipykernel install --user --name <env-name> --display-name "<env-name-to-display>"

List of packages installed in activated environment:

    $ conda list

List of packages installed in not activated environment:

    $ conda list -n <env-name>

Compare conda environments:

    $ conda list -n <env-name-1> --export > <file-name-1>
    $ conda list -n <env-name-2> --export > <file-name-2>
    $ diff <file-name-1> <file-name-2>

Please deactivate your environment before batch file submission.
