Appdesk
#######
Configuration for :php:class:`Nos\\Orm\\Model`'s appdesk.

Associative array:

:model: Model name.
:query: Optional. Additional informations about the query.
:search_text: Optional. Array of columns in which we search when the user fills appdesk's search bar.
:data_mapping: Optional. Defines which data_mapping item we display.
:inspectors: Optional.
:views: Optional.
:i18n: Optional. Extends default text items.
:thumbnails: Optional, boolean. Can the appdesk display items as thumbnails ?
:tree: Optional (automatically filled when model has the :ref:`tree behaviour <php/behaviours/tree>`)/.
:appdesk: Optional. Additional display information about the appdesk.

query
*****

Associative array. All keys are optional. Most keys are similar than the `find function second parameters <http://fuelphp.com/docs/packages/orm/crud.html#functions>`__.

:model: Model on which query is executed
:limit:
:order:
:related:
:callback: Array of callback functions allowing you to customize the query (first parameter is the current query, must return the modified query).

data_mapping
************

Associative or simple array. Defines which data_mapping items from :ref:`common configuration <common>` we display (mostly filtering).

Is is also possible to define new custom data_mapping items which will be only used on the appdesk.

If only value is defined, appdesk will display the data_mapping item from common configuration.

If it is a key => value association (value must then be an array), then the data_mapping item from common configuration is extended by the value.

.. code-block:: php

    <?php
    return array(
        // ...
        'data_mapping '=> array(
            'col1', // will display the col1 data_mapping item from common configuration.
            'col2' => array( // if col2 exists on common configuration data_mapping key then it is extended ; otherwise, the item is added to appdesk.
                // ...
            ),
        ),
    );

inspectors
**********

Associative or simple array. Defines which inspectors are used on appdesk.

If is also possible to define new custom inspectors which will be only used on the appdesk.

If only value is defined, appdesk will display the inspector located at `inspector/inspector_name` if the value is `inspector_name`.

If it is a key => value association (value must then be an array), then the inspector configuration is extended by the value.

.. code-block:: php

    <?php
    return array(
        // ...
        'inspectors '=> array(
            'inspector1', // will display the inspector located at inspector/inspector1.
            'inspector2' => array( // if inspector/inspector2 exists, then it is extended ; otherwise it creates a new inspector
                // ...
            ),
        ),
    );

views
*****


thumbnails
**********

Can the appdesk display items as thumbnails ?

If defined to true, data_mapping has to define two keys:

:thumbnail: url of item thumbnail.
:thumbnailAlternate: Default thumbnail when there is no thumbnails or thumbnail can't be found.


tree
****



appdesk
*******

