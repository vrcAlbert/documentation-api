Tabs
####


.. _javascript_tabs_add:

Add
---

.. js:function:: $(context).nosTabs('add', options[, where]);

    Opens a new tab in Novius OS.

    :param string method: 'add'
    :param object options: See below
    :param string where: 'end' (default). Use 'before' or 'after' to open next to current tab.

    Options list

    :param string url: URL for the tab. Mandatory
    :param string label: Label for the tab
    :param bool labelDisplay: Default true. Should the label be displayed?
    :param string iconUrl: Icon URL
    :param int iconSize: Which size is the icon? 16 or 32 are common values.

.. js:attribute:: test


Open
----

.. js:function:: $(context).nosTabs('open', options);

    Opens a new tab, or re-focus another one with the same URL, if found.

.. seealso::

	:ref:`nosTabs('open') <javascript_tabs_add>`