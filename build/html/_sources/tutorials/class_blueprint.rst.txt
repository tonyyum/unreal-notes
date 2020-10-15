Blueprint Class
===============

Creating Blueprint Class
------------------------

From empty
^^^^^^^^^^

Option 1 (Recommended)

Form `Content Browser` Create a folder `Blueprint` and in it right-click and select `Blue Print`

.. image:: /_static/images/blueprint_class_from_content_browser.png

Option 2

In the `Blueprints` dropdown, select `New Empty Blueprint Class`

Either way you would be presented with option for parent class. Choose `Actor`

.. image:: /_static/images/blueprint_parent_class.png

From selected object
^^^^^^^^^^^^^^^^^^^^

Select an object and click on `Blueprint/Add Script` on the World Outliner.

.. image:: /_static/images/convert_obj_to_blueprint_class.png

OR

From the blueprint dropdown, select `Convert Selection to Blueprint Class`

.. image:: /_static/images/convert_selectoin_to_blueprint_class.png

Add Components
--------------

From the component window (top left), click `+ Add Component` and use search to find what you need.

.. image:: /_static/images/add_component_to_blueprint_class.png

Example:

Box Collision
    Can be used as a trigger. Let's name it *Trigger*

Text Render
    Used for displaying text

 * Drag the exec out of text and select `Toggle Visibility`
 * Connect Enable input and Disable input to `Toggle Visibility`
 * Connect `On Component Begin Overlap` and `On Component End Overlap` to `Exec` of `Enabled Input` and `Disabled Input` respectively
 * Connect `Get Player Contrller` to `Player Controller` of `Enable Input` and `Disable Input`

 And the rest... Just see the final example.


Duplicate Blueprint Class
-------------------------

Alt and drag object to duplicate it in the view port.


Player Controller
-----------------

Insert `Get Player Controller`

Insert `Keyboard Event F`

.. image:: /_static/images/insert_keyboard_event_f_key.png

Debug
-----

You debug only one instance of Blueprint class at a time.

To see them. Change the instance at the top-right of the toolbar.

.. image:: /_static/images/debugging_instances_of_blueprint_class.png

Grouping
--------

* Left-click and drag to select nodes
* Press `c` to group and add comment
* Tip: change colour on `Comment Color` in the `Details` panel

Example
-------

.. image:: /_static/images/blueprint_class_example.png

Keyboard Shortcuts
------------------

When running game
^^^^^^^^^^^^^^^^^

Shift-F1 to regain mouse control

Reference
---------

https://www.youtube.com/watch?v=EmvekeKk-0o&t=537s