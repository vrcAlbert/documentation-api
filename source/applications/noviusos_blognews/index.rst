Blog/News Application
#####################

To modify configuration of Blog or News, extend respectively configuration files :file:`noviusos_blog::config` or :file:`noviusos_news::config`.

Configuration
*************

:categories:
    :enabled:  Boolean, ``true`` to enable categories. Default ``true`` for Blog and News.
    :show:     Boolean, ``true`` to show categories in front. Default ``true`` for Blog and News.
:tags:
    :enabled:  Boolean, ``true`` to enable tags. Default ``true`` for Blog and ``false`` for News.
    :show:     Boolean, ``true`` to show tags in front. Default ``true`` for Blog and News.
:authors:
    :enabled:  Boolean, ``true`` to enable authors. Default ``true`` for Blog and ``false`` for News.
    :show:     Boolean, ``true`` to show authors in front. Default ``true`` for Blog and News.
:summary:
    :enabled:  Boolean, ``true`` to enable summary. Default ``true`` for Blog and News.
    :show:     Boolean, ``true`` to show summary in front. Default ``true`` for Blog and News.
:comments:
    :enabled:  Boolean, ``true`` to enable comments. Default ``true`` for Blog and ``false`` for News.
    :show:     Boolean, ``true`` to show comments in front. Default ``true`` for Blog and News.
    :show_nb:  Boolean, ``true`` to show the number of comments in front. Default ``true`` for Blog and News.
    :can_post: Boolean, ``true`` if user can post new comments. Default ``true`` for Blog and News.
:publication_date:
    :enabled:  Boolean, ``true`` to enable publication dates. Default ``true`` for Blog and News.
    :show:     Boolean, ``true`` to show publication dates in front. Default ``true`` for Blog and News.
:thumbnail:
    :front:
        :list:
            :link_to_item: Boolean, ``true`` if you want a link to item on the thumbnail. Default ``true`` for Blog and News.
            :max_width:    Integer, width in pixels of the thumbnail. Default ``120`` for Blog and News.
        :item:
            :link_to_fullsize: Boolean, ``true`` if you want a link to fullsize image on the thumbnail. Default ``true`` for Blog and News.
            :max_width:        Integer, width in pixels of the thumbnail. Default ``200`` for Blog and News.
