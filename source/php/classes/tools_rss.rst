Tools_RSS
#########

.. php:namespace:: Nos

.. php:class:: Tools_RSS

	Use to build a RSS.

Methods
*******

::forge()
---------

.. php:staticmethod:: forge($channel = array(), array $items = array())

	:params mixed $channel: If it is a ``string``, use for ``title`` of channel. Associative array otherwise:

        :encoding: Default ``UTF-8``. Use for XML encoding attribut.
        :version: Default ``2.0``. Use for version attribut of XML tag <rss>.

		You can define any other key, which will be transformed into XML tag in the <channel />

	:params array $items: Associative array. Each key will be transformed into XML tag in a <item />.
	:returns: A new :php:class:`Tools_RSS`.

::set()
-------

.. php:method:: set($property, $value = null)

	:params mixed $property: A single ``string`` for set a channel property, or an associative array for multiple setting.
	:params mixed $value: If ``$property`` is a ``string``, the value of the property.

	Set one or multiple channel properties.

::set_items()
-------------

.. php:method:: set_items(array $items)

	:params array $items: Array of items.

	Set a new array of items.

::add_item()
------------

.. php:method:: add_item(array $item)

	:params array $item: An item.

	Add a new item to array items.

::build()
---------

.. php:method:: build(array $channel = array(), array $items = array())

	:params mixed $channel:
	:params array $items:
	:returns: A XML description of RSS

	See :php:meth:`Tools_RSS::forge` for parameters.

	For item, ``pubDate`` key can be a ``Fuel\\Core\\Date``, a string date representation or a timestamp.

Examples
********

.. code-block:: php

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


