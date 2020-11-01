BlueprintCallable UFUNCTION
===========================

Type Mapping
------------

Mapping Fundamental Types
^^^^^^^^^^^^^^^^^^^^^^^^^

+-----------+--------+
| Blueprint |  C++   |
+===========+========+
| Float     | float  |
+-----------+--------+
| \-        | double |
+-----------+--------+
| Integer   | int32  |
+-----------+--------+
| \-        | uint32 |
+-----------+--------+
| Integer64 | int64  |
+-----------+--------+
| \-        | uint64 |
+-----------+--------+
| Bool      | bool   |
+-----------+--------+

Mapping Utility Types
---------------------

Blueprint   FString

+-----------+-----------+
| Blueprint |  C++      |
+===========+===========+
| String    | FString   |
+-----------+-----------+
| Name      | FName     |  
+-----------+-----------+
| Vector    | FVector   |
+-----------+-----------+
| Rotator   | FRotator  |
+-----------+-----------+
| Transform | FTransform|
+-----------+-----------+

Mapping Object Types
--------------------

+----------------+-----------------+
| Blueprint      |  C++            |
+================+=================+
| Object         | UObject*        |
+----------------+-----------------+
| Actor          | AActor*         |
+----------------+-----------------+
| ActorComponent | UActorComponent*|
+----------------+-----------------+

Creating C++ Function
---------------------

Add to Grabber.h the below:

.. code-block:: cpp

	UFUNCTION(BlueprintCallable, BlueprintPure)
	FVector GetMaxGrabLocation() const;

Ctrl+. and create definition.

.. image:: /_static/images/quick_actions.PNG

.. image:: /_static/images/create_definition.PNG

Also tip: Ctrl-K Ctrl-O to swtich between .cpp and .h

Add the #include:

.. code-block:: cpp

    #include "Kismet/KismetMathLibrary.h"


Add the code:

.. code-block:: cpp

    FVector UGrabber::GetMaxGrabLocation() const
    {
        return GetComponentLocation() + UKismetMathLibrary::GetForwardVector(GetComponentRotation()) * MaxGrabDistance;
    }


Ctrl-Shift-B to compile and we'll see the blueprint now complains because grabber already exists.

.. image:: /_static/images/Grabber_already_exist_error.PNG

Now check references and see that all references have already been replaced with the C++ version.
Simply delete the Blueprint version and compile.

Now you should still be able to grab the pumpkin, but we have replaced the BP function with a C++ one.


