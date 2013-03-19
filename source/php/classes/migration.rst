Migration
#########

.. php:namespace:: Nos

.. php:class:: Migration

	Provides migration automation and methods useful for migrations.

->up()
---------------------------

.. php:method:: up()

	Tries to execute a sql file with same path (if migration filename is 001_install.php, it will try to execute
	001_install.sql).

->down()
---------------------------

.. php:method:: down()

	Does nothing. Need to be overridden if you want to support this operation.

::executeSqlFile($sql_file)
---------------------------

.. php:staticmethod:: executeSqlFile($sql_file)

	:param string $sql_file: Sql file location to be executed.