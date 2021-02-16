ResidentialReporter
===================

This is the ResidentialReporter development repository.

Bugs & Discussion
=================

Please research any bugs you find via our `Github issue tracker for
ResidentialReporter <https://github.com/residentialreporter/residentialreporter/issues>`__
and report them, if they're still unknown.

You can also find us here to ask questions or just chat:

* Gitter.im: `gitter.im/residentialreporter <https://gitter.im/residentialreporter/community>`__
* Github.org: `github.com/residentialreporter <https://github.com/residentialreporter>`__

WiP Status
==========

Right now, you should be able to:

* Install and build frontend including iOS/Android applications
* Install and configure the backend
* Log in a user account via frontend

What's upcoming:

* Retrieval and storage of objects
* Custom forms and tables for objects
* Map view of locations

Structure
=========

First of all: it's still a classical backend/frontend architecture.
Mesh based (scalable) and p2p collaborative infrastructure might follow later,
depending on other Isomer framework components' progress in that regard.

Backend
-------

This software package is a module for `Isomer <https://github.com/isomeric/isomer>`__.

Isomer - along with some base "isomeric" modules - provide basic required functionality
like:

* Object document modelling via json-schemata in MongoDB (Postgres is WiP)
* Object validation and versioning (Collaborative editing is WiP)
* Client API handling for classc CRUD via realtime websocket
* Administrative toolkit
* Secure user enrollment and notification mechanisms
* Geography related features
* Statistics and gamification aspects
* File handling for attachments
* Threaded comment system
* User sessions
* Simple newsroom functionality
* (optional) Calendar support

Frontend
--------

It comes with its own full frontend. Most of Isomer's old frontend technology will be
rebuilt with new technology for this package and parts will be reused in the new
generalized, next generation Isomer frontend, which we'll hopefully be able to
backport, later.

The new frontend uses quite sophisticated technologies, all latest versions
(as of January 2021) - earlier ones may work partially:

* Angular
* Ionic
* Cordova (switching to capacitor) for iOS and Android apps
* Electron for the desktop app
* Rxjs with ngrx and ngrx-auto-entities
* Material design
* Angular JSON schema form
* Openlayers

Installation
============

Summary
-------

The general idea is to:

* install Isomer first, then
* install this module, its provisions and finally
* build the frontend

Starting the Isomer backend should now give you access to the ResidentialReporter
components.

These instructions are for Debian but are adaptable to other operating systems.
If you're not on Debian, you'll need to get the following dependencies installed
somehow else.

Requirements
------------

Some dependencies - not listed here - will be automatically installed, other
minimal requirements should be handled by your operating system's packager of choice.

An asterisk in the following lists means earlier versions might work, too - no
guarantees!

Backend
~~~~~~~

* Python >= 3.6
* Pip3 >= 20.0*
* Pymongo for Python3 >= 3.0
* MongoDB >= 3.2
* Pillow for Python3 >= 8.0*

Frontend
~~~~~~~~

Debian Sid has these, but Buster is very probably too old:

* nodejs >= 12.0 (>= 10.0 *might* work, too)
* npm >= 7.1.0

For building the iOS and Android apps, you will need the respective SDKs, Emulators etc.

Setting up with (Debian) Linux
------------------------------

There are detailed instructions for multiple variants of setting up Isomer at the
`Isomer documentation site, <https://isomer.readthedocs.io/en/latest/start/quick.html>`_
but here's a brief synopsis for immediate development.

OS preparations
~~~~~~~~~~~~~~~

Below are instructions to set up apt-based distros..
These may be different for Arch, Gentoo, FreeBSD, etc, so please adapt:

.. code-block::

    # Development basics
    sudo apt install git virtualenv gnupg wget python3 python3-pip

    # Isomer specific
    sudo apt install python3-pymongo python3-pymongo-ext python3-spur \
        python3-bson pyton3-bson-ext enchant

    # Install these only if you're at least on Debian Sid:
    sudo apt install nodejs npm

Isomer + ResidentialReporter
~~~~~~~~~~~~~~~~

Let's download the source code and install it for development:

.. code-block::

    mkdir residentialreporter

    cd residentialreporter
    git clone https://github.com/isomeric/isomer.git
    git clone https://github.com/residentialreporter/residentialreporter.git
    git clone https://github.com/residentialreporter/residentialreporter-frontend.git

    virtualenv -p /usr/bin/python3 --system-site-packages venv
    source venv/bin/activate

    cd isomer
    pip3 install -r requirements-dev.txt
    python3 setup.py develop

    cd ../residentialreporter
    python3 setup.py develop

Setting up an Instance
~~~~~~~~~~~~~~~~~~~~~~

Test installation and create default instance to work with:

.. code-block::

    # Set up required paths, isomer user account and basic configuration
    # (We're omitting the platform steps because we installed them above)
    # (Add --log-actions or -l to see what will be done)
    sudo ../venv/bin/iso system --omit-platform all

    # Should greet with the logger listing ResidentialReporter schemata and others:
    iso dev entrypoints --all -f residentialreporter

    # Now create an empty more or less unconfigured instance for development
    sudo ../venv/bin/iso instance create

    # Set the database to a default name, otherwise it is unset
    sudo ../venv/bin/iso -e current environment set database default

Create admin user:

.. code-block::

    iso db user create-admin

To run the development instance:

.. code-block::

    iso launch --dev

Frontend
~~~~~~~~

Install and build the frontend:

.. code-block::

    cd ../residentialreporter-frontend

    npm install -g ionic @angular/cli
    npm install
    ionic serve

See the frontend readme for more details on frontend matters.

API url
~~~~~~~

The backend api is usually localhost:8055. Both port and host address can be
reconfigured either by editing `/etc/isomer/instances/default.conf` or by supplying
`--host` and `--port` arguments to the launcher command line:

.. code-block::

    iso launch --dev -p 8000 -a 192.168.1.42

The frontend development and production endpoints are configured in the standard
angular way, inside the `frontend/src/environments/environment.*.ts` files.

Development Guidelines
======================

WiP, please stay tuned and watch the issue tracker or the chat (see above) for
stuff to do.

In the meantime, you could browse the `Isomer Framework Developer guidelines
<https://isomer.readthedocs.io/en/latest/dev/general/index.html>`__.

Deployment
==========

A development backend for public testing will be rolled out, soon.
The production backend is planned to go live in early 2021.

For the frontend, we're testing Github's new-ish workflow system.
A build workflow that generates an Android APK is already in place.

See `.github/workflows` for more details.

History
=======

WiP

Licenses
========

Media Licenses
--------------

Most external meda (if not specifically mentioned) is licensed under the
CC-BY-SA-3.0 or similar license, which you can find here:
https://creativecommons.org/licenses/by-sa/3.0/deed.en

* building icon (in logo) by Brad Avison from the Noun Project
  https://thenounproject.com/term/building/2903271/
* Header image contains background photography from Norberto Kolus (CC-BY-SA 3.0)
  https://commons.wikimedia.org/wiki/File:Night_Walk_In_Berlin_(256820535).jpeg


AGPL3.0
-------

Copyright (C) 2020 ResidentialReporter Community and others.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
