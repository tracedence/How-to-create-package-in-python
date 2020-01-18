# How-to-create-package-in-python
How to create python package which can be installed


# __init__.py 
The package folder which contains a special file __init__.py. It's two purpose
1. It __init__.py present in folder, python will recognize it as a package.
2. In __init__.py we can specify which resources can be imported from current package.
3. An empty __init__.py makes all functions available to imported.


# How to install package
To install package, we have to call setup script. The setup script will call the setup() function from setuptools module.
The setup() function takes various arguments like author_name, author_email, version, zip_safe ..etc. The zip_safe argument defines whether the package is installed in compressed mode or regular mode.

What to put in setup.py
# code of setup.py
from setuptools import setup, find_packages

setup(
      name = 'package_name',
      version = '0.0.1',
      packages = find_packages(include= ['project_one']),
      install_requires = [
                          'pandas==0.23.0', # exact version of pandas
                          'numpy>=1.14',  # minmum version
                          'matplotlib>=2.2.0, <3.0.0' # range of version
                          'pytorch',
                          'tensorflow',
                          ]
      extra_require = {
                        'interactive': ['bigquery', 'jupyter',]
                      }
      entry_points = {
                        'console_scripts':['my-command=package_name.file_name:function_name']
                      }
      setup_requires=['pytest-runner'],
      tests_requires=['pytest'],
      package_data = {'package_name':['data/some_data.json']}
      )
      
Description of setup argument
* name: The name of package which pip will use to install package. The name should need to same as folder name. An example pip install scikit-learn and we use import sklearn.
* version: is used when we publish it on  PyPI.
* packages: it will install only those packages which are present as argument in find_package.
* install_requires: it will contains all those package which are required for my current package.
* extra_require: these are extra dependency which are required only in some cirmcustance. To run model into the production, we don't need jupyter. I need jupyter package only for analysis of data, so I can specify it in extra_require. If you we use pip install -e then only install_requires packages will installed. To install optional packages we will use pip install -e .['interactive']
* entry_points: To expose the functionality of package to the command line. we can now use my-command from command line to call the function.
* create a file setup.cfg, add the test= pytest. Now to run the test, we can simply type python setup.py test, it will automatically installed and run the pytest. If we have additonal requirement for testing we can specify it in setup_requires.
* package_data: will install the data available in package. It will store in pkg_resources after installed. To use this data code as follow: 
from json import load
from pkg_resoureces import resource_stream

data = load(resource_stream('package_name', 'location of data in package'))



# To install package
pip install -e . --> . represent here current directory and -e flag specifies that we want to install package in editable mode, which means that when we make changes in our package we do not need to re-install the package. We either need to restart python or reload the package.



# Resources from where I got all this information, I write it in my own way. 
Thank you "GO DATA DRIVEN"
https://blog.godatadriven.com/setup-py
      
