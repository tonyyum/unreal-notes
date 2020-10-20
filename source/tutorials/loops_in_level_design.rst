Loops in Level Design
=====================

1. Create Blueprint `ProceduralWall`

2. Drag `Pillar_50x500` from `Content Browser/StarterContent/Architecture` to new Blueprint

3. Create a new variable

  a. Name it `EndPoint`

  b. Variable Type = `Vector`

  c. check `Instance Editable`

  d. Tooltip = This is the end of the wall!

  e. check `Show 3D Widget`

.. image:: /_static/images/endpoint_variable.png


4. Drag `EndPoint` to `Construction Script`. Create a getter.

5. Drag `EndPoint` slot out and create `Not Equal (Vector)` by typing in `!`

.. image:: /_static/images/endpoint_not_eq.png

6. create `Branch` from `Not Equal (Vector)`

7. Connect `Construction Script` to `Branch`

8. Create a vector multiply in between `End Point` and `Not Equal` (search with `*`)

etc, etc... See example.

Example
-------

Summary
^^^^^^^

.. image:: /_static/images/level_design_loop_example_summary.PNG

Run Loop
^^^^^^^^

.. image:: /_static/images/level_design_loop_example_run_loop.PNG

Wall Meshes
^^^^^^^^^^^

.. image:: /_static/images/level_design_loop_example_wall_meshes.PNG

Rotate Wall
^^^^^^^^^^^

.. image:: /_static/images/level_design_loop_example_wall_rotate.PNG



Reference
---------

https://www.youtube.com/watch?v=kmnC6IUPGjI&t=26s