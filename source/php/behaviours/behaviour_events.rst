.. _php/behaviours/behaviour_event:

Behaviour events
################

Behaviours can catch events triggered on a :php:class:`Nos\\Orm\\Model` or on a instance of :php:class:`Nos\\Orm\\Model`.

.. _php/behaviours/behaviour_event/instance:

Instance events
***************

.. php:method:: dataset(&$dataset)

    Trigger when fill ``dataset`` of an item.

    :param array $dataset: Current ``dataset`` of the item.

.. php:method:: form_fieldset_fields(&$config)

    Trigger when build a ``fieldset`` from an item.

    :param array $config: Current ``fieldset`` configuration.

.. php:method:: form_processing($data, &$json_response)

    Trigger when receive a ``form`` response.

    :param array $data: Data received.
    :param array $json_response: JSON response to send.

.. php:method:: wysiwygOptions(&$options)

    Trigger when construct WYSIWYG options for an item.

    :param array $options: Current option for WYSIWYG.

.. _php/behaviours/behaviour_event/static:

Static events
*************

.. php:method:: gridQuery($config, &$query)

    Trigger when building a query for a grid of model's items.

    :param array $config: Configuration for the query.
    :param mixed $query: Current query.

.. php:method:: gridItem($object, &$item)

    Trigger when building a grid's item.

    :param mixed $object: Instance of Model's item.
    :param array $item: Current item in array style.

.. php:method:: gridAfter($config, $objects, &$items)

    Trigger after execute query for a grid of model's items.

    :param array $config: Configuration of the query.
    :param array $objects: Array of instances of model, result of the query.
    :param array $items: Current array of items in array style.

.. php:method:: commonConfig(&$config)

    Trigger when building a common configuration of a model.

    :param array $config: Current configuration.

.. php:method:: crudConfig(&$config, $controller)

    Trigger when building the configuration of the CRUD controller of the model.

    :param array $config: Current configuration of the CRUD controller.
    :param mixed $controller: Instance of the CRUD controller.

.. php:method:: crudFields(&$fields, $controller)

    Trigger when building the fields for the CRUD controller of the model.

    :param array $fields: Current fields of the CRUD controller.
    :param mixed $controller: Instance of the CRUD controller.

.. php:method:: buildRelations()

    Trigger when building relations of the model.

.. php:method:: before_query(&$options)

    Trigger before execute a query build on the model.

    :param array $options: Current options for the query.
