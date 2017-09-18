# Installation Steps - Windows

# Create a virtualenv

- download and install the latest python 3 release (python >= 3.4) from [Python Releases for Windows](https://www.python.org/downloads/windows/) page

Note: Make sure that you have the option **"Add Python to environment variables"** checked when asked during installation.

Example of python installation url:
    [python-3.5.2-amd64.exe](https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe)

- install [git-for-windows](https://git-for-windows.github.io/)

- start the "Git Bash" executable and verify that the latest version of the **pip** utility is installed

        $ pip --version
        $ python -m pip install --upgrade pip

- create a folder for storing dependencies

        $ cd ~
        $ mkdir .virtualenvs

- install the helper tool for isolating the installation files

        $ pip install virtualenv

- activate the isolation environment

        $ virtualenv ~/.virtualenvs/deduper
        $ source ~/.virtualenvs/deduper/Scripts/activate

- verify that the prompt has changed and indicates **(deduper)** as an active python environment


# Install and configure

We are using the standard python distribution model so installation should be relatively simple:

- install OneFlorida deduper package to access hash_generator script

        $ pip install deduper

- create a project folder for storing configuration files and data

        $ cd ~
        $ mkdir deduper
- enter the deduper project folder

		$ cd deduper

- create a directory for storing configuration files

        $ mkdir -p ~/deduper/config

- create a directory for storing log files

        $ mkdir -p ~/deduper/logs

- create a log config file by using the [`config/example/logs.cfg.example`](https://github.com/ufbmi/onefl-deduper/blob/master/config/example/logs.cfg.example) file as a template

        $ curl https://raw.githubusercontent.com/ufbmi/onefl-deduper/master/config/example/logs.cfg.example > config/logs.cfg

- create a config file by using the [`config/example/settings_hasher.py.example`](https://github.com/ufbmi/onefl-deduper/blob/master/config/example/settings_hasher.py.example) file as a template

        $ curl https://raw.githubusercontent.com/ufbmi/onefl-deduper/master/config/example/settings_hasher.py.example > config/settings_hasher.py

- edit the config file -- the `SALT` value

Note: we will provide the SALT to be used in production mode on request, for the initial testing it is fine to leave it empty

        $ vim ~/deduper/settings_hasher.py

- generate an example input file called `phi.csv` with the following header:
`patid`, `first`, `last`, `dob`, `sex`, `race`

Notes:

- For testing purposes you can use the example file [phi.csv](https://github.com/ufbmi/onefl-deduper/blob/master/tests/data_in/phi.csv).
- The example file uses `\t` as column separator.

        $ curl https://raw.githubusercontent.com/ufbmi/onefl-deduper/master/tests/data_in/phi.csv > phi.csv

- display the package version and run it

        $ hasher -v
        $ hasher -c ~/deduper/settings_hasher.py

    You should get some output indicating that a file was produced:

        >> Wrote output file: ./phi_hashes.csv

    The output file should have the following columns: `patid`, `F_L_D_G`, `F_L_D_R`

# Installation Steps - Windows without internet connection


1. Download the packages on a machine which *does* have internet connection:

    $ mkdir my_pypi && cd my_pypi
    $ pip download --platform=windows --only-binary=:all: virtualenv virtualenvwrapper invoke deduper

2. Transfer the `my_pypi` folder to the restricted windows environment

3. Install the packages from within the `my_pypi` folder

    $ cd C:\Users\asura\my_pypi
    $ pip install --no-index --find-links=. --root=. pbr six stevedore invoke virtualenv
    $ pip install --no-index --find-links=. --root=. deduper
