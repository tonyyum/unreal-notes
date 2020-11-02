Complete Quest
==============

Let's replace the CompleteQuest BP function with one in C++.

Take a look at the node and details:

.. image:: /_static/images/bp_quest_complete_details.PNG

We notice that.

1. This is a Public function

2. It is not Pure

3. The Inputs are:

  a. QuestId of type Name and not passed by reference.

  b. CompleteWholeQuest of type Boolean and not passed by reference.

4. There are no output

5. There is a pi going in named `Index`

Create the CompleteQuest C++ Function
-------------------------------------

In QuestManager.h add

.. code-block:: cpp

	UFUNCTION(BlueprintCallable, BlueprintNativeEvent)
	void CompleteQuest(FName QuestId, bool CompleteWholeQuest);

In QuestManager.cpp add

.. code-block:: cpp

    void AQuestManager::CompleteQuest_Implementation(FName QuestId, bool CompleteWholeQuest)
    {

    }

Overriding CompleteQuest
------------------------

1. Grab all but the input node from CompleteQuest BP, Ctrl-X to cut.

2. Delete `CompleteQuest`

3. Override the function `CompleteQuest`.

4. Paste the graph.

Noteice that we see `Event Complete Quest`. So it appears as an event. This is the case if the function return is void.

    a. The function is void

    b. Is not const

5.  Right click on `Event Complete Quest` and select `Add call to parent function`

.. image:: /_static/images/add_call_to_parent_function.PNG

Overriding GetQuestIndex
^^^^^^^^^^^^^^^^^^^^^^^^

1. Notice GetQuestIndex that is only available in Blueprint.

.. image:: /_static/images/get_quest_index.PNG

That would need to be migrated.

Also notice that the Output is `Index` which would not match C++.

.. image:: /_static/images/get_quest_index_return_value.PNG

Rename that to `Return Value` which is a special name in Blueprint would fix that. 

.. image:: /_static/images/get_request_index_outputs.PNG

2. Add the below to QuestManager.h

.. code-block:: cpp

	UFUNCTION(BlueprintPure, BlueprintImplementableEvent)
	int32 GetQuestIndex(FName QuestId);

3. Ctrl-X cut the content of the GetQuestIndex, delete and override with same name. Hook up the wires correctly

4: Fix the below error by Right-Click `Refresh Node` and reconnect.

.. code-block: console

    Get Quest Index  was pruned because its Exec pin is not connected, the connected value is not available and will instead be read as default

Implementing CompleteQuest
--------------------------

1. Add code to QuestManager.cpp

.. code-block:: cpp

    void AQuestManager::CompleteQuest_Implementation(FName QuestId, bool CompleteWholeQuest)
    {
        int32 QuestIndex = GetQuestIndex(QuestId);
        FQuestInfo Quest = QuestList[QuestIndex];
        if (CompleteWholeQuest) {
            QuestList[QuestIndex].Progress = Quest.ProgressTotal;
        }
        else {
            QuestList[QuestIndex].Progress = FMath::Min(Quest.Progress + 1, Quest.ProgressTotal);
        }
    }

2. All nodes pasted from before was used only for reference to replicate as code above.
   Now delete them.

3. connect input to calling parent to output along with `GetQuestIndex` and we have replaced the BP function in C++.