Refresh Visibility
==================

1. Prefix Blueprint variables with `DEPRECATED_`

2. Create the vairables in C++

.. code-block:: cpp

    UPROPERTY(EditAnywhere, BlueprintReadOnly)
    FName QuestName;

    UPROPERTY(EditAnywhere, BlueprintReadOnly)
    int32 ShowAtProgress = 0;

3. In stage viewport find the quest markers, copy and paste `Bp Quest Name` to `Quest Name`

.. image:: /_static/images/find_quest_markers.PNG

.. image:: /_static/images/copy_paste_quest_name.PNG

4. Do the same thing for `Show at Progress`

5. In QuestMarker:

add #include

.. code-block:: cpp

    #include "QuestManager.h"

Add UFUNCTION GetQuestManager

.. code-block:: cpp

	UFUNCTION(BlueprintPure, BlueprintImplementableEvent)
	AQuestManager* GetQuestManager() const;

6. Override GetQuestManager in Blueprint by actually calling GetQuestManager from BP Library.

.. image:: /_static/images/get_quest_manager.PNG

7.  Implement GetQuest

QuestManager.h


.. code-block:: cpp

	UFUNCTION(BlueprintPure)
	FQuestInfo GetQuest(FName Name) const;

QuestManager.cpp

.. code-block:: cpp

    FQuestInfo AQuestManager::GetQuest(FName Name) const
    {
        return QuestList[GetQuestIndex(Name)];
    }


Note, because GetQuest is a const, we'll need to make GetQuestIndex a const too

8. BP now compiles with error because GetQuest is const, but GetQuests is not. So let's make GetQuests const.

.. image:: /_static/images/make_get_quests_const.PNG

9. Implement RefreshVisibility

QuestMarker.h

.. code-block:: cpp

	UFUNCTION(BlueprintCallable)
	void RefreshVisibility();


QuestMarker.cpp

.. code-block:: cpp

    void AQuestMarker::RefreshVisibility()
    {
        FQuestInfo Quest = GetQuestManager()->GetQuest(QuestName);
        bool Visibility = GetQuestManager()->IsActiveQuest(QuestName) && Quest.Progress == ShowAtProgress;
        ParticleSystem->SetVisibility(Visibility);
    }


10. Delete BP_QuestName and BP_ShowAtProgress

