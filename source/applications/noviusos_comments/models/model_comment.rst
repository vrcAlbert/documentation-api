Model Comment
#############

.. php:namespace:: Nos\Comments

.. php:class:: Model_Comment

	Extends :php:class:`Nos\\Orm\\Model`.

Methods
*******

.. php:method:: getRelatedItem()

    Retrieves the instance of the related item model, if it exists.

    :returns: Returns the Model instance, if it exists

.. php:method:: changeSubscriptionStatus($from, $email, $subscribe)

    Changes the user subscription status to new comments on an item.

    :param Nos\\Orm\\Model $from: Related item
    :param string $email: The user's email address
    :param boolean $subscribe: false to disable the subscription, true to enabled it
