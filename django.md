# Django

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents

* [Model-View-Controller (MVC)](#model-view-controller-mvc)
* [Django MTV](#django-mtv)
* [Development Environment](#development-environment)
* [Creating a Django Project](#creating-a-project)
---
<br>

## Model-View-Controller (MVC)

MVC is a pattern for separating concerns regarding the data of a system and the user interface for that same system.

#### Model
* is the database layer
* process and manipulates any data from DB
* saves and validates data from the end-user

#### View
* is the presentation layer
* presents the output of the application to the end-user

#### Controller
* joins model and view
* process requests from the user to call the model layer as needed
* it does logic as needed on the data return from either the user or the model
* tells the view to render the collection of data

<div align="right">

[↥ back to top](#django)

</div>
<br>

## Django MTV
#### Model
* the data access layer
* matches the model in MVC

#### Template
* the presentation layer
* matches the view in MVC

#### View
* the business logic layer
* matches the controller in MVC
> A view function has two jobs: processing user input and returning appropriate response

<div align="right">

[↥ back to top](#django)

</div>
<br>

## Development Environment

A Python virtualenv (short for virtual environment) is how you set up your environment for different Python projects. It allows to use different packages in each project. Since it's not installing things system-wide, it does not require root permissions.

The following instructions apply to Red Hat 7.

### Installing EPEL and IUS packages
Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special Interest Group that creates, maintains, and manages a high quality set of additional packages for Enterprise Linux, including, but not limited to, Red Hat Enterprise Linux (RHEL), CentOS and Scientific Linux (SL), Oracle Linux (OL).

EPEL packages are usually based on their Fedora counterparts and will never conflict with or replace packages in the base Enterprise Linux distributions.
```shell
$ sudo yum install epel-release
```

Inline with Upstream Stable (or IUS) is a community project that provides RPM packages for newer versions of select software for Enterprise Linux distributions.
```shell
# If you are using CentOS replace package name with https://centos7.iuscommunity.org/ius-release.rpm
$ sudo yum install https://rhel7.iuscommunity.org/ius-release.rpm
```

### Installing Python 3.6 and virtualenvwrapper
The __python36u__ package provides the "python3.6" executable: the reference interpreter for the Python language, version 3.
The majority of its standard library is provided in the python36u-libs package, which should be installed automatically along with python36u. The remaining parts of the Python standard library are broken out into the python36u-tkinter and python36u-test packages, which may need to be installed separately.

Documentation for Python is provided in the python36u-docs package.

Packages containing additional libraries for Python are generally named with the "python36u-" prefix.
```shell
$ sudo yum install python36u
```

__virtualenvwrapper__ is a set of extensions to Ian Bicking’s virtualenv tool. The extensions include wrappers for creating and deleting virtual environments and otherwise managing your development workflow, making it easier to work on more than one project at a time without introducing conflicts in their dependencies.
```shell
$ pip3 install virtualenvwrapper
```

Include virtualenvwrapper settings in _~/.bashrc_. This assumes that python projects will reside in ~/Projects and virtual environments files within the hidden folder ~/.virtualenvs. Feel free to change according to your needs.
```shell
$ echo "# Virtualenvwrapper settings" >> ~/.bashrc
$ echo "export WORKON_HOME=\$HOME/.virtualenvs" >> ~/.bashrc
$ echo "export PROJECT_HOME=\$HOME/Projects" >> ~/.bashrc
$ echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3" >> ~/.bashrc
$ echo "source /usr/bin/virtualenvwrapper.sh" >> ~/.bashrc
```

Edit _postmkvirtualenv_ to automate the creation of the required folders for any given project and switch to that folder upon creation. This assumes that projects are under the ~/Projects folder and virtual environment files in ~/.virtualenvs, if you have changed those above, you'll need to change them accordingly here.
Application files will reside in the _app_ folder within the project name folder. This way, additional files not directly associated with the app but related to the project can coexist in the same project folder.
```shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postmkvirtualenv
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postmkvirtualenv
$ echo "mkdir -p \$DIRECTORY && cd \$DIRECTORY" >> ~/.virtualenvs/postmkvirtualenv
```

Edit _postactivate_ script in order to switch to the app folder upon virtual environment activation.
```shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postactivate
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postactivate
$ echo "if [ -d \"\$DIRECTORY\" ]; then cd \$DIRECTORY; fi" >> ~/.virtualenvs/postactivate
```

### Install PostgreSQL Server 10

PostgreSQL is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

Install PostgreSQL 10 repository
```shell
$ sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm
```

Install the server and client packages
```shell
$ sudo postgresql10-server postgresql10
```

Initialize the database and optionally enable automatic start
```shell
$ sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
$ sudo systemctl start postgresql-10
```

Optionally enable automatic start of the PostgrqSQL server on server start
```shell
$ systemctl enable postgresql-10
```

### Create the Virtual Environment

Create a new environment in the WORKON_HOME. The new environment is automatically activated after being initialized.
```shell
$ mkvirtualenv <project-name>
```

Install Django 1.11 LTS, Django Debug Toolbar and Selenium. Notice that when the virtual environment is activated, you can use pip command instead of pip3.
```shell
$ pip install "django>=1.11,<2.0" django-debug-toolbar "selenium<4"
```

Install Pyscopg2 to connect to PostgreSQL Server. This assumes PostgreSQL has already been installed.
```shell
$ pip install pyscopg2
```

Once finished working with the virtual environment you can exit from it by deactivating
```shell
$ deactivate
```
To work once again
```shell
$ workon <project-name>
```

<div align="right">

[↥ back to top](#django)

</div>
<br>

## Creating a Django Project

Create the project
```shell
$ django-admin startproject <project-name>
```
#### 2. Make migrations
This will also create the database
```shell
$ python manage.py migrate
```
#### 3. Start the development server
```shell
$ python manage.py runserver
```

#### Exit the virtual environment
```shell
$ deactivate
```

<div align="right">

[↥ back to top](#django)

</div>
<br>