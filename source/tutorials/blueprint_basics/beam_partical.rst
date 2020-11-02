Beam Partical
=============

Material
--------

1. Create folder `Material`

2. Create material `Lighting_M`

3. In `Material` change `Blender Mode` to `Translucent` and `Shading model` to `Unlit`

.. image:: /_static/images/beam_material.PNG

4. Create `Particle Color` and connect to `Lighting_M`

5. Creat `RadialGradientExponential`

6. Hold `M` and left click to create `Multiply`

7. Multiply `Particle Color` with `RadialGradientExponential` and connect result to `opacity` of `Lighting_M`


After clicking on `Apply`:

.. image:: /_static/images/apply_material.PNG

The result should look like the below:

.. image:: /_static/images/beam_material_final.PNG

Partical System
---------------

1. Add `Partical System` and name it `Lighting_P`

2. Click on `required` tab

.. image:: /_static/images/partical_system_required.PNG

3. Drag `Lighting_M` into material

.. image:: /_static/images/partical_system_material.PNG

4. Drag Partical system to world.

5. Right click `DataType` and select `New Beam Data`

.. image:: /_static/images/new_beam_data.PNG

6. Delete `Color over life`

.. image:: /_static/images/color_over_life.PNG

7. Right click `Color` and select `Initial Color`

8. Right Click, Bean and add `Source` and `Target`

9. Set `Souce Method` to `Actor`, `Source Name` to `BeamSource`

10. Set `Target Method` to `Actor`, `Target Name` to `BeamTarget`

11. Go back to world, select particle system and add two instance parameters with names given in previous steps.
    `Param Type` is `Actor` and use the eye drop icon to select the actor from world.

.. image:: /_static/images/beam_instance_param.PNG

12. Go back to particle sytem editor and change `Lifetime` to 0. 

.. image:: /_static/images/beam_lifetime_zero.PNG

13. Delete `Initial Velocity`

14. Select `Beam Data` and set `Speed` to 0

