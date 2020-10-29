Lifecycle Methods
=================

1. Add logs. e.g. take in QuestManager and Grabber's constructor and BeginPlayer

.. code-block:: cpp

    AQuestManager::AQuestManager()
    {
        // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
        PrimaryActorTick.bCanEverTick = true;

        UE_LOG(LogTemp, Warning, TEXT("QuestManager Constructor"))

    }


2. Go to Windows -> Developer Tools and Output log to see the log.

.. image:: /_static/images/output_log_window.PNG

3. Also notice in the above code there is `PrimaryActorTick.bCanEverTick = true;`.
If set to false then the Tick function would not be called on every frame.

