Inspectors
##########

Configuration for an inspector. Associative array depending on inspector type.

The only common keys are `input`, which describes how the inspector will affect the main grid, and `appdesk`, which defines how it is displayed.

input
*****

Associative array:

:key: Key name on which the main grid will be filtered. By default, if query key is not defined, must be the column name on which you want to filter the model.
:query: Optional. Callback function defining how to interact with the main grid query. The function gets two parameters ; the first is the value sent by the inspectors (when items are selected), and the second is the current query. The function must return the transformed query.


appdesk
*******

Associative array. All keys are optional:

:label: Main label of the inspector.
:contextChange: Does the inspector reloads when user selects an other context.
:reloadEvent: Event name that will reload the inspector?
:vertical: Is the appdesk vertical or horizontal ?
:inputName: Key on which selected values are sent.

Model inspector
***************

Associative array:

:model: Model class name
:query: Optional. Additional informations about the query. See :ref:`query in appdesk configuration <php/configuration/application/appdesk/query>`.
:data_mapping: Optional. Defines which data_mapping items are displayed. See :ref:`data_mapping in appdesk configuration <php/configuration/application/appdesk/data_mapping>`.
:appdesk: Optional. Additional display information about the appdesk.

appdesk
-------

Associative array:

:grid: Optional. Grids informations. Associative array:

    :urlJson: Url of the json API to get items
    :columns: Columns informations.

Model tree inspector
********************

Associative array:

:model: Model class name
:data_mapping: Optional. Defines which data_mapping items are displayed. See :ref:`data_mapping in appdesk configuration <php/configuration/application/appdesk/data_mapping>`.
:appdesk: Optional. Additional display information about the appdesk.
:models: Optional. See :ref:`appdesk tree configuration <php/configuration/application/appdesk/tree>`.
:roots: Optional. See :ref:`appdesk tree configuration <php/configuration/application/appdesk/tree>`.
:root_node: Optional. Add a global root node. Associative array containing dataset values (columns to be displayed).

appdesk
-------

Associative array:

:treeGrid: Optional. Grids informations. Associative array:

    :urlJson: Url of the json API to get items
    :columns: Columns informations.

Date inspector
**************

Associative array:

:input_begin: Name of the input for the begin date. Default value: ``date_begin``.
:input_end: Name of the input for the end date. Default value: ``date_end``.
:labels:
    :Custom dates: Default value: ``Custom dates``.
    :from begin to end: Default value: ``from {{begin}} to {{end}}``.
    :until end: Default value: ``until {{end}}``.
    :since begin: Default value: ``since {{begin}}``.
:options: | Array of options displayed by inspector. Default value: ``array('custom', 'since', 'month', 'year')``.
:since:
    :optgroup: Label of this group in the inspector. Default value: ``Since``.
    :options: Associative array. Key is the date, `string is processed by Date Class <http://fuelphp.com/docs/classes/date.html>`__, value is the label of the date.
:month:
    :optgroup: Label of this group in the inspector. Default value: ``Previous months``.
    :first_month: Month to start list from. Default value: ``now``.
    :limit_type: Limit type where the list end (value can be ``year`` or ``month``). Default value: ``year``.
    :limit_value: Number of items to display. For example, if ``limit_type`` is ``month`` and ``limit_value`` is 5, it will display the last 5 months. Default value: ``1``.
:year:
    :optgroup: Label of this group in the inspector. Default value: ``Years``.
    :first_year: Year to start list from. Default value: ``now``.
    :limit: Number of years to display. Default value: ``4``.

Plain data inspector
********************

Displays static data. Associative array:

:data: Array of items. Each item is an associative array:

    :id:
    :title:
    :icon: Optional.

:input:

    :query: Here this key is mandatory.

:appdesk:

    :url: Url to load in order to display list extension.
    :grid: How is the inspector grid displayed

        :columns: Grid columns. Associative array, key is column identifier and value is an associative array:

            :headerText: Column title
            :visible: Is key visible
            :dataKey: For each data item, defines which key is displayed