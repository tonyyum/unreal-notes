Binding User Input
==================

Creating FirstPersonCharacter C++ Class
---------------------------------------

Find BP_FirstPersonCharacter from Content -> Core

.. image:: /_static/images/bp_first_person_character.PNG

Create new C++ class deriving Character and name it FirstPersonCharacter.

Reparent the existing BP_FirstPersonCharacter to FirstPersonCharacter.

Forward Axis
------------

In the FirstPersonCharacter.h add:

.. code-block:: cpp

    private:
        void Forward(float AxisValue);

In FirstPersonCharacter.cpp add:

include:

.. code-block:: cpp

    #include "Components/InputComponent.h"

And add the following functions:

.. code-block:: cpp

    // Called to bind functionality to input
    void AFirstPersonCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
    {
        Super::SetupPlayerInputComponent(PlayerInputComponent);
        PlayerInputComponent->BindAxis(TEXT("Forward"), this, &AFirstPersonCharacter::Forward);
    }

    void AFirstPersonCharacter::Forward(float AxisValue)
    {
        UE_LOG(LogTemp, Warning, TEXT("Forward %f"), AxisValue);
    }

We know to BindAxis Forward because we can see it in the input event of BP_FirstPersonCharacter

You can also see the Axis and Inputs from Settings -> Project Setting. Then select Input.

.. image:: /_static/images/engine_input.PNG


Now delete the graph related to Forward, compile

Window -> Developer Tool -> Output Log

Run the game and we should see that pressing Forward
no longer walks forward. But rather it prints to the log.

Jump Action
-----------

Now create jump function.

FirstPersonCharacter.h

.. code-block:: cpp

	void Jump();

FirstPersonCharacter.cpp

.. code-block:: cpp

    void AFirstPersonCharacter::Jump()
    {
        UE_LOG(LogTemp, Warning, TEXT("Jump"));
    }

Now create add to AFirstPersonCharacter::SetupPlayerInputComponent

.. code-block:: cpp

	PlayerInputComponent->BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &AFirstPersonCharacter::Jump);

To know about EInputEvent, hit F12 and you'll see the available events.

.. code-block:: cpp

    UENUM( BlueprintType, meta=(ScriptName="InputEventType"))
    enum EInputEvent
    {
        IE_Pressed              =0,
        IE_Released             =1,
        IE_Repeat               =2,
        IE_DoubleClick          =3,
        IE_Axis                 =4,
        IE_MAX                  =5,
    };


Compile, remove jump in Blueprint event graph, compile blueprint, run to see Jump being logged.

Binding the rest
----------------

In Grabber.h add Grab and release with implementation in Grabber.cpp

.. code-block: cpp

    void UGrabber::Grab()
    {
        AActor* HitActor;
        UPrimitiveComponent* HitComponent;
        if (TraceForPhysicsBodies(HitActor, HitComponent))
        {
            HitComponent->SetSimulatePhysics(true);
            GetPhysicsComponent()->GrabComponentAtLocationWithRotation(
                HitComponent,
                NAME_None,
                HitComponent->GetCenterOfMass(),
                FRotator()
            );
            NotifyQuestActor(HitActor);
        }
    }

    void UGrabber::Release()
    {
        GetPhysicsComponent()->ReleaseComponent();
    }

Add to FirstPersonCharacter.cpp the include

.. code-block:: cpp

    #include "GameFramework/CharacterMovementComponent.h"

Bind the rest of inputs

.. code-block:: cpp

    // Called to bind functionality to input
    void AFirstPersonCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
    {
        Super::SetupPlayerInputComponent(PlayerInputComponent);
        PlayerInputComponent->BindAxis(TEXT("Forward"), this, &AFirstPersonCharacter::Forward);
        PlayerInputComponent->BindAxis(TEXT("Right"), this, &AFirstPersonCharacter::Right);
        PlayerInputComponent->BindAxis(TEXT("LookUp"), this, &APawn::AddControllerPitchInput);
        PlayerInputComponent->BindAxis(TEXT("LookRight"), this, &APawn::AddControllerYawInput);
        PlayerInputComponent->BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &ACharacter::Jump);
        PlayerInputComponent->BindAction(TEXT("Grab"), EInputEvent::IE_Pressed, this, &AFirstPersonCharacter::Grab);
        PlayerInputComponent->BindAction(TEXT("Release"), EInputEvent::IE_Pressed, this, &AFirstPersonCharacter::Release);
    }

    void AFirstPersonCharacter::Forward(float AxisValue)
    {
        GetCharacterMovement()->AddInputVector(GetActorForwardVector() * AxisValue);
    }

    void AFirstPersonCharacter::Right(float AxisValue)
    {
        GetCharacterMovement()->AddInputVector(GetActorRightVector() * AxisValue);
    }

    void AFirstPersonCharacter::Grab()
    {
        GetGrabber()->Grab();
    }

    void AFirstPersonCharacter::Release()
    {
        GetGrabber()->Release();
    }

