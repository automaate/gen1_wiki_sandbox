
This topic provides a step-by-step guide to adding simple event. For this guide we will use the Aria Quickstart demonstration project.

Description
This Quick Start tutorial shows how to add a simple event to the Aria Quickstart demonstration’s button. For details on how to load, build, program, and run this project, see MPLAB Harmony Graphics Library Help > Graphics Demonstrations > Demonstrations > aria_quickstart.

The steps are as follows:
1. Launch the MPLAB Harmony Configurator:

![Microchip Technology](images/QSG%20ARIA%20Launch%20MHC.png)

2. Open the project’s default saved state:

![Microchip Technology](images/QSG%20Aria%20Quickstart%20Open%20Default%20Saved%20State.png)

When the Configuration Database Setup dialog appears, just hit Launch.

3. Select the Graphics Composer from the MHC Pull-Down Menu which will open a
new window for the MPLAB Harmony Graphics Composer:

![Microchip Technology](images/QSG%20Launch%20Graphics%20Composer.png)

![Microchip Technology](images/QSG%20QuickStart%20Graphics%20Composer.png)

4. In step 8, below, we will change the behavior of the screen’s button by adding **Pressed** and **Released** events.
The **Pressed** event will change the text of the button. First, we must add the needed text. Select the **Asset** menu and click **Strings**.

![Microchip Technology](images/QSG%20Asset%20Strings.png)

5. Click the Add icon, ![Microchip Technology](images/QSG%20String%20Assets%20Add%20New%20String%20Icon.png)), and name the new string “Ouch_String” and then select **Create**.

![Microchip Technology](images/QSG%20Add%20Ouch_String.png)

6. Enter the string value of **Ouch! Ouch! Ouch!**. Next, Select **TimesNewRoman12** as the font . On completion, the screen should show:

![Microchip Technology](images/QSG%20Select%20ButtonWidget1.png)

When finished, close the String Asset dialog.

7. Select the Composer Screen Designer panel and select the **ButtonWidget1 **(“Make changes. Generate. Run”).

![Microchip Technology](images/QSG%20ARIA%20String%20Output.png)

8. Under the **Properties Editor** panel on the right side of the screen, the properties of ButtonWidget1 should appear. Enable the **Pressed** and **Released** events:

![Microchip Technology](images/QSG%20ARIA%20ButtonWidget1%20Properties.png)

9. Click the (![Microchip Technology](images/QSG%20ARIA%20Triple%20Dot%20Button.png)) button on the right side to bring up the Events Editor for the **Pressed** event and create a new action.

![Microchip Technology](images/QSG%20Step%2010%20Create%20New%20Action.png)

When the **Action Edit** dialog appears. Enter the name **ButtonPressed** and click **Next**.

10. Now select which widget the ButtonPressed event of ButtonWidget1 affects. This event can affect any of the display's widgets. However, the objective is for the ButtonPressed event to change the text of its own widget. Therefore, select **ButtonWidget1** and click **Next**.

![Microchip Technology](images/QSG%20Add%20an%20Event%20Step%2011.png)

11. The next dialog window provides instructions to select the action associated with this event. There are many choices, from **Adjust Position** to Set **Y Position**, all of which are related to properties of the button widget. Select **Set Text** as the action, and then click **Next**.


![Microchip Technology](images/QSG%20Add%20Events%20Step%2012.png)

12. In the next **Action Edit Dialog** window select the **Ouch_String** from steps 5 and 6, and then click **Finish**. This action resurfaces the **Event Editor - Pressed** dialog. Click **OK** to close this dialog.
13. Follow the same steps for the **Released** event, but instead create a new event named **ButtonReleased**. Use the same **Set Text** action as before, but use the **Instructions** string instead.
14. Examine the events the has been created by the Window:Event Manager menu. The Event Manager dialog is an alternative way of creating and managing graphics events for the application.

![Microchip Technology](images/QSG%20ARIA%20Event%20Manager%20Dialog.png)

15. Close the Graphics Composer window and save the new design.


![Microchip Technology](images/QSG%20Add%20Event%20Step%2015.png)

16. In the MPLAB Harmony Configurator (MHC) window save the new configuration, since it has been modified. Generate code for this new project configuration by selecting the Generate icon (![Microchip Technology](images/QSG%20ARIA%20Generate%20Code%20Icon.png)  ). Select **Overwrite** as the Merging Strategy, since we don't need to review all the changes made to the graphics design. The select the **Generate** button to generate the new code that implements the events that have just been added.

17. Select the Run Main Project icon ( ![Microchip Technology](images/QSG%20ARIA%20Run%20Main%20Project%20Icon.png) ) to build, load, and run this new configuration.

18. After the project has loaded, click the “Make changes. Generate. Run.” button. The button’s text should change to **Ouch! Ouch! Ouch!** when pressed and revert back to the original text when released.
