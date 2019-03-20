Heroku buildpack: Python
========================

This is a [Heroku buildpack](https://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](https://pip.pypa.io/).

[![Build Status](https://secure.travis-ci.org/heroku/heroku-buildpack-python.png?branch=master)](https://travis-ci.org/heroku/heroku-buildpack-python)

Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --stack cedar --buildpack git://github.com/heroku/heroku-buildpack-python.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> No runtime.txt provided; assuming python-2.7.6.
    -----> Preparing Python runtime (python-2.7.6)
    -----> Installing Distribute (0.7.3)
    -----> Installing Pip (1.5.4)
    -----> Installing dependencies using Pip (1.5.4)
           Downloading/unpacking Flask==0.7.2 (from -r requirements.txt (line 1))
           Downloading/unpacking Werkzeug>=0.6.1 (from Flask==0.7.2->-r requirements.txt (line 1))
           Downloading/unpacking Jinja2>=2.4 (from Flask==0.7.2->-r requirements.txt (line 1))
           Installing collected packages: Flask, Werkzeug, Jinja2
           Successfully installed Flask Werkzeug Jinja2
           Cleaning up...

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/heroku/heroku-buildpack-python.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.4.0
    
Runtime options include:

- python-2.7.6
- python-3.4.0
- pypy-2.2.1 (experimental)
