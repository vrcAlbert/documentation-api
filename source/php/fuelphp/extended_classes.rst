Extended Classes
################

We `extended some classes from FuelPHP <http://fuelphp.com/docs/general/extending_core.html>`__. The additions we
made are listed in this page.


.. contents::
    :depth: 2
    :local:

Core Classes
============

Arr
----

Added the static **recursive_filter**\($array, $callback) method.

Autoloader
----------

Allow for filename suffixes for *model* and *controller*, as follow: **model.model.php** and **controller.ctrl.php**.

If you have a ``Controller_Admin_Page``, its filename can either be ``classes/controller/admin/page.php`` or ``classes/controller/admin/page.ctrl.php``.

Cache_Storage_File
------------------

**__construct()** will try to create the specified cache directory when it doesn't exists.

Config
------

Added `events to alter the loaded configuration <events_configuration>`__.


Date
----

- Added the static method **compare**\($date1, $date2)
- Added the instance method **modify**\($modify)

Email_Driver
------------

**send()**: we added :ref:`two events <php/events/email>` ``email.before_send`` and ``email.after_send``

Event_Instance
--------------

Added two methods **register_function()** and **trigger_function()** to deal with by-reference arguments.


Fieldset and Fieldset_Field
---------------------------

- Added the static method **Fieldset::build_from_config()**
- Integration of :doc:`renderers </php/renderers/index>` in the methods of these two classes

File
----

Added the method **relativeSymlink()**


Finder
------

- Added the Novius OS framework path in the searched paths
- Allow for filename suffixes for *config*, *views* and *lang* files (same rule as the ``Autoloader``, see above)


Image
-----

Added the static method **gravatarUrl**\($email, $options)


Module
------

Allow for a custom namespace retrieved from the config when loading a module (used in our applications).


Response
--------

Added the static method **json()** to return JSON data


Security
--------

Added the method **htmlspecialchars()**


Session
-------

Added the static method **user()** to retrieve the current logged in user in the back-office.


String
------

Added the static methods **textToHtml**\($text) and **humanFileSize**\($bytes, $format);


View
----

Added the static method **redirect**\($from, $to, $callback)


ORM Package
===========

Model
-----

- Added a cache for ``Model::$_properties``
- Added :ref:`behaviours <php/behaviours>`
- Added somes :doc:`relations  </php/relations/index>`

Query
-----

Added getters for ``alias``, ``connection`` and ``model``.

