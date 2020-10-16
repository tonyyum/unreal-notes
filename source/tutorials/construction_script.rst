Construction Script
===================

Choose to `Construction Script` tab.

.. image:: /_static/images/construction_script_tab.png

Variables
---------

Right click on a slot and choose `Promote to Varaible`

Note: It is also possible to click on `+ Variable` in the `My Blueprint` panel.

.. image:: /_static/images/promote_to_variable.png

Change the `Variable Name` from the under `Variable` in `Details` panel.

You'll see a message saying `Please compile the blueprint`. So go ahead and compile.

Go to existing light, drag and drop to save colour. 

Go back to the variable and you can now select that same colour in `Default Color`.

Check the instance editable:

.. image:: /_static/images/instance_editable.png

Private vs Public Varriable
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The eye icon on the right of the variable shows whether it is public or private.

.. image:: /_static/images/private_vs_public_variable.png

Tooltip
^^^^^^^

On the `Details` panel, you could enter the tooltip for the variable.

Changing instances of a class
-----------------------------

With the construction script setup, you could now change the default colour per light in the viewport.

Next to allow turning light on and off per instance:

1. Create `Set Visibility`
2. Connect `Spot Light` to `Target`
3. Connect `Set Light Color` to `Exec`
4. Promote `New Visibility` to variable and name it `VisibilitySetting`
5. Set `Tooltip` for variable to `Turn on off the light`

You can now choose the default setting per light.

Example
-------

.. image:: /_static/images/construction_script_example.png