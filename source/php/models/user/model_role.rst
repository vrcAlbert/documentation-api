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

.. php:method:: checkPermission($permission_name, $category_key = null, $allow_empty = false)

    Check whether a permissions exists with the given category.

    :param string $permission_name: Name of the permission to check against
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :param bool $allow_empty: Should we grant access when nothing is configured?
    :returns bool: ``true`` or ``false``


.. php:method:: listPermissionCategories($permission_name)

    List all the categories of a given permission name. Returns an array of string or false when the role has not
    access, or the permission name does not exists.

    :param string $permission_name: The name of the permission to retrieve categories from
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :returns: ``array|false`` An array containing the list of categories (values) for the request permission name


.. php:method:: checkPermissionOrEmpty($permission_name, $category_key = null)

	Alias to :php:meth:`Nos\\User\\Model_Role::checkPermission` with ``$allow_empty = true``.


.. php:method:: checkPermissionExists($permission_name, $category_key = null, $allow_empty = false)

	Alias to :php:meth:`Nos\\User\\Model_Role::checkPermission`.


.. php:method:: checkPermissionExistsOrEmpty($permission_name, $category_key = null, $allow_empty = false)

	Alias to :php:meth:`Nos\\User\\Model_Role::checkPermission` with ``$allow_empty = true``.


.. php:staticmethod:: checkPermissionIsAllowed($permission_name, $allow_empty = false)

     Check against a binary permission (without categories).

     :param string $permission_name:  Name of the permission
     :param bool $allow_empty: Should we grant access when nothing is configured?
     :returns bool: ``true`` or ``false``


.. php:method:: checkPermissionAtLeast($permission_name, $threshold, $value_when_empty = 0)

     Check against a numeric / range permission.

     You can use ``string`` for the 2nd and 3rd parameters, they will be casted to ``(int)``. i.e. ``'2_write' === 2``.

     :param string $permission_name:  Name of the permission
     :param int $threshold: Minimum value to grant access
     :param int $value_when_empty: Default value to compare with when nothing is configured
     :returns bool: ``true`` or ``false``


.. php:method:: checkPermissionAtMost($permission_name, $threshold, $value_when_empty = 0)

     Check against a numeric / range permission.

     You can use ``string`` for the 2nd and 3rd parameters, they will be casted to ``(int)``. i.e. ``'2_write' === 2``.

     :param string $permission_name:  Name of the permission
     :param int $threshold: Maximum value to grant access
     :param int $value_when_empty: Default value to compare with when nothing is configured
     :returns bool: ``true`` or ``false``


.. php:method:: getPermissionValue($permission_name, $default = 0)

     Retrieve the value of a given permission.

     :param string $permission_name:  Name of the permission
     :param mixed $default: Default value to return when the permission does not exists
     :returns string:

