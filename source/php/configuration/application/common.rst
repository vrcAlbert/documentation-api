Common
######

Configuration for :php:class:`Nos\\Orm\\Model`, used in :doc:`appdesk`, :doc:`crud` or :doc:`inspector`.

Associative array:

:data_mapping: columns on :doc:`appdesk` and :doc:`inspector`.
:i18n: Optional, common translation
:actions: Optional, common actions on the :php:class:`Nos\\Orm\\Model`.
:icons: Optional, common icon related to the :php:class:`Nos\\Orm\\Model`.

Data mapping
************

Associative array where each key => value defines a column, all keys are optionals.

:title: Title of the grid column. If not set, column will not be displayed.
:column: Default value is same as key.
:search_column: Default value is column key value. Defines where on which sql column search / order.
:search_relation: Default value is deduced from key (ex: ``rel->col``). Relation to load (via related function on query).
:multiContextHide: Hide grid column when items are filtered on more than one contexts.
:value: A closure function taking current item :php:class:`Nos\\Orm\\Model` in first parameter. Overloads value displayed in grid.
:cellFormatters: Associative array of :ref:`cellFormatters <php/configuration/application/cellFormatters>` for formatting column display.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_a' => array(
                'title' => 'Column A',
                'column' => 'col_a',
                'multiContextHide' => true,
                'cellFormatters' => array(
                    'center' => array(
                        'type' => 'css',
                        'css' => array('text-align' => 'center'),
                    ),
                ),
            ),
            'column_b' => array(
                'title' => 'B',
                'search_column' => 'col_b_search',
                'search_relation' => 'rel',
                'value' => function($item) {
                    return 'test';
                },
            ),
            // ...
        ),
    );

Particular cases
================

In next example, ``column_a`` is sent in json but will not be displayed.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_a',
        ),
    );

In next example, ``col_b`` is sent in json under the column_b key but will not be displayed.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_b' => 'col_b',
        ),
    );


If the :php:class:`Model` have behaviour :php:class:`Orm_Behaviour_Twinnable`, a pseudo column ``context`` is automatically added at the end of ``data_mapping``.
But, if you want to place it elsewhere, you can insert it like this:

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_a' => array(
                'title' => 'Column a'
            ),
            'context',
            'column_b' => array(
                'title' => 'Column b'
            ),
        ),
        // ...
    );

I18n
****

This key contains all common translations.

.. code-block:: php

    <?php
    return array(
        'i18n' => array(
            // Crud
            'notification item added' => __('Done! The item has been added.'),
            'notification item saved' => __('OK, all changes are saved.'),
            'notification item deleted' => __('The item has been deleted.'),

            // General errors
            'notification item does not exist anymore' => __('This item doesn’t exist any more. It has been deleted.'),
            'notification item not found' => __('We cannot find this item.'),

            // ... extends /framework/config/i18n_common.config.php
        ),
    );

.. _php/configuration/application/common/actions:

Actions
*******

This key contains all common actions related to the model. There are 5 actions automatically added:

* ``add``: the :guilabel:`Add model` button located on the appdesk's toolbar
* ``edit``: The :guilabel:`Edit` button located on the grids and crud toolbar
* ``delete``: The :guilabel:`Delete` button located on the grids and crud toolbar
* ``visualize``: The :guilabel:`Visualize` button located on grids and crud toolbar, if item is displayable in front-office.
* ``share``: The :guilabel:`Share` button located on crud toolbar, if item have the :php:class:`Nos\\Orm_Behaviour_Sharable` behaviour.

The action key can be filled in two different ways.

The most common way is to define an associative array:

.. code-block:: php

    <?php
    return array(
        // ...
        'actions' => array(
            'action_1' => array(/* configuration */),
            'action_2' => array(/* configuration */),
            // ...
        ),
    );

If you want to define the order in which the actions are defined, two keys are to be defined:

:list: associative array of actions (similar to previous ``actions`` key)
:order: array of action key defining their order

.. code-block:: php

    <?php
    return array(
        // ...
        'actions' => array(
            'list' => array(
                'action_1' => array(/* configuration */),
                'action_2' => array(/* configuration */),
                // ...
            ),
            'order' => array(
                'action_2',
                'action_1'
            ),
        ),
    );

Each action is an associative array. Key is the action ID, and value is an array defining the action configuration:

:action: defines the action executed when action is triggered (using :doc:`/javascript/$/nosAction`).
:label: Text associated to action (displayed or on tooltip).
:primary: Is the action a primary action. On the grid, it defines whether or not it appears only in the action drop down or not.
:icon: Icon of the action. The string is appended to ``ui-icon-`` in order to obtain `jquery ui icon class <http://jqueryui.com/themeroller/#icons>`__.
:red: Is the action red or not.
:targets: Where to display the action. It is an associated array where keys defines where to display the action, the value a boolean defining whether or not the action is displayed. ``targets`` can be refined by the ``visible`` key. There are 3 available keys:

    :grid: Is the action displayed on the grid (appdesk and inspector) ?
    :toolbar-grid: Is the action displayed on the grid toolbar ?
    :toolbar-edit: Is the action displayed on the crud edit toolbar ?

:disabled: Callback function that returns a boolean defining if the action is disabled or not for an item. There is only one parameter sent: the current item.
:visible: Callback function that returns a boolean defining if the action is visible or not on a context. There is only one parameter sent, an associative array:

    :model: Model tested.
    :item: Only defined when actions are displayed on crud.
    :target: Target where action is displayed. Value can be ``grid``, ``toolbar-grid`` or ``toolbar-edit`` (related to ``targets``).
    :class: Class of the controller calling the function (this way you can differentiate appdesk and inspectors for instance).

.. code-block:: php

    <?php
    return array(
        'actions '=> array(
            'action_id' => array(
                'action' => array(
                    'action' => 'confirmationDialog',
                    'dialog' => array(
                        'contentUrl' => '{{controller_base_url}}delete/{{_id}}',
                        'title' => 'Delete',
                    ),
                ),
                'label' => __('Delete'),
                'primary' => true,
                'icon' => 'trash',
                'red' => true,
                'targets' => array(
                    'grid' => true,
                    'toolbar-edit' => true,
                ),
                'disabled' => function($item) {
                    return false;
                },
                'visible' => function($params) {
                    return !isset($params['item']) || !$params['item']->is_new();
                },
            ),
        ),
    );

Default actions and particular cases
====================================

Default actions (such as ``add`` or ``edit``) can be overloaded with this ``actions`` key. `\\Arr::merge <http://fuelphp.com/docs/classes/arr.html#/method_merge>`__ is used to merge defined actions with default actions.

This will hide the default ``add`` action:

.. code-block:: php

    <?php
    return array(
        // ...
        'actions '=> array(
            'add' => false,
        ),
    );

Placeholders
============

Placeholders are available in order to simplify action targets and labels. First, some placeholders are always available:

* ``controller_base_url``: url of crud controller
* ``model_label``: generated from model class name
* ``_id``: id of the object
* ``_context``: if behaviour contextable
* ``publication_status``: if behaviour publishable

Additionally, all ``dataset`` items are used as placeholders.

Icons
*****

This key contains all common icons related to the model. Structure is similar to the icons key in :doc:`metadata` configuration file :

.. code-block:: php

    <?php
    return array(
        'icons' => array(
            64 => 'static/apps/noviusos_page/img/64/page.png',
            32 => 'static/apps/noviusos_page/img/32/page.png',
            16 => 'static/apps/noviusos_page/img/16/page.png',
        ),
    );