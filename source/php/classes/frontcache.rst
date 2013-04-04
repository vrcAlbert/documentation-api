.. _php/classes/frontcache:

FrontCache
##########

.. php:namespace:: Nos

.. php:class:: FrontCache

	Manage front cache

Methods
*******

.. php:staticmethod:: callHmvcUncached($uri, $args = array())

    Write a HMVC call in cache for after cache execution.

    :param string $uri: Route for the request.
    :param array $args: The method parameters.

    .. seealso:: :php:meth:`Nos\\Nos::hmvc`

.. php:staticmethod:: viewForgeUncached($file = null, $data = null, $auto_filter = null)

    Write a View forge in cache for after cache execution.

    :param string $file: The view filename
    :param array $data: Array of values
    :param boolean $auto_filter: Set to true or false to set auto encoding

