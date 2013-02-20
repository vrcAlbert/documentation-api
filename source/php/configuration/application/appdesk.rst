Appdesk
#######

Configuration for :php:class:`Nos\\Orm\\Model`'s appdesk.

Associative array:

:model: Model name.
:query: Optional. Additional informations about the query.
:search_text: Optional. Array of columns in which we search when the user fills appdesk's search bar.
:data_mapping: Optional. Defines which data_mapping item are displayed.
:inspectors: Optional.
:views: Optional.
:inputs: Optional. How to process additional parameters sent to
:selectedView: Optional. Default selected view identifier.
:i18n: Optional. Extends default text items.
:thumbnails: Optional, boolean. Can the appdesk display items as thumbnails ?
:tree: Optional (automatically filled when model has the :doc:`/php/behaviours/tree` behaviours enabled).
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

Associative or simple array. Defines which data_mapping items from :doc:`common` configuration we display (mostly filtering).

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

Associative array defining different way of displaying the appdesk. The key is the view identifier. Value is vew configuration:

:name: Optionnal. Display view name in view selector
:virtual: Optionnal. Is the view present on the view selector ?
:json: Array of javascript files to load. These javascript extends appdesk configuration.

.. todo:: show how appdesk configuration can be extended on javascript ?

thumbnails
**********

Can the appdesk display items as thumbnails ?

If defined to true, data_mapping has to define two keys:

:thumbnail: url of item thumbnail.
:thumbnailAlternate: Default thumbnail when there is no thumbnails or thumbnail can't be found.

tree
****

Defines how the model tree is constructed on the appdesk. It is automatically filled when model has the :ref:`tree behaviour <php/behaviours/tree>`)/. Associative array:

:models: Models to be loaded on the tree. Array of associative array:

    :model: Model class name
    :order_by:
    :childs: Array of model class name. Which models instances are children.
    :dataset: dataset information sent by objects in json format.

:roots:

    :model: Model class name
    :order_by:
    :where:

.. todo:: order_by but also other find parameters ?

appdesk
*******

Associative array describing how appdesk interacts and is displayed. All items are automatically generated, but can be overloaded.

:appdesk: Defines how appdesk is displayed. Associative array:

    :defaultView: Default view of appdesk.
    :buttons: Associative array containing grid toolbar actions information. See :ref:`php/configuration/application/common/actions`.
    :splitterVertical: Size of the vertical splitter.
    :inspectors: Associative array containing information about inspectors. Key is the inspector identifier, value is its configurations. See :ref:`inspectors configuration <common>`.
    :grid: Grids informations. Associative array:

        :urlJson: Url of the json API to get items
        :columns: Columns informations

    :treeGrid:

        :urlJson: Url of the json API to get items

:tab: Information about tab information (see :ref:`javascript/$/nosAction/nosTabs`).
:reloadEvent: Event name that will reload appdesk.
:actions: Associative array containing main grid actions information. See :ref:`php/configuration/application/common/actions`.