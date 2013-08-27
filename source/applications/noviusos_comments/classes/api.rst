API Class
##########

.. php:namespace:: Nos\Comments

.. php:class:: Api

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

.. php:method:: getRss($options = array())

    :param array $options: If no key ``item``, return all comments of the model for the current context.

        :item: A :php:class:`Nos\\Orm\\Model` instance. If set, return all comments of the item.

    :returns: A :php:class:`Nos\\Tools_RSS` instance.

.. php:method:: changeSubscriptionStatus($from, $email, $subscribe)

    :param string $from: A :php:class:`Nos\\Orm\\Model` instance
    :param string $email: Password to check if it matches the user's password
    :param boolean $subscribe: Password to check if it matches the user's password

