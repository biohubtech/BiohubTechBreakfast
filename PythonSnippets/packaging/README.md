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



Structure

 

####Creating symbolic link to run the code

	ln -s pyiexpt-v1.0.0 awesome

Now we can run the code thus

	python awesome

With a new release we can install next to this package and just change the link OR
completely move the package without anything breaking.
Just change the link.
