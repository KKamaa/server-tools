============
Fuzzy Search
============

.. !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! This file is generated by oca-gen-addon-readme !!
   !! changes will be overwritten.                   !!
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

.. |badge1| image:: https://img.shields.io/badge/maturity-Beta-yellow.png
    :target: https://odoo-community.org/page/development-status
    :alt: Beta
.. |badge2| image:: https://img.shields.io/badge/licence-AGPL--3-blue.png
    :target: http://www.gnu.org/licenses/agpl-3.0-standalone.html
    :alt: License: AGPL-3
.. |badge3| image:: https://img.shields.io/badge/github-OCA%2Fserver--tools-lightgray.png?logo=github
    :target: https://github.com/OCA/server-tools/tree/14.0/base_search_fuzzy
    :alt: OCA/server-tools
.. |badge4| image:: https://img.shields.io/badge/weblate-Translate%20me-F47D42.png
    :target: https://translation.odoo-community.org/projects/server-tools-14-0/server-tools-14-0-base_search_fuzzy
    :alt: Translate me on Weblate
.. |badge5| image:: https://img.shields.io/badge/runbot-Try%20me-875A7B.png
    :target: https://runbot.odoo-community.org/runbot/149/14.0
    :alt: Try me on Runbot

|badge1| |badge2| |badge3| |badge4| |badge5| 

This addon provides the ability to create GIN or GiST indexes of char and text
fields and also to use the search operator `%` in search domains. Currently
this module doesn't change the backend search or anything else. It provides
only the possibility to perform the fuzzy search for external addons.

**Table of contents**

.. contents::
   :local:

Installation
============

#. The PostgreSQL extension ``pg_trgm`` should be available. In debian based
   distribution you have to install the `postgresql-contrib` module.
#. Install the ``pg_trgm`` extension to your database or give your postgresql
   user the ``SUPERUSER`` right (this allows the odoo module to install the
   extension to the database).

Configuration
=============

If the odoo module is installed:

#. You can define ``GIN`` and ``GiST`` indexes for `char` and `text` via
   `Settings -> Database Structure -> Trigram Index`. The index name will
   automatically created for new entries.

Usage
=====

#. You can create an index for the `name` field of `res.partner`.
#. In the search you can use:

   ``self.env['res.partner'].search([('name', '%', 'Jon Miller)])``

#. In this example the function will return positive result for `John Miller`
   or `John Mill`.

#. You can tweak the number of strings to be returned by adjusting the set
   limit (default: 0.3). NB: Currently you have to set the limit by executing
   the following SQL statement:

   ``self.env.cr.execute("SELECT set_limit(0.2);")``

#. Another interesting feature is the use of ``similarity(column, 'text')``
   function in the ``order`` parameter to order by similarity. This module just
   contains a basic implementation which doesn't perform validations and has to
   start with this function. For example you can define the function as
   followed:

   ``similarity(%s.name, 'John Mil') DESC" % self.env['res.partner']._table``

For further questions read the Documentation of the
`pg_trgm <https://www.postgresql.org/docs/current/static/pgtrgm.html>`_ module.


Usage with demo data
====================

There are some demo data that allow you to test functionally this module
if you are in a **demo** database. The steps are the following:

#. Go to *Contacts* and type the text **Jon Smith** or **Smith John** in
   the search box and select **Search Display Name for: ...**
#. You will see two contacts, and they are the ones with display names
   **John Smith** and **John Smizz**.

Known issues / Roadmap
======================

* Modify the general search parts (e.g. in tree view or many2one fields)
* Add better `order by` handling

Bug Tracker
===========

Bugs are tracked on `GitHub Issues <https://github.com/OCA/server-tools/issues>`_.
In case of trouble, please check there if your issue has already been reported.
If you spotted it first, help us smashing it by providing a detailed and welcomed
`feedback <https://github.com/OCA/server-tools/issues/new?body=module:%20base_search_fuzzy%0Aversion:%2014.0%0A%0A**Steps%20to%20reproduce**%0A-%20...%0A%0A**Current%20behavior**%0A%0A**Expected%20behavior**>`_.

Do not contact contributors directly about support or help with technical issues.

Credits
=======

Authors
~~~~~~~

* bloopark systems GmbH & Co. KG
* ForgeFlow
* Serpent CS

Contributors
~~~~~~~~~~~~

* Christoph Giesel <https://github.com/christophlsa>
* Jordi Ballester <jordi.ballester@forgeflow.com>
* Serpent Consulting Services Pvt. Ltd. <support@serpentcs.com>
* Dave Lasley <dave@laslabs.com>

* `Tecnativa <https://www.tecnativa.com>`_:
  * Vicent Cubells
  * Ernesto Tejeda
* teodoralexandru@nexterp.ro  2020            NextERP SRL.

Maintainers
~~~~~~~~~~~

This module is maintained by the OCA.

.. image:: https://odoo-community.org/logo.png
   :alt: Odoo Community Association
   :target: https://odoo-community.org

OCA, or the Odoo Community Association, is a nonprofit organization whose
mission is to support the collaborative development of Odoo features and
promote its widespread use.

This module is part of the `OCA/server-tools <https://github.com/OCA/server-tools/tree/14.0/base_search_fuzzy>`_ project on GitHub.

You are welcome to contribute. To learn how please visit https://odoo-community.org/page/Contribute.
