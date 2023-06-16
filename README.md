# creative-making（VR project + Animation)

## YOUTUBE link1 (VR project)：https://youtu.be/8iMgcK5z8dA

## Project files link: https://1drv.ms/u/s!Aj3rNlM23GydiAyNKb1d0weamfcd 
I will describe how my work is made and offer it to those who are interested.

## Painting	 
First complete the usual project creation operation, delete all the extra objects, then create a new copy of the default game mode and VRPawn, and save the default map as PaintingMap
 
 

## Drawing lines	 
Create an Actor named BP_Stroke and create two "instantiated static mesh components" under this Stroke
![6e6e482b961b4324bbf622597c0f462](https://github.com/maanqii/creative-making/assets/119876408/f82e6007-05da-4a9c-88d4-1063053b1445)
 
Import the Cylinder and Sphere (just drag them in) and create a spare M_Stroke material

⭐ Be careful to choose translucent for the blend mode, this will ensure that there is no flickering effect when strokes are stacked
![image](https://github.com/maanqii/creative-making/assets/119876408/7213256c-69be-48fa-bac2-c0eba3753b6a)

 
 
 
Then select the Cylinder static mesh and M_stroke material in StrokeMeshes; 

select the Sphere static mesh and M_stroke material in JointMeshes.


![image](https://github.com/maanqii/creative-making/assets/119876408/cac342c8-6abc-4d5f-951b-de60130f4cd7)
 



Create PreviousCursorLocation and ControlPoints variables, and Update function


 
Call Update function in PaintingPawn to generate successive balls by pressing Trigger

![image](https://github.com/maanqii/creative-making/assets/119876408/cbcfdbff-ae38-4920-a39c-f90054a77583)

 
 
Contraction of the Joint inversion transform position to the GetNextJointTransform function

![image](https://github.com/maanqii/creative-making/assets/119876408/92511ea7-cde6-468f-9f68-b29e60e4d1aa)

 
Create a GetNextSegmentTransform function to calculate the length and rotation between the points of each frame

![image](https://github.com/maanqii/creative-making/assets/119876408/eba6379b-1b06-4a91-948f-70dac9b67b44)

 
 
Update the StrokeMeshes and JointMeshes in Update to draw point lines
 
In order to archive, the position of each time needs to be recorded in Control Points

![image](https://github.com/maanqii/creative-making/assets/119876408/799fb25a-6705-46b9-84bd-43f99001a341)

 
 
## Preservation of paintings	 
Create a Painting variable in PaintingPawn to hold the name of this painting
 
Create a Stroke structure to hold an array of ControlPoints

![image](https://github.com/maanqii/creative-making/assets/119876408/331d58b3-4bf3-490c-bf94-5d725142f2bc)

 
Create a SaveGame class named BP_PainterSave

![image](https://github.com/maanqii/creative-making/assets/119876408/ba0420d7-a2ff-4154-a9d5-963ce11b2452)

 
 
Create a Strokes variable, an array of the type Stroke structure
Then create two more functions, Save and Load, to store the data
 
![image](https://github.com/maanqii/creative-making/assets/119876408/9d6278e4-dba9-4d7d-8875-99c023cd23d8)

![image](https://github.com/maanqii/creative-making/assets/119876408/003488e4-4447-4636-8dd1-726927b7b680)

 
Initialise the game archive object in PaintingPawn

![image](https://github.com/maanqii/creative-making/assets/119876408/016c8a2a-d177-447a-bd79-3e08336b19f4)

 
The Save and Load action maps are then created to initiate archive and read operations

![image](https://github.com/maanqii/creative-making/assets/119876408/a1629f8d-8c96-4914-b048-8792780fbf7d)

Implementing archive operations

![image](https://github.com/maanqii/creative-making/assets/119876408/3eadbe8e-946b-49f5-97be-2bbfc701c3f4)

 
When the corresponding action button is pressed, our current drawing is stored locally, with the following effect

![image](https://github.com/maanqii/creative-making/assets/119876408/fdc04f95-0398-41ff-b884-3cf81e26c643)

 
## Read the archive	 
Create a DestoryWorld function that clears the file before reading it

![image](https://github.com/maanqii/creative-making/assets/119876408/309d5dd4-7fb9-4c44-bd70-26315e90009b)

 
Create a Load function to load an archive

![image](https://github.com/maanqii/creative-making/assets/119876408/261a9fe0-f989-4d55-905d-524f08e63b9d)

 
 
The SpawnAndDeserialStrokes function, which is used to decompress the data after reading the file

![image](https://github.com/maanqii/creative-making/assets/119876408/a84a1d5c-8ef1-4bac-8c0a-15e02e16608a)

 
Finally the Load function is called in PaintingPawn to finish reading the file


 
## Picture albums	 
### UI artboards	 
Map configuration
Create a MainMenu map and create the corresponding UIGameMode and UIPawn
UIGameMode is a direct copy of the previous PaintingGameMode
 

UIPawn inherits from VRPawn

WBP_PaintingGrid
Create a control blueprint, inherited from the user control, named WBP_PaintingGrid

![image](https://github.com/maanqii/creative-making/assets/119876408/159dff47-361a-4827-afdb-8adfc457764a)


 
BP_PaintingPicker
Create an Actor blueprint named BP_PaintingPicker
Create a sample Spline and a control component PaintingGrid


 
Switch to the right view of the viewport and move the position of the PaintingGrid to the end point of the sample bar. After the move, the details of the PaintingGrid are configured as follows

![image](https://github.com/maanqii/creative-making/assets/119876408/75680979-cb72-44f9-a29d-fa948fcba9c4)
 
## UIPawn
A new control interaction component in UIPawn for interaction between VR and control blueprints
 
 
Make the following configuration and then add this blueprint to the time chart for mapping joystick interactions to mouse interactions

![image](https://github.com/maanqii/creative-making/assets/119876408/1e86fe5e-21b8-44b5-930b-917840780fbc)

 
## Map Configuration
The newly created map is empty and needs to be added with the user start point and the BP_PaintingPicker created above


 
 

## Operating tables

![image](https://github.com/maanqii/creative-making/assets/119876408/d7b4ae77-c17b-4119-9583-67be8f19ea0e)

![image](https://github.com/maanqii/creative-making/assets/119876408/1187f6b1-e6fb-47fc-bb7b-76e785be299a)


 
 
 
 
 
 
 
 

 
 
## Adding a painting	 
The main operations on the painting are done in the BP_PaintingPicker.
We need to bind the ActionBar to the PaintingPicker
Open the ActionBar's chart and create a function that stores a reference to the PaintingPicker

Then open the PaintingPicker, do some initialization, associate the ActionBar, and store the PaintingGrid's panel.

![image](https://github.com/maanqii/creative-making/assets/119876408/312e94b9-f5dc-4cf1-a788-9f13bf648989)

 
 
⭐the PaintingGrid should have variables turned on
 
 
Create a user control named WBP_PaintingCard

![image](https://github.com/maanqii/creative-making/assets/119876408/f7ddce7b-a266-4e6e-8b40-9e33337b11e0)

 
Add a new Painting variable to the chart of WBP_PaintingCard to store the name of the painting

 
Create the AddPainting function in the PaintingPicker


![image](https://github.com/maanqii/creative-making/assets/119876408/34e22cf1-d231-4883-b40e-bf2851e35dd9)

 
where GetTimeStamp is to get the timestamp to ensure that the name of each painting is different

![image](https://github.com/maanqii/creative-making/assets/119876408/fe27c4e6-f153-44f4-a41a-a564064c54f2)

 
AddCard is to add a new painting card

![image](https://github.com/maanqii/creative-making/assets/119876408/a3dc7fa0-17ce-4909-b34d-88264066cfb6)
  
Finally, bind the Add event in the ActionBar.


 
## Deleting a painting	 
Click on the delete button on the console, all the paintings will appear in red, then click on the corresponding painting to delete
First open the PaintingCard control and create a PaintingPicker variable to bind the relationship between them

![image](https://github.com/maanqii/creative-making/assets/119876408/9df44438-66e9-4129-83f1-419be41f6012)

 
 
Then add this part of the initialisation logic to the AddCard logic of the PaintingPicker

![image](https://github.com/maanqii/creative-making/assets/119876408/a6dac5bd-4bb8-465d-ac3a-bef1a2e6851e)


 
Create a function to delete a painting, called DeletePainting

Find the Painting you want to delete from the Paintings string array, then clear all the panels, then create all the cards again based on the new painting array.

![image](https://github.com/maanqii/creative-making/assets/119876408/496115fe-9e3a-472d-a18f-7eeca7cd4c68)

 
The logic of InitCards is as follows

![image](https://github.com/maanqii/creative-making/assets/119876408/3a53be64-01e3-4e0b-b930-2ce3b551bce0)
 
 
Next, to control the delete mode and normal mode, I create a ChangeDeleteMode function and create the relevant variables
(DeleteButtonStyle, NormalButtonStyle, DeleteMode)
DeleteButtonStyle is the style of the card in delete mode
NormalButtonStyle is the style of the card in its normal state
DeleteMode is a boolean value that controls the state

![image](https://github.com/maanqii/creative-making/assets/119876408/85a8bbf7-82d1-428d-a8f3-991e6dd8693f)

 
The detailed logic of SetCardButtonStyle is as follows

![image](https://github.com/maanqii/creative-making/assets/119876408/45f3ed7d-51e2-4035-9df3-bde6a6682049)

 
After controlling the two modes, a CardClick function is created to delete the card when the card is clicked in delete mode

![image](https://github.com/maanqii/creative-making/assets/119876408/7111df13-d4ff-4dff-91c6-2608a34c1ace)
 
 
Finally, call this function in PaintingCard
 
## Saving the board	 
Create a SaveGame blueprint, named BP_MenuSave
Create two functions Save and Load
 
When the PaintingPicker is initialised, BP_MenuSave is initialised and the corresponding archive is read

![image](https://github.com/maanqii/creative-making/assets/119876408/9cb12129-62a0-4185-b712-b691b8699272)

 
When you add a new painting or delete a painting, you will also need to save it, so create a save function first and call it when appropriate

![image](https://github.com/maanqii/creative-making/assets/119876408/d7eeb1f5-a3a8-40b9-8842-74c21edef46e)

![image](https://github.com/maanqii/creative-making/assets/119876408/7d0e0525-053f-4602-8905-b5906a2ad0da)

![image](https://github.com/maanqii/creative-making/assets/119876408/e14a9245-b784-4762-b747-317ea15458ee)

 
 
 
 
Once this is done, the whole board will be saved and read automatically

## Optimisation	 
### Data Linking	 
Create a game instance, named PaintingGameInstance
  
Create a CurrentPainting variable in this game instance
 
Apply this game instance in the project settings
 
When the user clicks on a card, we set the CurrentPainting in the game instance to the corresponding card's Painting and open the PaintingMap

![image](https://github.com/maanqii/creative-making/assets/119876408/6f609405-b7c6-4b54-98c1-8cd33cd619c9)

 
When initialising the PaintingPawn, the file is read according to CurrentPainting

![image](https://github.com/maanqii/creative-making/assets/119876408/074895fa-19e3-463f-a261-2e558e42f499)

 
 
Finally, add an action to return to the home page

![image](https://github.com/maanqii/creative-making/assets/119876408/96f68d6a-02a6-4346-99a6-182dc49823f9)


 
 
## The painting cover	 
Make a screenshot to remind the user of the general content of each painting
First create a render target, named RT_PainterSpectator 
 
Then open PaintingPawn and create a scene capture 2D
 
 
 
 
While the user is archiving, take a screenshot in the process

![image](https://github.com/maanqii/creative-making/assets/119876408/335d846e-8424-45b0-9501-2c7eaabe6993)

![image](https://github.com/maanqii/creative-making/assets/119876408/9b0a635e-215c-40ec-820f-cdc38a158bca)


 
 

 
Then back to the PaintingPicker, we need to read the image and display it in the gallery
Create a DefaultImg variable that will read the default image when the user creates a new drawing, or when the drawing screenshot is empty


 
 
Create a SetImg function to implement the ability to populate the cover of the card

![image](https://github.com/maanqii/creative-making/assets/119876408/3601a46d-4867-42f8-9143-b41376375d31)
 
⭐Add the ability to fill the cover when all cards are initialised 
⭐When the user adds a new painting, the default cover needs to be added as well
 
At this point all the sketchbooks will have a cover

### Stroke removal	 

First create a Painter static grid inside PainterPawn to indicate the exact pen tip contact

![image](https://github.com/maanqii/creative-making/assets/119876408/36a59ef4-be20-40af-be7c-c6ed7461868c)

  
To distinguish between delete and normal modes, we want the Painter to display different colours in different modes
First create a dynamic material instance when PaintingPawn is initialised

![image](https://github.com/maanqii/creative-making/assets/119876408/4c557cd6-1787-42cb-9955-d9dc09059446)

 
Then when the right Grab key is pressed, set the different modes and colours (note that the DeleteMode variable needs to be created in advance)

![image](https://github.com/maanqii/creative-making/assets/119876408/da94cb1f-e1f8-485b-b2f0-838b87e3c288)
 
 
Then we detect the collision between the Painter and the stroke, and if we hit it in delete mode, we delete the stroke directly

![image](https://github.com/maanqii/creative-making/assets/119876408/be0f52a1-b9ef-417c-92cf-55b7b82a2e90)

In order for the collision to occur smoothly, we also need to set the collision preset for Painter and BP_stroke

#![template](https://github.com/maanqii/creative-making/assets/119876408/8b4554cd-4e96-42fc-b9ba-d48de027e82e)
# YOUTUBE link2 (Exhibition Projects）：https://youtu.be/3LVkwf4Isuk

