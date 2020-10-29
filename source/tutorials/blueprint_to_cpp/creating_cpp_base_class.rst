Creating C++ Base Class
=======================

1. In Contents -> Blueprint. rename `Grabber` to `BP_Grabber` and do the same with `CuttableTree`

2. Check the parent of `BP_Grabber` by either checking `Class Settings` or looking at the top right
   and we should see that the parent is `Scene Component`

.. image:: /_static/images/bp_class_settings.PNG

.. image:: /_static/images/parent_is_scene_component.PNG

3. Ensure Windows SDK is installed:
https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/

4. Right click and create new C++ class and choose `Scene Component` and name it `Grabber`. Click on `Public`

.. image:: /_static/images/new_cpp_class.PNG

5. Change the code `BlueprintsToCpp\Source\BlueprintsToCpp\Public\Grabber.h`

.. code-block:: cpp

   UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )
   class BLUEPRINTSTOCPP_API UGrabber : public USceneComponent

Add Blueprintable:

.. code-block:: cpp

   UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent), Blueprintable )

6. Ctrl-Shift-B to build the project and we should see it in the Content Browser.
   (In some versions of UE4 it may require rebooting)

.. image:: /_static/images/grabber_cpp_in_content_browser.PNG

7. In the `BP_Grabber` BluePrint, go to `Class Settings` and change `Parent Class` to `Grabber`

.. image:: /_static/images/set_grabber_cpp_as_parent.PNG

8. Do the same thing with `BP_QuestManager`.
   Check that parent is Actor so create an Actor C++ Class named `QuestManager`.
   Note that this time we do not need to add `Blueprintable` because Actor is
   already `Blueprintable`. Now make parent of `BP_QuestManager` to be `QuestManager`