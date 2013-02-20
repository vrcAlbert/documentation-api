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
