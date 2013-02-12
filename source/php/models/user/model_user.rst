Model_User
##########

.. php:class:: Model_User

	| Extend :php:class:`Model`.
	| Belongs to the namespace :php:ns:`Nos/User`

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

	:params string $password: Password to check if it matches the user password
	:returns: ``True`` if passwords match, ``false`` otherwise.

.. php:method:: generate_md5()

	Generate a ``md5`` for user and set to column ``user_md5``.
