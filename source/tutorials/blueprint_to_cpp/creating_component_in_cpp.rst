Create Components in C++
========================

1. Create new C++ class `QuestMarker` as a subclass of an `Actor`

2. Go to BP_QuestMarker and re-parent to `QuestMarker`

3. To avoid conflict, rename subcomponent ParticleSystem in Blueprint to BP_ParticleSystem.

4. Add the following to QuestMarker.h

Include:

.. code-block:: cpp

    #include "Particles/ParticleSystemComponent.h"

And add propoerties:

.. code-block:: cpp

    protected:
        UPROPERTY(VisibleAnywhere, BlueprintReadOnly)
        USceneComponent* Root;

        UPROPERTY(VisibleAnywhere, BlueprintReadOnly)
        UParticleSystemComponent* ParticleSystem;
    };


5. Add the following to QuestMarker.cpp

.. code-block:: cpp

    AQuestMarker::AQuestMarker()
    {
        // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
        PrimaryActorTick.bCanEverTick = false;

        Root = CreateDefaultSubobject<USceneComponent>(TEXT("SceneRoot"));

        // Can only be used in constructor
        ParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("ParticleSystem"));
        SetRootComponent(Root);

        ParticleSystem->SetupAttachment(Root);
    }

Note that due to some strange cachinng problem you'll need to restart UE4,
rename ParticleSystem to ParticleSystem1 and rename it back to ParticleSystem again

6. From UE4 Editor, copy and paste all the properties from BP_ParticleSystem to ParticleSystem

7. Find references to BP_ParticleSystem and replace them with ParticleSystem

8. Delete BP_ParticleSystem