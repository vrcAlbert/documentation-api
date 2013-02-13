Common
######

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(
            // columns on appdesks and inspectors.
        ),
        'i18n' => array(
            // Optionnal: common translation (appdesk, crud, inspectors...).
        ),
        'actions' => array(
            // Optionnal: common actions on the model.
        ),
        'icons' => array(
            // Optionnal: common icon related to the model.
        ),
    );

Data mapping
============

Data mapping key defines columns on appdesks on inspectors.

Each value / key => value defines a column.

.. code-block:: php

    <?php
    return array(
        'data_mapping' => array(

            // $item->column_a is sent in json (but must be processed to be of any use).
            'column_a',

            // $item->col_b is sent in json under the column_b key (but must be processed to be of any use).
            'column_b' => 'col_b',

            // $item->column_c is displayed in the grid under column which title is "Column C".
            'column_c' => array(
                'title' => 'Column C'
            ),

            // Full example.
            'column_d' => array(

                // Title of the grid column.
                'title' => 'Column C',

                // Default value is key. Will display $item->col_d if value key is empty.
                'column' => 'col_d',

                // Default value is column key value. Defines where on which sql column search / order.
                'search_column' => 'col_d_search',

                // Default value is deduced from key (ex: "rel->col"). Relation to load (via related function on query).
                'search_relation' => 'rel',

                // Hide grid column when models are filtered on more than one contexts.
                'multiContextHide' => true,

                // Overloads value displayed in grid. Here value is always 'test'.
                'value' => function($item) {
                    return 'test';
                },
            ),

            // Special value in order to display current contexts of the item.
            'context',
        ),
        // ...
    );

I18n
====

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

Actions
=======



Icons
=====