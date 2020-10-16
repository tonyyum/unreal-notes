Level Editor Component Workflow
===============================

Create the Actor
----------------

Empty Actor
^^^^^^^^^^^

In `Place Actor` choose `Basic` and drag `Empty Actor` to the viewport.

.. image:: /_static/images/empty_actor.png

Add the Bush
^^^^^^^^^^^^

In the `Content Browser` go to `Content > StarterContent > Props` and drag `SM_Bush` into the Empty Actor's component.

.. image:: /_static/images/putting_bush_inside_empty_actor.png

Drag the `SM_Bush` upward and replace `DefaultSceneRoot`

Add the fire
^^^^^^^^^^^^

Click `+ Add Component` select `Particle System` and rename to `Fire`

Under `Template` change `None` to `P_Fire`

.. image:: /_static/images/change_ps_template_to_fire.png

Uncheck the `Auto Activate`

.. image:: /_static/images/uncheck_auto_activate.png

Trigger Box
^^^^^^^^^^^

Click `+ Add Component` Choose `Box Collision` and rename it to `TriggerBox`

Adjust the box to contain the `SM_Bush`

Create Blueprint
----------------

Click on `Blueprint/Add Script`:

.. image:: /_static/images/convert_obj_to_blueprint_class.png

Choose `/Game/Blueprint/BurningBush_BP`

.. image:: /_static/images/create_burningbush_bp.png

Event Scripting
---------------

1. Select `TriggerBox` and click on add `On Component Begin Overlap`

2. Create reference to `Fire`

3. Connect fire to `Activate`

.. image:: /_static/images/connect_fire_to_activate.png

4. Connect `On Component Begin OVerlap` to `Activate`

Bush Blueprint
--------------

.. image:: /_static/images/bush_blueprint.png

Blueprint from existing objects
-------------------------------

Select walls, `TriggerBox` and `PointLight`.

.. image:: /_static/images/select_walls_triggerbox_pointlight.png

Under `Blueprint` select `Convert Selection to Blueprint Class...`

.. image:: /_static/images/convert_selectoin_to_blueprint_class.png

Redo event scripting, make a few houses and they all behaves the same.

Click on `Save All` under the `Content Browser`

.. image:: /_static/images/save_all.png


Reference
---------

https://www.youtube.com/watch?v=mHfiAOlZZRQ