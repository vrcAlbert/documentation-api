Common
######

Configuration for :php:class:`Model`, used in :doc:`appdesk`, :doc:`crud` or :doc:`inspector`.

Associative array:

:data_mapping: columns on :doc:`appdesk` and :doc:`inspector`.
:i18n: Optional, common translation
:actions: Optional, common actions on the :php:class:`Model`.
:icons: Optional, common icon related to the :php:class:`Model`.

Data mapping
************

Associative array where each key => value defines a column, all keys are optionals.

:title: Title of the grid column. If not set, column will not be displayed.
:column: Default value is same as key.
:search_column: Default value is column key value. Defines where on which sql column search / order.
:search_relation: Default value is deduced from key (ex: "rel->col"). Relation to load (via related function on query).
:multiContextHide: Hide grid column when items are filtered on more than one contexts.
:value: A closure function taking current item :php:class:`Model` in first parameter. Overloads value displayed in grid.
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


If the :php:class:`Model` have behaviour :php:class:`Orm_Behaviour_Twinnable`, a pseudo column ``context`` is automatically add at the end of ``data_mapping``.
But, if you want to position elsewhere, you can refrence:

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

.. todo::

	Actions et icons de la configuration commun