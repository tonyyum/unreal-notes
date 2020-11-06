Declaring Delegates For Blueprint
=================================

Introduction
------------

Delegate
^^^^^^^^

Can be dynamic, multicast, return or not and can have params.

Examples:

DECLARE_DYNAMIC_MULTICAST_DELEGATE_RetValue_OneParam

DECLARE_MULTICAST_DELEATE_TwoParams

Events
^^^^^^

Similar to delegate, but cannot be dynamic. It's C++ only (No Blueprint) so more performant.

Example:

DECLARE_EVENT_OneParam

DECLARE_EVENT_SixParam

Add Multicast Delegate to project
---------------------------------

1. Change QuestManager.h

Above class declaration add:

DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FCompletedQuestSignature, int32, Index);

And inside public, add

	UPROPERTY(BlueprintAssignable, BlueprintCallable)
	FCompletedQuestSignature CompletedQuest;

2. Compile and we'll see under Event Dispatcher that CompletedQuest is renamed to CompletedQuest_0

3. Find references to CompletedQuest

Go to CompletedQuest_0, Find References as we'll see there are no references.

Click on the goggle and instead search for CompletedRequest

.. image:: /_static/images/completedquest_0_not_found.PNG

4. Replace Call Completed Quest 0 with Call Completed Quest.

5. Compile QuestManager and QuestMarker
