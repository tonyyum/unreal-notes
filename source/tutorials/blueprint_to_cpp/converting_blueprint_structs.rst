Converting Blueprint Structs
============================

In this part, we are giong to convert the FQuestInfo BP Struct to C++

.. image:: /_static/images/fquestinfo_thumb.PNG

.. image:: /_static/images/fquestinfo.PNG

1. Rename `FQuestInfo` to `FQuestInfo_Deprecated`

2. Create new C++ class. Choose `Show All Classes` -> `Object` to create a `UObject`.
   Name it `QuestInfo`.

.. image:: /_static/images/new_cpp_class_uobject.PNG

3. In QuestInfo.h change UCLASS to USTRUCT, removed inheritance of UOBject,
   change class to struct and change UQuestInfo to FQuestInfo

.. code-block:: cpp

   UCLASS()
   struct BLUEPRINTSTOCPP_API FQuestInfo


.. code-block:: cpp

   USTRUCT(BlueprintType)
   class BLUEPRINTSTOCPP_API FQuestInfo

4. Add the body of QuestInfo struct.

.. code-block:: cpp

   USTRUCT(BlueprintType)
   struct BLUEPRINTSTOCPP_API FQuestInfo
   {
      GENERATED_BODY()

      UPROPERTY(EditAnywhere, BlueprintReadWrite)
      FString Name;

      UPROPERTY(EditAnywhere, BlueprintReadWrite)
      FName QuestId;

      UPROPERTY(EditAnywhere, BlueprintReadWrite)
      int32 Progress;

      UPROPERTY(EditAnywhere, BlueprintReadWrite)
      int32 ProgressTotal;
   };

In my case UE4 would crash and so require launching again.

5. Include QuestInfo.h in QuestManager.h

.. code-block:: cpp

   #include "QuestInfo.h"

6. Add protected UPROPERTY to 

.. code-block:: cpp

   protected:
      UPROPERTY(EditAnywhere, BlueprintReadWrite)
      TArray<FQuestInfo> QuestList;

7. Rename variable `QuestList` to `QuestList_Deprecated`

8. In BP_QuestManager Blueprint -> Class Defaults, replace QuestList with the new one.
   Unforunately, we'll have to copy and paste each item over.

.. image:: /_static/images/quest_manager_default_quest_list.PNG

9. Find all references to QuestList_Deprecated and fix them. 

GetQuest is slightly more tricky it's interface expect return of QuestInfo_Deprecated.

We could either migrate all uses of GetQuest or we can convert our C++ QuestInfo to QuestInfo_Deprecated.

.. image:: /_static/images/get_quest_rewired.PNG

Now go through all other references of QuestList_Deprecated and replace with QuestList.

Where the graph is large and uses get on  `QuestList_Deprecated`, we could always be lazy
and replace it with `GetQuests` that we created.

