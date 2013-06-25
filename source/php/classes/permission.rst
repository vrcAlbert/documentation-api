.. _php/classes/permission:

Permission
##########

.. php:namespace:: Nos\User

.. php:class:: Permission

    This class checks the permissions for the current logged in user.

    When multiple roles are enable, if any role has the requested permission, it means the user is authorised to do it.

.. php:staticmethod:: check($permission_name, $category_key = null, $allow_empty = false)

    Alias to :php:meth:`Nos\\User\\Permission::exists`


.. php:staticmethod:: exists($permission_name, $category_key = null, $allow_empty = false)

    Check whether a permissions exists (against all the roles of the current logged in user).

    :param string $permission_name: Name of the permission to check against
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :param bool $allow_empty: (optional) Should we grant access when nothing is configured?
    :returns bool: ``true`` or ``false``


.. php:staticmethod:: existsOrEmpty($permission_name, $category_key = null, $allow_empty = false)

    Alias to :php:meth:`Nos\\User\\Permission::exists` with the optional parameter ``$alowEmpty = true``.

    :param string $permission_name: Name of the permission to check against
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :returns bool: ``true`` or ``false``


.. php:staticmethod:: isAllowed($permission_name, $allow_empty = false)

     Check against a binary permission (without categories) against all the roles of the current logged in user.

     :param string $permission_name:  Name of the permission
     :param bool $allow_empty: Should we grant access when nothing is configured?
     :returns bool: ``true`` or ``false``


.. php:staticmethod:: atLeast($permission_name, $threshold, $value_when_empty = 0)

     Check against a numeric / range permission (for all the roles of the current logged in user).

     You can use ``string`` for the 2nd and 3rd parameters, they will be casted to ``(int)``. i.e. ``'2_write' === 2``.

     :param string $permission_name:  Name of the permission
     :param int $threshold: Minimum value to grant access
     :param int $value_when_empty: Default value to compare with when nothing is configured
     :returns bool: ``true`` or ``false``


.. php:staticmethod:: atMost($permission_name, $threshold, $value_when_empty = 0)

     Check against a numeric / range permission (for all the roles of the current logged in user).

     You can use ``string`` for the 2nd and 3rd parameters, they will be casted to ``(int)``. i.e. ``'2_write' === 2``.

     :param string $permission_name:  Name of the permission
     :param int $threshold: Maximum value to grant access
     :param int $value_when_empty: Default value to compare with when nothing is configured
     :returns bool: ``true`` or ``false``


.. php:staticmethod:: listPermissionCategories($permission_name)

     List all the categories of a given permission name (merged values from all the roles of the current logged in user).

     Returns an array of string or ``false`` when access is denied, or the permission name does not exists.

     :param string $permission_name:  The name of the permission to retrieve categories from
     :returns array|false: An array containing the list of categories (values) for the requested permission name


.. php:staticmethod:: isApplicationAuthorised($application_name)

     Check whether a user can access a particular application

     :param string $application_name:  Name of the application
         :returns bool: ``true`` or ``false``


.. php:staticmethod:: contexts()

     .. seealso:: :php:meth:`Nos\\Tools_Context::contexts`

     Returns an array of all the contexts the user can access.


.. php:staticmethod:: locales()

     .. seealso:: :php:meth:`Nos\\Tools_Context::locales`

     Returns an array of all the locales the user can access.


.. php:staticmethod:: sites()

     .. seealso:: :php:meth:`Nos\\Tools_Context::sites`

     Returns an array of all the sites the user can access.
