
.. _php/events:

Events
######


Configuration
*************

.. _events_configuration:


config|<path>
=============

.. php:function:: config|<path>($config)

    A configuration file is loaded.

    :param array &$config: The loaded array from the file

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|nos::controller/admin/page/page', function(&$config)
        {
            // ...
        }
        // Triggering the event
        $config = Config::load('nos::controller/admin/page/page', true);


    Also works with absolute paths :

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|/data/www/novius-os/local/config/test.php', function(&$config)
        {
            // ...
        }
        // Triggering the event (file must exists)
        $config = Config::load('/data/www/novius-os/local/config/test.php', true);


config|<group>
==============


.. php:function:: config|<group>($config)

    A configuration array is loaded.

    :param array &$config: The loaded array

    .. code-block:: php

        <?php

        // Listening to the event
        Event::register_function('config|group', function(&$config)
        {
            // ...
        }
        // Triggering the event
        Config::load(array(), 'group');


.. _php/events/front-office:

Front-office (website)
**********************


front.start
===========

.. php:function:: front.start($params)

    An .html page is requested.

    :param array $params:

        :&$url: ``string``  Current URL (without leading domain, with trailing .html)
        :&$cache_path: ``string``  Which entry should be checked / written in the cache

    .. code-block:: php

        <?php

        Event::register_function('front.start', function($params)
        {
            $url =& $params['url'];
            $cache_path =& $params['cache_path'];
            // ...
        });


front.parse_wysiwyg
===================

.. php:function:: front.parse_wysiwyg($html)

    Additional processing on a WYSIWYG (HTML content).

    :param string $html: HTML content, already pre-processed by the core

    .. code-block:: php

        <?php

        Event::register_function('front.parse_wysiwyg', function(&$content)
        {
            // ...
        });


front.display
=============

.. php:function:: front.display($html)

    Additional processing on the page (HTML content).

    :param string $html: HTML content of the page (will be written in the cache)

    .. code-block:: php

        <?php

        Event::register_function('front.display', function(&$html)
        {
            // ...
        });

front.pageFound
=================

.. php:function:: front.pageFound($params)

    Page to display have been found.

    :param array $params:

        :$page: :php:class:`Nos\\Page\\Model_Page`

    .. code-block:: php

        <?php

        Event::register('front.pageFound', function($params)
        {
            $page = $params['page'];
            // ...
        });


front.response
==============

.. php:function:: front.response($params)

    Before that the response be sended.

    :param array $params:

        :&$content: ``string``  The response body
        :&$status: ``int``  The HTTP response status for this response
        :&$headers: ``array``  HTTP headers for this response

    .. code-block:: php

        <?php

        Event::register_function('front.response', function($params)
        {
            $content =& $params['content'];
            $status =& $params['status'];
            $headers =& $params['headers'];
            // ...
        });

front.404NotFound
=================

.. php:function:: front.404NotFound($params)

    An .html page was requested, but not found.

    :param array $params:

        :$url: ``string``  Current URL (without leading domain, with trailing .html)

    .. code-block:: php

        <?php

        Event::register('front.404NotFound', function($params)
        {
            $url = $params['url'];
            // ...
        });

404 entry point
***************

.. versionadded:: 0.2.0.2

404.start
===========

.. php:function:: 404.start($params)

    A inexistant file is requested. Can be media or attachment file.

    :param array $params:

        :&$url: ``string``  URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register_function('404.start', function($params)
        {
            $url =& $params['url'];
            // ...
        });

.. _php/events/404.mediaFound:

404.mediaFound
=================

.. php:function:: 404.mediaFound($params)

    Media to send have been found.

    :param array $params:

        :$url: ``string``  The requested URL
        :$media: :php:class:`Nos\\Media\\Model_Media`
        :&$send_file: ``string``  The path of the file to be sent

    .. code-block:: php

        <?php

        Event::register_function('404.mediaFound', function($params)
        {
            $url = $params['url'];
            $media = $params['media'];
            $send_file =& $params['send_file'];
            // ...
        });

404.mediaNotFound
=================

.. php:function:: 404.mediaNotFound($url)

	A inexistant media file is requested.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.mediaNotFound', function($url)
        {
            // ...
        });

.. _php/events/404.attachmentFound:

