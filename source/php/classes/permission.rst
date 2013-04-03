Permission
##########

.. php:class:: Permission

.. php:staticmethod:: check($permission_name, $category_key = null)

    This is a helper to call :php:meth:`Nos\\User\\Model_User::check_permission` for the logged :php:class:`Nos\\User\\Model_User`.

	:param string $permission_name: Name of the permission to check against
    :param string $category_key: (optional) If the permission has categories, the category key to check against
    :returns: ``True`` if the user has the required authorisation, ``false`` otherwise.

