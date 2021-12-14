# Contributing #

The documentation is built using [Sphinx](http://sphinx-doc.org) and [reStructuredText](http://sphinx-doc.org/rest.html).  
This guide is copied from the official [ASP.NET Docs](https://github.com/aspnet/Docs).

## Building the Docs ##

Once you have cloned the Docs to your local machine, the following instructions will walk you through installing the tools necessary to build and test.

1. [Download python](https://www.python.org/downloads/) version 2.7.10 or higher (Version 3.5 is recommended). If you install 3.5, check the include python in path option.

2. Skip this step if you installed python 3.5 and checked the "include in python path" option. If you are installing on Windows, ensure both the Python install directory and the Python scripts directory have been added to your `PATH` environment variable. For example, if you install Python into the c:\python34 directory, you would add `c:\python34;c:\python34\scripts` to your `PATH` environment variable.

3. Clone the docs: 

    ```git clone https://github.com/Sitecore/Helix.Docs.git```
 
4. Navigate to the Docs repo and install the build dependencies:

	```cd Helix.Docs```

	```pip install -r requirements.txt```
	
  **Note**: You might need to run this command from Power Shell.
	
5. Navigate to the  *helix* directory and run ``make.bat``

	```cd helix```

	```make.bat html ```

6. Once make completes, the generated docs will be in the .../Helix.Docs/helix/_build/html directory. Open the `index.html` file in your browser to see the built docs for that project. ``make livehtml`` is recommended, see the next section.

## Use autobuild to easily view site changes locally ##

You can also install [sphinx-autobuild](https://github.com/GaretJax/sphinx-autobuild) which will run a local web server and automatically refresh whenever changes to the source files are detected. To do so:
    

1. Run ``make livehtml`` (make.bat on Windows, Makefile on Mac/Linux) from the *helix* directory
 
    ```make.bat livehtml```

2. Browse to `http://127.0.0.1:8000` to see the locally built documentation. 

3. Hit `^C` to stop the local server.
