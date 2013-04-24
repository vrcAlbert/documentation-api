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

.. php:method:: check_permission($permission_name, $category_key = null)

    :param string $permission_name: Name of the permission to check against
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :returns: ``True`` if the user has the required authorisation, ``false`` otherwise


Methods
*******

.. php:method:: check_password($password)

    :param string $password: Password to check if it matches the user's password
    :returns: ``True`` if passwords match, ``false`` otherwise.

.. php:method:: generate_md5()

	Generate a new ``md5`` for the user (store in the ``user_md5`` column).
