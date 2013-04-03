Permissions
###########

This configuration file is used to define the permissions used in your application.

It has the same syntax as the **full** version of the :ref:`crud layout <php/configuration/crud/layout>`.

i.e. You need to configure one or several (``view`` + ``params``) pair(s), like so:

.. code-block:: php

    <?php
    return array(
        'all' => array(
            'view' => 'nos::form/accordion',
            'params' => array(
                'accordions' => array(
                    'standalone' => array(
                        'title' => __('Permissions for this application'),
                        'view' => 'nos::admin/permissions/standalone',
                        'params' => array(
                            'list' => array(
                                'noviusos_app::create' => array(
                                    'label' => __('Can create new items'),
                                    'checked' => true,
                                ),
                                'noviusos_app::delete_locked' => array(
                                    'label' => __('Can delete locked item'),
                                ),
                            ),
                        ),
                    ),
                ),
            ),
        ),
    );



In addition to view-specific params / data, Novius OS always include the following vars:

* ``$role`` : Current :php:class:`role <Nos\\User\\Model_Role>` for which the permissions are applicable to.

We (kindly) provide a native view to cover basic usage: :ref:`php/views/permissions_standalone`.
