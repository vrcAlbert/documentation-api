API Class
##########

.. php:namespace:: Nos\Comments

.. php:class:: Api

.. php:method:: __construct($config)

    :param array $config: API configuration

.. php:method:: addComment($data)

    :param array $data:

        :ismm: Must be equal to ``anti_spam_identifier.passed`` of the :doc:`comments API configuration <../configuration/api>`.
        :id: Id of the item on which the comment was post
        :comm_email: Email of the commenter
        :comm_author: Name of the commenter
        :comm_content: Content of the comment
        :subscribe_to_comments: True if the commenter accept to receive new comments by email
        :recaptcha_challenge_field: The content of recaptcha challenge field
        :recaptcha_response_field: The content of recaptcha response field

    :returns: ``True`` if comment is added, ``false`` if not passed recaptcha, 'none' if not passed anti spam.

.. php:method:: sendNewCommentToAuthor(Model_Comment $comment)

    :param Model_Comment $comment: The new comment

.. php:method:: sendNewCommentToCommenters(Model_Comment $comment)

    :param Model_Comment $comment: The new comment

.. php:method:: getConfig()

    :returns: the API configuration.

.. php:method:: getRssComment($comment)

    :param $comment: Comment item

    :returns: An array (to be used with :php:class:`Nos\\Tools_RSS`)

.. php:method:: getRss($options = array())

    :param array $options: If no key ``item``, returns all comments of the model for the current context.

        :item: A :php:class:`Nos\\Orm\\Model` instance. If set, returns all comments of the item.

    :returns: A :php:class:`Nos\\Tools_RSS` instance.

.. php:method:: changeSubscriptionStatus($from, $email, $subscribe)

    :param string $from: A :php:class:`Nos\\Orm\\Model` instance
    :param string $email: Email of the commenter to change the subscription status
    :param boolean $subscribe: New subscription status (true to receive notifications, false to disable)

