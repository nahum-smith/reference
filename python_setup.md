# Python Setup Procedure

## Step Zero- Create a project skeleton if you don't have one

1)  `$ mkdir skeleton`
2)  `$ cd skeleton`
3)  `$ mkdir bin NAME tests docs`

NAME will be changed to whatever the main module in <project_name> you chose

Create empty Python Directories
4)  `$ touch NAME/__init__.py`
5)  `$ touch tests/__init__.py`

Creating the setup.py file

6)  `$ touch setup.py`
7)  Add the following to the file (substitute your info into the contact info):
  ```
    try:
      from setuptools import setup
    except ImportError:
      from distutils.core import setup

    config = {
      'description':      'My Project',
      'Author':           'My Name',
      'url':              'your url',
      'download_url':     'where to download it',
      'author_email':     'My email',
      'version':          '0.1',
      'install_requires': ['nose'],
      'packages':         ['NAME'],
      'scripts':          [],
      'name':             'project_name'
    }
    setup(**config)

  ```
8) Create a simple skeleton file for tests: `$ touch tests/NAME_tests.py`

  ```
    from nose.tools import *
    import NAME

    def setup():
      print('Project Setup')

    def teardown():
      print('Project Teardown')

    def test_basic():
      print('Basic tests ran')

  ```
Your directory structure should look like the below:
  ```

    skeleton/
      NAME/
        __init__.py
      bin/
      docs/
      setup.py
      tests/
        NAME_tests.py
        __init__.py

  ```

test your skeleton structure by running: `$ nosetests` from the root project directory
You should see:
  ```
    $ nosetests
    -----------------------------------------------------

    Ran 1 test in 0.0006s

    OK

  ```

## Step one- Initial Setup
1) Create a virtual environment (segregated installation)
  * `$ mkvirtualenv <my_project>`
2) Initialize source control
  * `$ git init`
  * `$ touch .gitignore`
  * add: `*.pyc` and `__pycache__` to the `.gitignore`
3) `$ touch README.md`
  * add basic program description
4) create first commit with those two files
5) copy project skeleton from above