404.attachmentFound
===================

.. php:function:: 404.attachmentFound($params)

    Attachment file to send have been found.

    :param array $params:

        :$url: ``string``  The requested URL
        :$attachement: :php:class:`Nos\\Attachment`
        :&$send_file: ``string``  The path of the file to be sent

    .. code-block:: php

        <?php

        Event::register_function('404.attachmentFound', function($params)
        {
            $url = $params['url'];
            $attachement = $params['attachement'];
            $send_file =& $params['send_file'];
            // ...
        });

404.attachmentNotFound
======================

.. php:function:: 404.attachmentNotFound($url)

	A inexistant attachment file is requested.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.attachmentNotFound', function($url)
        {
            // ...
        });


404.end
=======

.. php:function:: 404.end($url)

	A inexistant file is requested. No attachment or media file matched the URL.

    :param string $url: URL requested (without leading domain)

    .. code-block:: php

        <?php

        Event::register('404.end', function($url)
        {
            // ...
        });


Back-office
***********

.. _php/events/admin.loginSuccess:

admin.loginSuccess
==================

.. php:function:: admin.loginSuccess()

    A user just successfully connected to the back-office.

    .. code-block:: php

        <?php

        Event::register('admin.loginSuccess', function()
        {
            // ...
        });

.. _php/events/admin.loginFail:

admin.loginFail
==================

.. php:function:: admin.loginFail()

    A user is trying to connect to the back-office with an email or an invalid password.

    .. code-block:: php

        <?php

        Event::register('admin.loginFail', function()
        {
            // ...
        });

.. _php/events/admin.loginSuccessWithCookie:

admin.loginSuccessWithCookie
============================

.. php:function:: admin.loginSuccessWithCookie()

    A user just successfully re-connected to the back-office using the cookie.

    .. code-block:: php

        <?php

        Event::register('admin.loginSuccessWithCookie', function()
        {
            // ...
        });

.. _php/events/admin.loginFailWithCookie:

admin.loginFailWithCookie
=========================

.. php:function:: admin.loginFailWithCookie()

    A user has failed to connect to the back-office using the cookie.

    .. code-block:: php

        <?php

        Event::register('admin.loginFailWithCookie', function()
        {
            // ...
        });


.. _php/events/email:

Emails
******


email.before_send
=================

.. php:function:: email.before_send($email)

    Before sending an email.

    :param object $email: Email_Driver instance

    .. code-block:: php

        <?php

        Event::register('email.before_send', function($email)
        {
            // ...
        }


email.after_send
================

.. php:function:: email.after_send($email)

    After a mail was sent.

    :param object $email: Email_Driver instance

    .. code-block:: php

        <?php

        Event::register('email.after_send', function($email)
        {
            // ...
        }

email.error
================

.. php:function:: email.error($params)

    On email send error.

    :param object $params: Email_Driver instance

        :$email: The email driver object
        :$exception: The exception object

        .. code-block:: php

            <?php

            Event::register('email.error', function($params)
            {
                $email = $params['email'];
                $exception = $params['exception'];
                // ...
            }

Deprecated
**********

.. _php/events/nos.deprecated:

nos.deprecated
==============

.. php:function:: nos.deprecated($params)

    A deprecated message will be write in log.

    :param array $params:

            :$message: The message to log.
            :$since: The version since deprecation.
            :$debug_backtrace: The debug_backtrace

    .. code-block:: php

        <?php

        Event::register('nos.deprecated', function($params)
        {
            $message = $params['message'];
            $since = $params['since'];
            $debug_backtrace = $params['debug_backtrace'];
            // ...
        });

Migration
**********

.. _php/events/migrate.exception:

migrate.exception
=================

.. php:function:: migrate.exception($params)

    A migration throw an exception. Exception propagation can be stopped.

    :param array $params:

        :$e: The exception object
        :&$ignore: ``boolean`` If the event change is value to ``true``, the exception will not be propagated.
        :$migration: ``array``  The migration array

    .. code-block:: php

        <?php

        Event::register_function('migrate.exception', function($params)
        {
            $e = $params['e'];
            $ignore = $params['ignore'];
            $migration =& $params['migration'];
            // ...

            $ignore = true; // The exception will not be propagated
        });
