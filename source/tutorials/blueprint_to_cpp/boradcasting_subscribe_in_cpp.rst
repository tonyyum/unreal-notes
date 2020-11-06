Broadcasting and Subscribe in C++
=================================

C++ code
--------

Add to QuestMarker.h

.. code-block:: cpp

    protected:
        virtual void BeginPlay() override;

    private:
        void QuestUpdate(int32 Index);

Added to QuestMarker.cpp

.. code-block:: cpp

    void AQuestMarker::BeginPlay()
    {
        GetQuestManager()->CompletedQuest.AddDynamic(this, &AQuestMarker::QuestUpdate);
        RefreshVisibility();
    }
 
.. code-block:: cpp

    void AQuestMarker::QuestUpdate(int32 Index)
    {
        RefreshVisibility();
    }


Add one line at the bottom of QuestManager.cpp -> AQuestManager::CompleteQuest_Implementation

.. code-block:: cpp

	CompletedQuest.Broadcast(QuestIndex);

Blueprint
---------

We can not delete the event graph for QuestMarker and QuestManager