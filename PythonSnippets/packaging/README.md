MedChemica Limited
------------------

Python Code Snippets
--------------------

###Creating a Python Package that can be run from Command Line

####Problem Statement

Your new product 'awesome' is a complex piece of code that you have custom written for a client
They have no version control and they systems are fluid and directories may change

How do we writing a Python Package for the code that can be driven by Command Line and imported
into other code without having to set PYTHONPATH or write code for the program to work out
where it is on their system. The client it prone to creating sub-directories for version numbers
and messing everything up

We 'have-to' include a version number in the project directory, when we send out tar-ball
Can we use symbolic link then to run the code? 

Solution - write a Python package within the directory with all the code

Within the package 'relative imports' can be used - so that the code directory can move about
This also means the package can be imported without problem
If we wrap the package in a higher directory we can code an arg parser so CommandLine is possible


####Structure

	pyiexpt-v1.0.0
		|-	__init__.py
		|-	__main__.py		# is run by interpreter at runtime - this imports and calls parts from the module
		|
 		|-    prom			# This is our python package - a complete modules - relative import done in here
		|	|-	__init__.py
		|	|-     MC
		|	|	|-	__init__.py
		|	|	|-	PrintFun.py
		|
		|	|-     app
		|	|	|-	__init__.py
		|	|	|-	experiment.py
		|
		|	|-     plugin		# This could be a different GitHub repo at allow growth and separate development
		|	|	|-	__init__.py
		|	|	|-     app
		|	|	|	|-	__init__.py
		|	|	|	|-	main.py
		|

####NOTES - Using relative imports

Each sub directory must have a __init__.py file to be notes as part of the package
This file can be empty

	$ touch __init__.py

At a minimum it provides a label

Treat relative imports just like moving about in a shell (ish)

	from .thismodule import stuff

Single . for the current directory

	from ..MC import PrintFun

Two dots up a level and then across to another directory.

Say we were importing from main.py in the plugin.app

	from ...app import experiment

Now three dots.

By using relative imports we could completely move the package around anywhere and not loose connections.

####Running the script from the command line


If we call from outside

	python pyiexpt-v1.0.0

__init__.py and __main__.py will can called.
These file the importing from the package AND MUST BE ABOVE THE PACKAGE.

Relative imports do not work if a module is called directly for outside the PACKAGE

Look at __main__.py

This program uses absolute imports to now do the work.
This is the only place to now worry about paths needing to be right.



####Creating symbolic link to run the code

	ln -s pyiexpt-v1.0.0 awesome

Now we can run the code thus

	python awesome

With a new release we can install next to this package and just change the link OR
completely move the package without anything breaking.
Just change the link.
