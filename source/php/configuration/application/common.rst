Common
######

Configuration for :php:class:`Nos\\Orm\\Model`, used in :doc:`appdesk`, :doc:`crud` or :doc:`inspector`.

Associative array:

:data_mapping: columns on :doc:`appdesk` and :doc:`inspector`.
:i18n:         Optional, common translation
:actions:      Optional, common actions on the :php:class:`Nos\\Orm\\Model`.
:icons:        Optional, common icons related to the :php:class:`Nos\\Orm\\Model`.

Data mapping
************

Associative array where each key => value defines a column, all keys are optionals.

:title:            Title of the grid column. If not set, column will not be displayed.
:column:           Default value is same as key.
:search_column:    Default value is column key value. Defines on which SQL column search / order.
:search_relation:  Default value is deduced from key (ex: ``rel->col``). Relation to load (via related function on query).
:sorting_callback: A closure function taking two parameters: the ``$query`` object and the ``$sortDirection``.
:multiContextHide: Hide grid column when items are filtered on more than one contexts.
:isSafeHtml:       If ``true``, the content won't be escaped when displayed (inside the grid).
:value:            A closure function taking current item :php:class:`Nos\\Orm\\Model` in first parameter. Overloads value displayed in the grid.
:cellFormatters:   Associative array of :ref:`cellFormatters <php/configuration/application/cellFormatters>` for formatting column display.

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

In the following example, ``column_a`` is sent in json but is not displayed in the grid.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_a',
        ),
    );

In the following example, ``col_b`` is sent in json under the ``column_b`` key but is not displayed in the grid.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            'column_b' => 'col_b',
        ),
    );


If the :php:class:`Model` has the :php:class:`Orm_Behaviour_Twinnable` behaviour, a pseudo column ``context`` is
automatically added at the end of the ``data_mapping``.
But, if you want to place it elsewhere, you can force its position like this:

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

This key contains all the common translations.

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

            // ... see the 'framework/config/i18n_common.config.php' file to include the appropriate keys depending on your item
        ),
    );

.. _php/configuration/application/common/actions:

Actions
*******

This key contains all the common actions related to the model. 5 actions are automatically added:

:add:       The :guilabel:`Add model` button located on the appdesk's toolbar
:edit:      The :guilabel:`Edit` button located on the grids and the crud's toolbar
:delete:    The :guilabel:`Delete` button located on the grids and the crud's toolbar
:visualise: The :guilabel:`Visualise` button located on the grids and crud's toolbar, if the item can be displayed in front-office.
:share:     The :guilabel:`Share` button located on the crud's toolbar, if the item has the :php:class:`Nos\\Orm_Behaviour_Sharable` behaviour.

The action key can be filled in two different ways.

The most common way is to use an associative array:

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

If you want to change the order in which the actions are displayed, two keys are to be defined:

:list:  associative array of actions (similar to the previous ``actions`` key)
:order: array of action's key defining their order

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

:action:  which action is executed when clicking on the button (using :doc:`/javascript/$container/nosAction`).
:label:   Text associated with the action (either shown as text or in a tooltip).
:primary: Is it a primary action? Primary actions have a dedicated button, and secondary actions appears in the action drop down.
:icon:    Icon of the action. It's a `jquery ui icon class <http://jqueryui.com/themeroller/#icons>`__, but without the leading ``ui-icon-`` string.
:red:     Is it a red action? (especially used for 'Delete')
:align:   Alignment of the button. Can be a string (``begin`` or ``end``) or a number (``begin`` is equivalent to
    ``-10`` and ``end`` is equivalent to ``10``). Defines actions default order (``align`` in ascending order).
:targets: Where is the action displayed? This has no effect if the action is not ``visible`` (see below). There are 3 locations available:

    :grid:         Is the action displayed on the grid (appdesk and inspector)?
    :toolbar-grid: Is the action displayed on the grid's toolbar?
    :toolbar-edit: Is the action displayed on the crud's toolbar (edition form)?

:disabled: Callback function or array of callback functions (the one taken into account is the first which doesn't
    return ``false``) that returns a boolean or a string defining if the action is disabled or not for an item (a string
    disable the action and the value is used as title). There is two sent parameters: the current ``$item``, and
    ``$params`` containing the common configuration.
:visible:  Callback function or array of callback functions (the one taken into account is the first which doesn't
    return ``true``) that returns a boolean defining if the action is visible or not on a context. There is only one
    parameter sent, an associative array:

    :model:  Model tested.
    :target: Target where action is displayed. Value can be ``grid``, ``toolbar-grid`` or ``toolbar-edit`` (related to action's ``targets``).
    :item:   Only populated when ``target == 'toolbar-edit'``.
    :class:  Name of the controller class calling the function (this way you can differentiate appdesk and inspectors for instance).

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

Default actions (such as ``add`` or ``edit``) can be overloaded with this ``actions`` key. `Arr::merge <http://fuelphp.com/docs/classes/arr.html#/method_merge>`__ is used to merge defined actions with default actions.

To hide an action, set its value to ``false``:

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

* ``controller_base_url``: URL of the crud controller
* ``model_label``: generated from model class name
* ``_id``: ID of the item
* ``_title``: Title of the item
* ``_context``: if the item has the ``Contextable`` behaviour

Additionally, all ``dataset`` keys can be used as placeholders.

Icons
*****

This key contains all common icons related to the model. Structure is similar to the icons key of the :doc:`metadata` configuration file :

.. code-block:: php

    <?php
    return array(
        'icons' => array(
            64 => 'static/apps/noviusos_page/img/64/page.png',
            32 => 'static/apps/noviusos_page/img/32/page.png',
            16 => 'static/apps/noviusos_page/img/16/page.png',
        ),
    );
