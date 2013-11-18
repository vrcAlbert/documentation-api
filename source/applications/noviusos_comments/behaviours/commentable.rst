.. _applications/noviusos_comments/behaviours/commentable:

Behaviour Commentable
#####################

.. php:namespace:: Nos\Comments

.. php:class:: Orm_Behaviour_Commentable

	Adds the ability to use the Comment API on an a :php:class:`Nos\\Orm\\Model`.

Methods
*******

.. php:staticmethod:: commentApi()

	:returns: An instance of :class:`Nos\\Comments\\Api``, configured for this item.

.. php:method:: count_comments()

    Returns and caches the number of comments related to one item
	:returns: Number of comments

.. php:method:: setNbComments($nb)

    Allow to enter a custom cached number of comments related to the item. Can be
    useful when adding or removing a comment for instance.
	:param $nb: number of comments

.. php:staticmethod:: count_multiple_comments($items)

    From a items' list, retrieve the number of comments in an optimal way.
	:param $items


Relations
*********

This behaviour adds a **comments** relation to retrieve all the published comments of the Model.

Others
******

* This behaviours adds a **Comments** action on the Model's App Desk, which will open a tab listing all the comments of the item.

* This behaviours adds a **Comments** column in the App Desk, containing the number of comments for each item.

Example
*******

.. code-block:: php

	<?php

	class Model_Monkey extends \Nos\Orm\Model
	{
		protected static $_behaviours = array(
			'Nos\Comments\Orm_Behaviour_Commentable' => array(
			),
		);
	}
