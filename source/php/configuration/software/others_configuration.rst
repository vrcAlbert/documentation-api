.. _php/configuration/software/db:

Database
########

The DB configuration was set by the install wizard. But you can (must for the passage in production)  update it after install.

DB configuration is in :file:`local/config/db.php` and see `FuelPHP Database documentation <http://fuelphp.com/docs/classes/database/introduction.html>`_.

Email
#####

By default, your Novius OS was not configure to send mail. The configuration is too dependent on the server.

You have a sample file for configuration in :file:`local/config/email.config.php.sample`.
Simply rename it to :file:`local/config/email.config.php` and update it to your case.
See `FuelPHP email package documentation <http://fuelphp.com/docs/packages/email/introduction.html>`_ for details.
