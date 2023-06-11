# creative-making
## YOUTUBE link：https://youtu.be/8iMgcK5z8dA
I will describe how my work is made and offer it to those who are interested.

## Painting	 
First complete the usual project creation operation, delete all the extra objects, then create a new copy of the default game mode and VRPawn, and save the default map as PaintingMap
 
 

### Drawing lines	 
Create an Actor named BP_Stroke and create two "instantiated static mesh components" under this Stroke
 
Import the Cylinder and Sphere (just drag them in) and create a spare M_Stroke material
⭐ Be careful to choose translucent for the blend mode, this will ensure that there is no flickering effect when strokes are stacked
 
 
 
Then select the Cylinder static mesh and M_stroke material in StrokeMeshes; select the Sphere static mesh and M_stroke material in JointMeshes.
 
 
Create PreviousCursorLocation and ControlPoints variables, and Update function
 
Call Update function in PaintingPawn to generate successive balls by pressing Trigger
 
 
Contraction of the Joint inversion transform position to the GetNextJointTransform function
 
Create a GetNextSegmentTransform function to calculate the length and rotation between the points of each frame
 
 
Update the StrokeMeshes and JointMeshes in Update to draw point lines
 
In order to archive, the position of each time needs to be recorded in Control Points

 

The environment was then modified to enter the closed scene and it was found that the initial first point was always at the origin, the solution was as follows（？？？）
 
 
### Preservation of paintings	 
Create a Painting variable in PaintingPawn to hold the name of this painting
 
Create a Stroke structure to hold an array of ControlPoints
 
Create a SaveGame class named BP_PainterSave
 
 
Create a Strokes variable, an array of the type Stroke structure
Then create two more functions, Save and Load, to store the data
 
 
 
Initialise the game archive object in PaintingPawn
 
The Save and Load action maps are then created to initiate archive and read operations
 
 
### Implementing archive operations
 
When the corresponding action button is pressed, our current drawing is stored locally, with the following effect
 
## Read the archive	 
Create a DestoryWorld function that clears the file before reading it
 
Create a Load function to load an archive
 
 
The SpawnAndDeserialStrokes function, which is used to decompress the data after reading the file
 
Finally the Load function is called in PaintingPawn to finish reading the file
 
## Picture albums	 
### UI artboards	 
Map configuration
Create a MainMenu map and create the corresponding UIGameMode and UIPawn
UIGameMode is a direct copy of the previous PaintingGameMode
 

UIPawn inherits from VRPawn

WBP_PaintingGrid
Create a control blueprint, inherited from the user control, named WBP_PaintingGrid

 
BP_PaintingPicker
Create an Actor blueprint named BP_PaintingPicker
Create a sample Spline and a control component PaintingGrid

 
 
Switch to the right view of the viewport and move the position of the PaintingGrid to the end point of the sample bar. After the move, the details of the PaintingGrid are configured as follows
 
## UIPawn
A new control interaction component in UIPawn for interaction between VR and control blueprints
 
 
Make the following configuration and then add this blueprint to the time chart for mapping joystick interactions to mouse interactions
 
## Map Configuration
The newly created map is empty and needs to be added with the user start point and the BP_PaintingPicker created above
 
 

## Operating tables

 
 
 
 
 
 
 
 

 
 
## Adding a painting	 
The main operations on the painting are done in the BP_PaintingPicker.
We need to bind the ActionBar to the PaintingPicker
Open the ActionBar's chart and create a function that stores a reference to the PaintingPicker
 
 

Then open the PaintingPicker, do some initialization, associate the ActionBar, and store the PaintingGrid's panel.
 
⭐that the PaintingGrid should have variables turned on
 
 
Create a user control named WBP_PaintingCard
 
Add a new Painting variable to the chart of WBP_PaintingCard to store the name of the painting
 
 
Create the AddPainting function in the PaintingPicker
 
where GetTimeStamp is to get the timestamp to ensure that the name of each painting is different
 
AddCard is to add a new painting card
 
 
Finally, bind the Add event in the ActionBar.
 
## Deleting a painting	 
Click on the delete button on the console, all the paintings will appear in red, then click on the corresponding painting to
Deleting
First open the PaintingCard control and create a PaintingPicker variable to bind the relationship between them
 
 
Then add this part of the initialisation logic to the AddCard logic of the PaintingPicker

 
Create a function to delete a painting, called DeletePainting
Find the Painting you want to delete from the Paintings string array, then clear all the panels, then create all the cards again based on the new painting array.
 
The logic of InitCards is as follows
 
 
Next, to control the delete mode and normal mode, I create a ChangeDeleteMode function and create the relevant variables
(DeleteButtonStyle, NormalButtonStyle, DeleteMode)
DeleteButtonStyle is the style of the card in delete mode
NormalButtonStyle is the style of the card in its normal state
DeleteMode is a boolean value that controls the state
 
The detailed logic of SetCardButtonStyle is as follows
 
After controlling the two modes, a CardClick function is created to delete the card when the card is clicked in delete mode
 
 
Finally, call this function in PaintingCard
 
## Saving the board	 
Create a SaveGame blueprint, named BP_MenuSave
Create two functions Save and Load
 
 
 
When the PaintingPicker is initialised, BP_MenuSave is initialised and the corresponding archive is read
 
When you add a new painting or delete a painting, you will also need to save it, so create a save function first and call it when appropriate
 
 
 
 
Once this is done, the whole board will be saved and read automatically

Optimisation	 
Data Linking	 
Create a game instance, named PaintingGameInstance
 
 
Create a CurrentPainting variable in this game instance
 
Apply this game instance in the project settings
 
 
When the user clicks on a card, we set the CurrentPainting in the game instance to the corresponding card's Painting and open the PaintingMap
 
When initialising the PaintingPawn, the file is read according to CurrentPainting
 
 
Finally, add an action to return to the painting book
 
 
## The painting cover	 
Make a screenshot to remind the user of the general content of each painting
First create a render target, named RT_PainterSpectator
 
 
Then configure its details
 
 
Then open PaintingPawn and create a scene capture 2D
 
 
 
 
While the user is archiving, take a screenshot in the process
 
 

 
Then back to the PaintingPicker, we need to read the image and display it in the gallery
Create a DefaultImg variable that will read the default image when the user creates a new drawing, or when the drawing screenshot is empty
 
 
Create a SetImg function to implement the ability to populate the cover of the card
 
Add the ability to fill the cover when all cards are initialised
 
 
When the user adds a new painting, the default cover needs to be added as well
 
At this point all the sketchbooks will have a cover
Stroke removal	 

First create a Painter static grid inside PainterPawn to indicate the exact pen tip contact
 
 
 
To distinguish between delete and normal modes, we want the Painter to display different colours in different modes
First create a dynamic material instance when PaintingPawn is initialised
 
Then when the right Grab key is pressed, set the different modes and colours (note that the DeleteMode variable needs to be created in advance)
 
 
Then we detect the collision between the Painter and the stroke, and if we hit it in delete mode, we delete the stroke directly
In order for the collision to occur smoothly, we also need to set the collision preset for Painter and BP_stroke

