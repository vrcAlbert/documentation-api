Model_Page
##########

.. php:namespace:: Nos\Page

.. php:class:: Model_Page

	Extend :php:class:`Nos\\Orm\\Model`.

Constantes
**********

Page types
==========

.. php:const:: TYPE_CLASSIC
.. php:const:: TYPE_EXTERNAL_LINK

Values for ``page_type`` column.

External target types
=====================

.. php:const:: EXTERNAL_TARGET_NEW
.. php:const:: EXTERNAL_TARGET_SAME

Values for ``page_external_link_type`` column.

Lock types
==========

.. php:const:: LOCK_UNLOCKED
.. php:const:: LOCK_DELETION

Values for ``page_lock`` column.

Relations
*********

.. php:attr:: children

	* Relation type : :term:`has_many`.
	* Model : :php:class:`Model_Page`


.. php:attr:: parent

	* Relation type : :term:`belongs_to`.
	* Model : :php:class:`Model_Page`

Behaviours
**********

* :php:class:`Twinnable <Nos\\Orm_Behaviour_Twinnable>`
* :php:class:`Tree <Nos\\Orm_Behaviour_Tree>`
* :php:class:`Virtual path <Nos\\Orm_Behaviour_Virtualpath>`
* :php:class:`Sortable <Nos\\Orm_Behaviour_Sortable>`
* :php:class:`Publishable <Nos\\Orm_Behaviour_Publishable>`

Methods
*******

.. php:staticmethod:: link()

	:returns: Returns the href and target attributes for an HTML link ``<a>``.

.. php:staticmethod:: url($params = array())

	:param array $params:

		:preview: If set, return URL for previewed page

	:returns: The absolute URL of the page
