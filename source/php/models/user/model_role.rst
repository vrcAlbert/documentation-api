Model_Role
##########

.. php:namespace:: Nos\User

.. php:class:: Model_Role

	Extend :php:class:`Nos\\Orm\\Model`.

Relations
*********

.. php:attr:: users

	* Relation type : :term:`many_many`.
	* Model : :php:class:`Model_User`


Methods
*******

.. php:method:: check_permission($permission_name, $category_key = null)

	:param string $permission_name: Name of the permission to check against
    	:param string $category_key: (optional) If the permission has categories, the category key to check against
    	:returns: ``True`` if the role has the required authorisation, ``false`` otherwise


.. php:method:: listPermissionCategories($permission_name)

    List all the categories of a given permission name. Returns an array of string or false when the role has not
    access, or the permission name does not exists.

	:param string $permission_name: The name of the permission to retrieve categories from
    	:param string $category_key: (optional) If the permission has categories, the category key to check against
    	:returns: ``array|false`` An array containing the list of categories (values) for the request permission name
