# Flask Basic Setup Protocol

### Instance Folders

Instance folders enables the developer to segregate deployment-specific files from
our application,

1) Create an instance directory in the root of the application: `$ mkdir instance`

  The directory structure should resemble this:

  ```
    application_name/
        - app.py
        - instance/
            - config.cfg
  ```

  We can then use the instance path parameter to set the absolute path of this
  instance folder on the application object.  Once set we use the
  instance_relative_config parameter on the same application object:

  ```python
    app = Flask(
      __name__, instance_path = '/absolute/path/to/instance/folder',
                instance_relative_config = True
      )

    app.config.from_pyfile('config.cfg', silent = True)

  ```

  The `silent = True` acts to suppress any error if the files are not found

### Composition of Views and Models

1. Create a new directory and move all our files inside of it
2. Create an `__init__.py` in each folder, so we can use these as modules
3. Create a new file called `run.py` in the topmost folder.
4. Create separate folders to act as modules.

```
application_name/
    - run.py
    - my_app/
        – __init__.py
        - hello/
            - __init__.py
            - models.py
            - views.py
```

The `run.py` file will resemble:

  ```python
    from my_app import app
    app.run(debug=True)
  ```

The `__init_-.py` file for the my_app directory should resemble:
  ```python
  # import flask
  from flask import Flask

  # initialize the app
  app = Flask(__name__)

  # import the views from the hello module
  import my_app.hello.views
  ```

To make hello a module it must have an `__init__.py` file within it.  This file
does not need to have any running code though.

To run the app we just need to be in the root application directory and run `python run.py` from the command-line.

### Using Blueprints
[Flask Blueprints Docs](http://flask.pocoo.org/docs/0.12/blueprints/)

Blueprints in Flask are intended for these cases: (from the docs)

* Factor an application into a set of blueprints. This is ideal for larger applications; a project could instantiate an application object, initialize several extensions, and register a collection of blueprints.
* Register a blueprint on an application at a URL prefix and/or subdomain. Parameters in the URL prefix/subdomain become common view arguments (with defaults) across all view functions in the blueprint.
* Register a blueprint multiple times on an application with different URL rules.
* Provide template filters, static files, templates, and other utilities through blueprints. A blueprint does not have to implement applications or view functions.
* Register a blueprint on an application for any of these cases when initializing a Flask extension.

Open the `application_name/my_app/__init__.py` file and update it:

```python
from flask import Flask
from my_app.hello.views import hello

app = Flask(__name__)
app.register_blueprint(hello)
```

### Templating

To include templates create a `template/` directory in the root application directory.

```
application_name/
    - run.py
    - my_app/
        – __init__.py
        - hello/
            - __init__.py
            - models.py
            - views.py
        - templates/
```
