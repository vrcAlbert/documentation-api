Behaviours
##########

.. toctree::
	:glob:

	*


Printer friendly
****************

============= ================================ ===============================================================================
Behaviour     Configuration                    Methods
============= ================================ ===============================================================================
Publishable   * publication_bool_property      * ->published()
Sortable      * sort_property                  * ->move_before($item)
              * sort_order                     * ->move_after($item)
                                               * ->move_to_last_position()
Contextable   * context_property               * ->get_context()
              * default_context
Twinnable     * common_id_property             * ->delete_all_context()
              * is_main_property               * ->is_main_context()
              * context_property               * ->find_context($context)
              * default_context                * ->find_main_context()
                                               * ->find_other_context($filter)
                                               * ->get_all_context()
                                               * ->get_other_context($filter)
Tree          * level_property                 * ->get_parent()
              * parent_relation                * ->set_parent($new_parent)
              * children_relation              * ->find_children($where = array(), $order_by = array(), $options = array())
                                               * ->find_children_recursive($include_self)
                                               * ->find_root()
Urlenhancer   * enhancers                      * ->urls($params = array())
                                               * ->url($params = array())
                                               * ->url_canonical($params = array())
                                               * ->preview_url()
Virtualname   * virtual_name_property          * ->virtual_name()
              * unique                         * ::friendly_slug($slug)
Virtualpath   * virtual_name_property          * ->virtual_path($dir = false)
              * virtual_path_property          * ->extension()
              * unique
              * extension_property
              * parent_relation
Sharable      * data                           * ->get_default_nuggets()
                                               * ->get_catcher_nuggets($catcher)
                                               * ->data_catchers()
============= ================================ ===============================================================================
