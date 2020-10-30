Exposing Variables
==================

1. Add the Macro following to MaxGrabDistance

.. code-block:: cpp

    protected:
        UPROPERTY(EditAnywhere, BlueprintReadOnly)
        float MaxGrabDistance = 100;

2. Ctrl-Shift-B to build.

3. Go back to Grabber Blueprint and compile.

4. Right click on MaxGrabDistance_0 find referene and we see that it is used only in 1 place

5. Delete the MaxGrabDistance_0 variable and replace it with MaxGrabDistance (drag wire out from the `X` box)

.. image:: /_static/images/replace_max_grab_distance.PNG

6. Fly next to a pumpkin, right click anywhere and select `Play from here` and make sure that grabber still works