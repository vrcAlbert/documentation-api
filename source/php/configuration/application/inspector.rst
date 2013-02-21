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
:query: Optional. Additional informations about the query. See :ref:`query in appdesk configuration <php/configuration/application/appdesk/query>`.
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

:input_begin: Optional. Default value: `date_begin`.
:input_end: Optional. Default value: `date_end`.
:label_custom: Optional. Title used when custom dates can be selected. Default value: "Custom dates".
:label_custom_inputs: Optional. Defines how the custom inputs are displayed. There is two placeholders: `begin` and `end`.
:options: Optional. Main (root) options for date selector. For each option a key must exists which value is an associative array:

    :since: Custom date we can filter since.

        :optgroup: Label
        :options: Associative array. Key is the date, `string is processed by <http://fuelphp.com/docs/classes/date.html>`__, value is the label of the date.

    :month: Filter by month.

        :optgroup: Label.
        :first_month: Month to start list from.
        :limit_type: Limit type where the list end (value can be "year" or "month").
        :limit_value: Number of items to display. For example, if `limit_type` is "month" and `limit_value` is 5, it will display the last 5 months.

    :year: Filter by year.

        :optgroup: Label.
        :first_year: Year to start list from.
        :limit: Number of years to display.

Plain data inspector
********************

Displays static data, so it is the simplest inspector. Associative array:

:data: Array of items. Each item is an associative array:

    :id:
    :title:
    :icon: Optional.

:appdesk:

    :url: Url to load in order to display list extension.
    :grid: How is the inspector grid displayed

        :columns: Grid columns. Associative array, key is column identifier and value is an associative array:

            :headerText: Column title
            :visible: Is key visible
            :dataKey: For each data item, defines which key is displayed