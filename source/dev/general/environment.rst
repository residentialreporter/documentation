.. _Git: https://git-scm.com/

.. _environment:

Setting up a ResidentialReporter Development Environment
============================================

This is the recommended way to setup a development environment for developing
the backend, frontend and modules of ResidentialReporter.

Getting Started
---------------

Here is a summary of the steps to your own development environment:

1. `Fork ResidentialReporter <https://github.com/residentialreporter/residentialreporter#fork-destination-box>`_
   (*if you haven't done so already*)
2. Clone your forked repository using `Git`_
3. Install the local management tool
4. Install an Isomer development instance
5. Install the ResidentialReporter module
6. Set up further development tools as desired

And you're done!

Setup
-----

The setup guide shall aid you in setting up a development environment for all
purposes and facettes of ResidentialReporter development.

Get the sourcecode
^^^^^^^^^^^^^^^^^^

After forking the repository, clone it to your local machine:

.. code-block:: sh

    git clone git@github.com:yourgithubaccount/residentialreporter.git ~/src/residentialreporter


Setting up a basic development Instance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This guide assumes, you have already installed Isomer on your development machine.

Create a new development instance:

.. code-block:: sh

    iso -i residentialreporter-dev instance create

Install the development instance from your repository clone:

.. code-block:: sh

    cd ~/src/residentialreporter

    iso -i residentialreporter-dev instance install-modules --install-env --source develop .

In theory, you should be able to ignore most of the instance and environment handling.
This process will be optimized in near future, so you won't have to bother about it at
all. If you encounter any problems, please report them.

Frontend Development
^^^^^^^^^^^^^^^^^^^^

.. attention::

    These instructions have not yet been verified but should be good. If you find
    any bugs, please report them.

Clone the frontend repository:

.. code-block::

    cd ~/src/residentialreporter
    git clone https://github.com/residentialreporter/residentialreporter-frontend frontend

Change to frontend directory and install dependencies:

.. code-block:: sh

    cd frontend
    npm install -g ionic @angular/cli
    npm install

and run the development webserver:

.. code-block:: sh

    ionic serve

Now after testing and compiling, it should launch the frontend in your default browser.

Usual ionic/angular development guidelines apply.
