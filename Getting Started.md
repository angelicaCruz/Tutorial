# Creating a Unity Project for Hololens

- Open unity and choose "New" to create new unity project. Call the project "SampleProject".
- Make sure  3d3 is chosen 
- Choose a location for the project. 
	Suggestion : choose the Desktop as destination for the project's folder.
- Choose create project and wait for Unity to complete the task. 

## Setting the scene
- Choose the "Main Camera" in the Heirarchy panel (left side of the Scene window).
- In the Inspector panel modify the camera's position into (0,0,0)
<p align="left">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/camera1.png">
</p>

- Find "Clear Flags" and change it's value from Skybox to Solid Color.
- Change the "Background" to black by clicking the box and change RGBA values to 0.
	Remember: black background will appear transparent in Hololens.
<p align="left">	
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/camera2.png">
</p>
- Finally save the scene in order to make changes permanent.

## Adding METool kit
- Open the the previously downloaded METool Kit. 
- Find and choose the following folders: **DataMesh, Resources and Streaming assets**.

## Project Settings
- Open **Edit -> Project Settings -> Quality**
<p align="left">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/settings1.png">
</p>

- In the Inspector Panel go under **Window Store** icon. Click on the Default arrow and choose
	Fastest. You will see a green check right under Windows Store icon.
<p align="left">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/settings2.png">
</p>

- Find 'Other' under the same panel and change 'V Sync Count' value to Don't Sync.
	(image: settings3)a

Build Settings
- open File -> Build Settings -> Player Settings
- Click on "Add Open Scene" in order to add the scene created before. 
- with the chosen platform change Architecture vlaue in x86_64
	(image: settings4)
- click 'Player Settings' and go to the inspector panel.
- In the inspector Panel find 'Other Settings' section, go to Optimization and change
	API Compatibility level to .NET 2.0
	(image; setings6)
- Re open Build Settings, choose Windows Store under Platform and click Switch Platform.
	(if done, the unity icon must be beside Windows Store)
	On the right side, do as follows:
	SDK -> Universal10
	Target device -> Hololens
	UWP Build Type -> D3D
	chech Unit C# Projects 
	(image: settings7)
- Click on the Player Settings -> Other Settings.
	Check Virtual Reality Supported and Windows Holographic will appear as the default SDK.
	(image: settings8)
- Go to Publishing Settings -> Capabilities and check the following:
	InternetClient
	InternetClientServer
	PrivateNetworkClientServer
	WebCam
	SpatialPerception
- All is set! click Build. In the project's folder create a folder
	that will contain the project's build and choose that folder. 
	Wait for the process to happen. 
	The created folder must be like in the picture below.
	(image: settings10)
	
Build and Deploy
- add a cube in the scene and place it where camera can capture
- build the project
- open the build folder 
- find for the  Visual Studio Solution
	(image: build1)
- in Visual Studio, in the upper panel do as follows: 
	Debug -> Release
	x64 -> x86 
	Local Macchine -> Device
	(image: build2 and build2.1)
- press CTRL + F5 or press the icon near Device.
- In Hololens, a cube will be seen and that is a small Hololens
application made with Unity,

It is also possible to have Local Machine -> Remote Machine.
but the hololens' ip address must be provided
(image: build2.2)
The Hololens ip address is in 
Settings -> Network & Internet -> advance option -> ipv4 address

In the next pages, we will integrate METoolKit and Unity Project.
