Blueprint Events to C++
===========================

BlueprintImplementableEvent
---------------------------

Add NotifyQuestActor to Grabber.h

.. code-block:: cpp

	UFUNCTION(BlueprintCallable, BlueprintImplementableEvent)
	void NotifyQuestActor(AActor* Actor);


You could now replace the BluePrint event with the C++ equivalent.

BlueprintNativeEvent
--------------------

1. In Blueprint rename `TraceForPhysicsBodies` to `BP_TraceForPhysicsBodies`

2. In Grabber.h add UFUNCTION

Notice that the BP function returns 3 values. In C++ we'll return 1 and use output parameters for the other 2.

.. image:: /_static/images/trace_for_physics_bodies_return.PNG

.. code-block:: cpp

    UFUNCTION(BlueprintCallable, BlueprintNativeEvent)
	bool TraceForPhysicsBodies(AActor*& HitActor, UPrimitiveComponent*& HitComponent);

3. In Grabber.cpp add implementation, note the name has `_Implementation` as suffix

.. code-block:: cpp

	bool UGrabber::TraceForPhysicsBodies_Implementation(AActor*& HitActor, UPrimitiveComponent*& HitComponent)
	{
		return false;
	}

4. Override `TraceForPhysicsBodies` in Blueprint:

.. image:: /_static/images/override_trace_for_physics_bodies.PNG

5. Replace reference of `BP_TraceForPhysicsBodies` with `TraceForPhysicsBodies` and then delete `BP_TraceForPhysicsBodies`.



