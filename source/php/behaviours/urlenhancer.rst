.. _php/behaviours/urlenhancer:

Urlenhancer
###########

.. php:namespace:: Nos

.. php:class:: Orm_Behaviour_Urlenhancer

	| Used for :php:class:`Nos\\Orm\\Model` displayed in the front-office by an :ref:`URL Enhancer <metadata/enhancers>`.

Configuration
*************

.. php:attr:: enhancers

	Required.
	Array of :ref:`enhancers <metadata/enhancers>` ID which can generate an URL for the item.

	Listed :ref:`enhancers <metadata/enhancers>` must define a ``getUrlEnhanced($params)`` method.

Methods
*******

.. php:method:: urls($params = array())

	:param array $params:

		:enhancer: Specify :ref:`enhancer <metadata/enhancers>` ID. Restricts the search to the specified :ref:`enhancer <metadata/enhancers>`.

	:returns: Associative array of all possibles URLs for this item

		* key : ``page_id::item_slug``. ``item slug`` is the URL part generate by :ref:`enhancer <metadata/enhancers>`.
		* value : Absolute URL.

.. php:method:: url($params = array())

	:param array $params:

		See :php:meth:`Orm_Behaviour_Urlenhancer::urls`.

		:canonical: If ``true``, return canonical URL of item.
		:preview: If ``true``, return even unpublished URL of item.

	:returns: Absolute URL of item or ``null`` if item can't be displayed in front.

.. php:method:: url_canonical($params = array())

	:param array $params: See :php:meth:`Orm_Behaviour_Urlenhancer::url`.
	:returns: Absolute canonical URL of item or ``null`` if item can't be displayed in front.

	Alias for ``->url(array('canonical' => true))``.

	If the item is :php:class:`sharable <Nos\\Orm_Behaviour_Sharable>`, returns the URL set in the ``shared data (content nugget)``.

	.. todo::

		Link to shared data (content nugget)

.. php:method:: preview_url()

	:returns: Absolute canonical URL of item, even if it's not published, or ``null`` if item can't be displayed in the front-office.

	Alias for ``->url_canonical(array('preview' => true))``.


.. php:method:: deleteCacheEnhancer()

     Delete the cache of the pages containing an URL enhancer for the item.
     Warning: this will delete for all the enhancer, not only the pages containing the item.


.. php:method:: htmlAnchor($attributes = array())

    :param array $attributes:
        | Array of attributes to be applied to the anchor tag.
        | If key 'href' is set in $attributes parameter:

        * if is a string, used for href attribute
        * if is an array, used as argument of ->url() method

        If key 'text' is set in $attributes parameter, its value replace item title
    :returns: Returns an HTML anchor tag with, by default, item URL in href and item title in text.

Example
*******

.. code-block:: php

	<?php
	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Orm_Behaviour_Urlenhancer' => array(
				'enhancers' => array('noviusos_monkey'),
			),
		);
	}
