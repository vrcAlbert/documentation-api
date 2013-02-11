Model_Page
##########

.. php:class:: Model_Page

	| Extend :php:class:`Model`.
	| Belongs to the namespace :php:ns:`Nos/Page`

Constantes
**********

Page types
==========

.. php:const:: TYPE_CLASSIC
.. php:const:: TYPE_EXTERNAL_LINK

External target types
=====================

.. php:const:: EXTERNAL_TARGET_NEW
.. php:const:: EXTERNAL_TARGET_SAME

Lock types
==========

.. php:const:: LOCK_UNLOCKED
.. php:const:: LOCK_DELETION

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

* :php:class:`Twinnable <Orm_Behaviour_Twinnable>`
* :php:class:`Tree <Orm_Behaviour_Tree>`
* :php:class:`Virtual path <Orm_Behaviour_Virtualpath>`
* :php:class:`Sortable <Orm_Behaviour_Sortable>`
* :php:class:`Publishable <Orm_Behaviour_Publishable>`

Methods
*******

.. php:staticmethod:: link()

	:returns: Returns the href and target attributes for an HTML link <a>.

.. php:staticmethod:: url($params = array())

	:params array $params:

		:preview: If set, return URL for previewed page

	:returns: The absolute URL of the page
