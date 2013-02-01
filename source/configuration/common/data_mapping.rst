Data mapping
############

Data mapping key defines columns on appdesks on inspectors.

Each value / key => value defines a column.

.. code-block:: php

    <?php
    return array(

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

            // title of the grid column.
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
    );