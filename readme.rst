CodeIgniter 3.1.13 IPMS Admin
================================

Modern setup for legacy PHP 7.2.3 servers — with generator scripts for rapid admin panel development.

.. image:: https://img.shields.io/badge/PHP-7.2.3-blue
   :alt: PHP 7.2.3
.. image:: https://img.shields.io/badge/CodeIgniter-3.1.13-orange
   :alt: CodeIgniter 3.1.13
.. image:: https://img.shields.io/badge/XAMPP-Windows-green
   :alt: XAMPP Windows

----

Server Requirements
-------------------

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Requirement
     - Version
   * - PHP
     - 7.2.3 ✓
   * - Database
     - MySQL / MariaDB (XAMPP default)
   * - Web Server
     - Apache with ``mod_rewrite``
   * - Environment
     - XAMPP (Windows localhost)

----

Quick XAMPP Installation
-------------------------

1. Download & Extract
~~~~~~~~~~~~~~~~~~~~~

Download the CI 3.1.13 ZIP and extract it to::

   C:\xampp\htdocs\admin-system\

2. Start XAMPP
~~~~~~~~~~~~~~

Launch the XAMPP Control Panel and start **Apache** and **MySQL**.

3. Configure Base URL
~~~~~~~~~~~~~~~~~~~~~

Edit ``application/config/config.php``:

.. code-block:: php

   $config['base_url'] = 'http://localhost/admin-system/';

4. Configure Database
~~~~~~~~~~~~~~~~~~~~~

Edit ``application/config/database.php``:

.. code-block:: php

   $db['default']['hostname'] = 'localhost';
   $db['default']['database'] = 'ci_admin';
   $db['default']['username'] = 'root';
   $db['default']['password'] = '';

5. Enable Clean URLs
~~~~~~~~~~~~~~~~~~~~

Create a ``.htaccess`` file in the project root with ``mod_rewrite`` enabled:

.. code-block:: apache

   RewriteEngine On
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule ^(.*)$ index.php/$1 [L]

6. Test Your Installation
~~~~~~~~~~~~~~~~~~~~~~~~~

Visit: `http://localhost/admin-system/ <http://localhost/admin-system/>`_

----

Generator Scripts (CI3 CLI)
----------------------------

Place ``ci-gen.ps1`` (PowerShell) and ``ci-gen.sh`` (Bash) in the project root.
Each command scaffolds a **Migration + Model + Controller + View** automatically.

PowerShell (Windows / XAMPP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: powershell

   # Open PowerShell inside admin-system/
   .\ci-gen.ps1 make:user

Bash (Git Bash / WSL)
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   chmod +x ci-gen.sh
   ./ci-gen.sh make:admin

Then visit ``http://localhost/admin-system/admin`` for instant CRUD!

----

Migrations
----------

1. **Enable migrations** — create ``application/config/migration.php`` and set:

   .. code-block:: php

      $config['migration_enabled'] = TRUE;

2. **Generate** a migration:

   .. code-block:: powershell

      .\ci-gen.ps1 make:user

3. **Run** migrations by visiting::

      http://localhost/admin-system/migrate

----

Development Workflow
--------------------

.. code-block:: text

   1. .\ci-gen.ps1 make:users              # Scaffold files
   2. http://localhost/admin-system/migrate # Run DB migrations
   3. Customize application/controllers/users.php
   4. Add Tailwind / Bootstrap to your views
   5. Deploy to your PHP 7.2.3 server

----

Project Structure
-----------------

.. code-block:: text

   admin-system/
   ├── ci-gen.ps1              # Generator script (Windows)
   ├── ci-gen.sh               # Generator script (Linux/Mac)
   ├── index.php
   ├── .htaccess               # Clean URL rewrite rules
   ├── application/
   │   ├── config/             # database.php, migration.php
   │   ├── controllers/        # Generated controllers
   │   ├── models/             # Generated models
   │   ├── migrations/         # Generated migration files
   │   └── views/              # Generated views
   └── system/                 # CI3 core (do not modify)

----

Deployment
----------

1. Upload all project files **except** ``ci-gen.ps1`` and ``ci-gen.sh``
2. Update ``$config['base_url']`` in ``application/config/config.php`` to your production domain
3. Run migrations against your production database

----

Resources
---------

- `CodeIgniter 3 User Guide <https://codeigniter.com/userguide3/>`_
- `XAMPP Documentation <https://www.apachefriends.org/faq_windows.html>`_

License
-------

Distributed under the `CodeIgniter License <https://github.com/bcit-ci/CodeIgniter/blob/develop/license.txt>`_.