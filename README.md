# Smoke-for-Microsoft-Flight-Simulator
This is a comprehensive beginners guide on how to add the Team Turbulence Smoke to your MSFS projects. This will explain how to add the effect to aircraft for people that are new to, or don't have any coding experience.

First you'll need to add the smoke .spb/.xml files to your project. Copy the VisualEffectLibs folder and place it in the top most folder for your aircraft (Next to SimObjects). 

Next, in my file, go to SimObjects -> Airplanes -> [YourAirplane] and open systems.cfg. Here you'll see two lines, the first line is explaining the significance of the second line. Copy the second line:
```CFG
circuit.21 = Type:CIRCUIT_LIGHT_LOGO				#Connections:bus.3#			Power:10, 15, 20.0#			Name:Logo_Light ; logo light 15W
```
Paste this into your systems.cfg circuit section, i like to put it at the end, when you do this make sure you change the `21` to the next chronological number that would come after the previous circuit in the list.

Next, you'll need to add in the model's behavior code this will be what tells the game what bindings you're using, and what effect is bound to that. Close Systems.cfg and open the model folder and open the Example XML file. Note that the code for the VFX is between `<Behaviors>` `</Behaviors>` tags. Copy this:
```XML
<!-- SMOKE -->

		<Component ID="FX_SMOKE_ID">

      <!-- LEFT ESG -->

		<!-- ESG pods disabled so that smoke can work on only the light switch for mutliplayer visibility

		<Component ID="FX_SMOKE_ID_NODE1_WHITE_NEAR" Node="FX_SMOKE_RIGHT_MODEL_NODE">

			  <UseTemplate Name="ASOBO_GT_FX">

				<FX_CODE>(A:LIGHT LOGO:1, bool)</FX_GUID>

			  </UseTemplate>

			</Component>

			<Component ID="FX_SMOKE_ID_NODE1_WHITE_FAR" Node="FX_SMOKE_RIGHT_MODEL_NODE">

			  <UseTemplate Name="ASOBO_GT_FX">

				<FX_CODE>(A:LIGHT LOGO:1, bool)</FX_CODE>

				<FX_GUID>{2E980C6D-731D-462F-B273-14834102831B}</FX_GUID>

			  </UseTemplate>

			</Component>-->

      

      <!-- Smoke -->

		    <Component ID="FX_SMOKE_ID_NODE3_WHITE_NEAR" Node="FX_SMOKE_RIGHT_MODEL_NODE">

			  <UseTemplate Name="ASOBO_GT_FX">

				<FX_CODE>(A:LIGHT LOGO:1, bool)</FX_CODE>

				<FX_GUID>{2562B47E-5D9A-44D1-8DBA-73E9AAB7CF5C}</FX_GUID>

			  </UseTemplate>

			</Component>

			<Component ID="FX_SMOKE_ID_NODE3_WHITE_FAR" Node="FX_SMOKE_RIGHT_MODEL_NODE">

			  <UseTemplate Name="ASOBO_GT_FX">

				<FX_CODE>(A:LIGHT LOGO:1, bool)</FX_CODE>

				<FX_GUID>{2E980C6D-731D-462F-B273-14834102831B}</FX_GUID>

			  </UseTemplate>

			</Component>

        </Component>
```
        
When you have this copied, paste the code in your Aircrafts Model.xml file MAKE SURE YOU AREN'T PUTTING IT INTO THE INTERIOR'S XML this is usually labeled as "int" in the file name. Look for a tag that says `<Behaviors>` I recommend scrolling down until you find the end of that section which will be marked as `</Behaviors>` add a new line just before this and then paste the code in.

Next, you'll need to find the Node to attach the smoke to, this is basically telling the sim where the smoke should emit from, otherwise it will be all wonky and randomly shoot out in weird directions. Load up BLENDER, and import the Exterior GLTF file for your aircraft using the MSFS blender plugin, more information on how to obtain, and use this plugin can be found on the official MSFS SDK docs: https://docs.flightsimulator.com/html/Asset_Creation/Blender_Plugin/The_Blender_Plugin.htm

In blender, you can click on a part of the model, and it will say on the top left what the name of that part is, this will be your Node take this name and replace each instance of `Node=""` with the name of whatever part you want it to emit from inside of the quotations.

These changes require a Sim Restart, so ALT + F4 out of MSFS 

Load into the sim, get into the plane you implemented the change on, and if you've followed my instructions correctly, you should have smoke bound to LOGO LIGHTS toggle which can be bound to a button in controls. You can also quickly check if it worked by toggling master lights which is default L on your keyboard.

        


