Tools_RSS
#########

.. php:namespace:: Nos

.. php:class:: Tools_RSS

	Used to build a RSS feed.

Methods
*******

::forge()
---------

.. php:staticmethod:: forge($channel = array(), array $items = array())

	:param mixed $channel: If it is a ``string``, used as channel's ``title``. Associative array otherwise:

        :encoding: Default ``UTF-8``. Used for the XML encoding attribute.
        :version: Default ``2.0``. Used for XML version attribute (``<rss>`` tag).

		You can define any other key, which will be transformed into XML tag in the ``<channel />``

	:param array $items: Associative array. Each key will be transformed into XML tag in a ``<item />``.
	:returns: A instance of :php:class:`Tools_RSS`.

::set()
-------

.. php:method:: set($property, $value = null)

	:param mixed $property: A single ``string`` to set a channel property, or an associative array for multiple settings.
	:param mixed $value: If ``$property`` is a ``string``, the value of the property.

	Set one or multiple channel properties.

::set_items()
-------------

.. php:method:: set_items(array $items)

	:param array $items: Array of items.

	Set a new array of items.

::add_item()
------------

.. php:method:: add_item(array $item)

	:param array $item: An item.

	Add a new item to the ``$items`` array.

::build()
---------

.. php:method:: build(array $channel = array(), array $items = array())

	:param mixed $channel:
	:param array $items:
	:returns: The XML description of the RSS

	See :php:meth:`Tools_RSS::forge` for parameters.

	The ``pubDate`` key can be a ``Fuel\\Core\\Date`` instance, or a string (date representation) or a timestamp.

Examples
********

.. code-block:: php

	<?php
	$rss = \Nos\Tools_RSS::forge('RSS title');
	$rss->set_items(array(
		'title' => 'Item title',
		'link' => 'http://www.mydomain.com/item_url.html',
		'description' => '<p>A description of item </p>',
		'pubDate' => '2012-08-16',
		'author' => 'Me',
	));
	$xml = $rss->build();

	$rss->set('subtitle', 'A subtitle for ma RSS');
	echo $rss; // Call $rss->build() with magic method __ toString()


