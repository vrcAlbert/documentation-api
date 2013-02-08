Urlenhancer
###########

.. php:class:: Orm_Behaviour_Urlenhancer

	| For Model displayed in front by a ``URL Enhancer``.
	| Belongs to the namespace :php:ns:`Nos`

.. todo::

	Un seealso vers Enhancer et URL Enhancer

Configuration
*************

.. php:attr:: enhancers

	Required.
	Array of ``enhancers`` ID which can generate an URL for item.

	``Enhancers`` listed must define a method ``get_url_model($item, $params)``.

Methods
*******

.. php:method:: urls($params = array())

	:param array $params:

		:enhancer: Specify ``enhancer`` ID. Reduce search to the specify ``enhancer``.

	:returns: Associative array of possible URLs for this item

		* key : ``page_id::item_slug``. ``item slug`` is the URL part generate by ``enhancer``.
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

	Alias for `->url(array('canonical' => true))`.

	If item have behaviour :php:class:`Orm_Behaviour_Sharable`, return URL set in ``shared data (content nugget)``.

.. php:method:: preview_url()

	:returns: Absolute canonical URL of item, even if unpublished, or ``null`` if item can't be displayed in front.

	Alias for `->url_canonical(array('preview' => true))`.

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
