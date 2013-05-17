.. _php/configuration/software:

Novius OS
#########

A sample configuration file is available in :file:`local/config/config.php.sample`.
Just rename (or copy) it to :file:`local/config/config.php`, and update it to your case.

.. php:global:: cache

    ``Boolean`` for use of cache on front. By default is ``true``, except in DEVELOPMENT environment.

    .. versionadded:: 0.2.0.2

.. php:global:: cache_duration_page

    ``Int``, number of seconds of cache validity. By default is ``60``.

.. php:global:: cache_model_properties

    ``Boolean`` for use of cache on :php:class:`Nos\\Orm\\Model` properties. By default is ``false``.
    If is ``true``, all models properties will be cached with a auto-refresh mechanism : if you add a column on a model which has properties defined,
    the cache will be refreshed by a DB ``list_columns`` request when you access this column with ``get()`` or ``set()``.

    .. versionadded:: Chiba 1.0.1

.. php:global:: upload

    ``Array`` :

    :param disabled_extensions: ``Array`` of invalid extensions for files uploaded in Novius OS. By default ``php`` is disabled.

.. php:global:: assets_minified

    ``Boolean`` for use of assets minified in back-office. By default is ``true``, except in DEVELOPMENT environment.

.. _php/configuration/software/db:

Database
########

The DB configuration was initially created by the installation wizard. But you can (and you must to go live) update
it after installation.

The DB configuration is in :file:`local/config/db.php`.

 .. seealso::

 	`FuelPHP Database documentation <http://fuelphp.com/docs/classes/database/introduction.html>`_ for details.

Email
#####

By default, your Novius OS is not configured to send mail, because it's too dependent on the server.

A sample configuration file is available in :file:`local/config/email.config.php.sample`.
Just rename (or copy) it to :file:`local/config/email.config.php`, and update it to your case.

.. seealso::

	`FuelPHP email package documentation <http://fuelphp.com/docs/packages/email/introduction.html>`_ for details.
