Mapping Blueprint To C++
========================

Finding out the function name
-----------------------------

To go from a Blueprint function to C++ function.

1. Hover over target and we see Scene Component.

2. In VS Ctrl+, and type in SceneComponent.h

3. search for `GetWorldLocation` and we'll see the below

.. code-block:: cpp

	/** Return location of the component, in world space */
	UFUNCTION(BlueprintCallable, meta=(DisplayName = "GetWorldLocation", ScriptName = "GetWorldLocation"), Category="Utilities|Transformation")
	FVector K2_GetComponentLocation() const;

4. F12 on `K2_GetComponentLocation` and we'll see the below. Now we've mapped BP `GetWorldLocation` to C++ `GetComponentLocation`

.. code-block:: cpp

    FVector USceneComponent::K2_GetComponentLocation() const
    {
        return GetComponentLocation();
    }

Similarly we can do the same with `KismetMathLibrary.h` and look for `GetForwardVector` and we'd find:

.. code-block:: cpp

	/** Rotate the world forward vector by the given rotation */
	UFUNCTION(BlueprintPure, meta=(ScriptMethod = "GetForwardVector", Keywords="rotation rotate"), Category="Math|Vector")
	static FVector GetForwardVector(FRotator InRot);

If we F12 on GetForwardVector we'll see this.

.. code-block:: cpp

    FVector UKismetMathLibrary::GetForwardVector(FRotator InRot)
    {
        return InRot.Vector();
    }

Now we realised that we can simplify the code:

.. code-block:: cpp

    FVector UGrabber::GetMaxGrabLocation() const
    {
        return GetComponentLocation() + UKismetMathLibrary::GetForwardVector(GetComponentRotation()) * MaxGrabDistance;
    }

In to:

.. code-block:: cpp

    FVector UGrabber::GetMaxGrabLocation() const
    {
        return GetComponentLocation() + GetComponentRotation().Vector() * MaxGrabDistance;
    }


    FVector UGrabber::GetMaxGrabLocation() const
    {
        return GetComponentLocation() + UKismetMathLibrary::GetForwardVector(GetComponentRotation()) * MaxGrabDistance;
    }

Common Includes
---------------

+----------------------+------------------------------+
| Class                | #include                     |
+======================+==============================+
| UWorld               | Engine/World.h               |
+----------------------+------------------------------+
| AActor               | GameFramework/Actor.h        |
+----------------------+------------------------------+
| UActorComponent      | Components/ActorComponents.h |
+----------------------+------------------------------+
| UGameplayStatics     | Kismet/GameplayStatics.h     |
+----------------------+------------------------------+
| UKismetSystemLibrary | Kismet/KismetSystemLibrary.h |
+----------------------+------------------------------+
| FMath                | Math/UnrealMathUtility.h     |
+----------------------+------------------------------+

Converting GetPhysicsComponent
------------------------------

1. Add #include to Grabber.h. Note: it has to go before `Grabber.generated.h` as that has to be the last #include.

.. code-block:: cpp

    #include "PhysicsEngine/PhysicsHandleComponent.h"

2. Add function declaration:

.. code-block:: cpp

	UFUNCTION(BlueprintCallable, BlueprintPure)
	FVector GetPhysicsComponent() const;

3. Add #include to Grabber.cpp

.. code-block:: cpp

    #include "GameFramework/Actor.h"


4. Add function definition:

.. code-block:: cpp

    UPhysicsHandleComponent* UGrabber::GetPhysicsComponent() const
    {
        return GetOwner()->FindComponentByClass<UPhysicsHandleComponent>();
    }

5. As usual, delete GetPhysicsComponent BP function and recompile
