Model_User
##########

.. php:namespace:: Nos\User

.. php:class:: Model_User

	Extend :php:class:`Nos\\Orm\\Model`.

.. todo::

	Methods hash_password et check_permission utilisées ?

Relations
*********

.. php:attr:: roles

	* Relation type : :term:`many_many`.
	* Model : :php:class:`Model_Role`


Methods
*******

.. php:method:: check_password($password)

	:param string $password: Password to check if it matches the user password
	:returns: ``True`` if passwords match, ``false`` otherwise.

.. php:method:: generate_md5()

	Generate a ``md5`` for user and set to column ``user_md5``.
