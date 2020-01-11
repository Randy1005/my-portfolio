# Prelogue
Feel free to look around! This isn't much but this is where I play around with various styles of game designing, and let us begin.

# Link to each section
[Ziggy's Adventure](#Ziggy's Adventure)
[Poocman](#Poocman)
[Shadow Mapping/Normal Mapping/Parallax Mapping with OpenGL](#Shadow Mapping / Normal Mapping / Parallax Mapping Implementation with Collision Detection)




## Ziggy's Adventure
### Intro
After the release of "Inside" by Playdead Studio, I've always wondered what it's like to make a platformer, so here it is, "Ziggy's Adventure". I made this with Qt as the graphical framework and Box2D as the physics engine. I borrowed the basic settings from a course project I made in 2016, which is an "Angrybird" game.

### Design Statement
For all the game objects, I used a class "GameItem" for them to inherit, since all objects are required to have physics bodies, and they all needed animation framework. As the animations needed frames of sprites, I made the class "SpriteItem" so that I can render parts of a big spritesheet, instead of cutting out sprite frames manually and store them in separate pixmap objects.

The main Character "Ziggy", defines its body, shape, fixture inside its constructor, and also parses animation informations from a JSON file. Since Ziggy needs some special behaviors, some methods such as "fire", "HPDecrement" are implemented inside it, and I installed an event filter for user keyboard control. Other item classes such as "Slime", "Platform", "BulletWave" are implemented with the same logic, but with their own different methods.

To handle the collisions, I created "ContactListener", which inherits from "b2ContactListener". By overriding the method "BeginContact" and "EndContact", we have the fixtures that are colliding under control. Designing the user data pattern stored in the fixtures becomes a tricky question, I wanted to be able to extract every piece of information I need while packing minimum user data. So I created a structure called "userDataStruct", and stored the game object pointer and a self-defined ID inside it, and it worked quite well, I get to manipulate the items as the bullets, enemies and Ziggy bumps into each other.

To sum up, Box2D is quite a powerful physics engine, though setting up basic attributes for the physics bodies is heavy work, and the coordinate converting took up a lot of time, because the coordinate system designed in Qt and Box2D are entirely different. Fixing the setting problems (though not all of them, the physics body shapes are actually still a bit off) and seeing the game objects bouncing around made me really exciting, because I felt a bit more closer to making a real game.

### Demo Clip
[![](http://img.youtube.com/vi/OWG2oOFKxKE/0.jpg)](http://www.youtube.com/watch?v=OWG2oOFKxKE "Ziggy's Adventure")

### Repository URL
[Ziggy's Adventure](https://github.com/Randy1005/Example-code-for-Project-3)

### Install / Download Instructions
- install Git for Windows
- run Git Bash anywhere and type in the following command:
```
  git clone https://github.com/Randy1005/Example-code-for-Project-3.git
```
- the executable file will be in *Example-code-for-Project-3/ziggyAdventureRelease/ziggysAdventure.exe*
- run the executable file

### Controls
+ Arrow keys to move, jump
+ Space bar to perform sword attack
+ S key to launch destruction wave

## Poocman
### Intro
This was a project I came up with when I graduated from university and wanted to make something with better style of coding. I wanted to integrate algorithms and modularized programming while working on this project, so with a simple Pacman-like game, I did my best to accomplish these goals I set for myself.

### Design Statement
For map generation, Instead of a fixed arena, I wanted “Poocman” to generate a maze for itself, so I used Backtracking Recursion to generate the map. Given cells and walls, the “MazeGenerator” class generates a new map as we run the game.

Since no physics engine is attached to the graphical user interface, I then came up with an idea to detect walls and walkable cells with RGB differences. The walls in the game are all gray, and the cells are all black, so as the main character or monsters bump into an area with certain RGB combinations, they know to stop or turn.

Also, animation is an element that I can’t miss out in this project. Instead of creating a whole bunch of pixmap objects and iterating through them to play animations, I wanted to save some memory space and implement sprite animations in a more efficient way. I coded the “AnimationSprite” class, which instantiates a game object that reads information from individual JSON files (containing informations: animation frames, animation names), and cuts out subregions from a big sprite sheet, and store the animation frames for different movements (idle, moving up, moving down, etc.), and all that’s left for the user to do is call the method: startAnimation(“animationName”).

To sum up, I gave up to what I used to do with sprite animations, and figure out a framework for myself. Also regarding the game characters, different from what I used to do, which is create a different class for each of them (and that’s obviously a bad coding style), I put inheritance into use this time. Just like what our course instructor said, “Small games, big thoughts”, think bigger, and even the game scale was no bigger than projects I did before, I certainly had more fun.

### Demo Clip
[![](http://img.youtube.com/vi/Gor8nSBUJLY/0.jpg)](http://www.youtube.com/watch?v=Gor8nSBUJLY "Poocman")

### Repository URL
[Poocman](https://github.com/Randy1005/poocman)

### Install / Download Instructions
- install Git for Windows
- run Git Bash anywhere and type in the following command
```
  git clone https://github.com/Randy1005/poocman.git
```
- the executable file will be in *poocman/poocmanRelease/poocman.exe*
- run the executable file


## Shadow Mapping / Normal Mapping / Parallax Mapping Implementation with Collision Detection
### Intro
This project was made as a final course project when I attended "Practical Computer Graphics Skills for Technical Artists", and this was built as a team project with OpenGL. Normal Mapping and Parallax Mapping are different methods to make textures on a flat sheet "stick out", that is, to make it three-dimensional. Shadow Mapping is a method to create shadows in a scene, with the help of a depth map of the scene, and other optimization steps. As we demonstrate these implementations by making a 3D maze simulator, I coded collision detection, camera, and rendered the maze.

### Design Statement
Since textures improving and shadow mapping can be done in separate projects, first we decided to split tracks, two of us work on normal mapping and parallax mapping, the other teammate and I work on collision detection and shadow mapping. As my teammate finished the implementation of shadow mapping quite fast, we started to work on collision detections and game camera. 

Camera was not an initially integrated concept in OpenGL, but we browsed some tutorials and managed to code it by calculating the camera coordinates and matrices. Collision Detection was a lot more easier. Based on the maze we rendered, the cells are all consistently cubes, so we applied the basic Axis-Aligned Bounding Box (AABB) method, and this made the border checking easy enough to implement. 

As both tracks of our team reached our final stage of development, merging the project actually took little time, because all there was left to do was to apply the enhanced texture to the cubes in the maze, and readjust some parameters for the camera instance and shadow mapping. 

In summary, we managed to demonstrate all the concepts we learned in class, and it's quite fascinating that flat sprites can be converted to three-dimensional textures by calculating height maps, also I gained a basic knowledge of how shadows are created in games and CGI movies.

### Demo Clip
[![](http://img.youtube.com/vi/XoElVAiN2Dc/0.jpg)](http://www.youtube.com/watch?v=XoElVAiN2Dc "Shadow Mapping, Normal Mapping, Parallax Mapping (3D Maze Sim)")

### Repository URL
[3D Maze Simulator with OpenGL](https://github.com/eric8607242/Opengl_mapping_implementation)

### Install / Download Instructions
#### Requirement
*P.S Linux Environment Recommended*
1. cmake
2. conan - package manager
```bash
pip3 install conan
```
3. download package
```bash
mkdir build && cd build
conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan
conan install .. --build glad -sbuild_type=Debug
```


#### Configure
```bash
cd build
cmake .. 
```

#### Build
```bash
cd build
cmake --build .
```

### Controls
+ W, A, S, D to move around
+ mouse to look around
+ Tab to toggle menu (Enable/Disable Normal, Parallax Mapping)


## 4. 3D Vision Check Game (Spring 2018)
### Intro
This was a project done by me and another classmate when we were taking the course "C# Programming", and it's the first project we've done with Unity Engine. We came across this game that does myopia examination with dropping objects, and the less time spent finding the opening, the higher score we get, then we decided to make a 3D version of this game.

### Design Statement
Our game can be divided to the following parts: game menu, main game, special abilities, collectables. My teammate programmed the main game, creating the game's general playability, and I programmed special abilities ,added collectable items, and added some special physical effects. Before switching to Unity Engine, which is a professional game engine, we've already used some other Graphical User Interfaces(e.g. Qt). The biggest difference we noticed is that Unity Engine has built-in timer-based methods, which normally we need to implement it ourselves in other GUIs, since they weren't meant to be used to develop games. Also, Unity Engine integrated physics bodies as components of an object, which normally we need to connect to a external physics library back in GUIs. 

Professional game engines like Unity open up a new vision for technical artists, but besides the fascinating features, game engines also inspired me to look more into the field of Computer Graphics, which lead to me attending the course "Practical Computer Graphics Skills for Technical Artists".

### Demo Clip
[![](http://img.youtube.com/vi/lrxwcvE3swc/0.jpg)](http://www.youtube.com/watch?v=lrxwcvE3swc "3D Vision Check Game with Unity Engine")

### Repository URL
[3D Vision Check Game with Unity Engine](https://bitbucket.org/randy1005/3dsightchecking/src/master/)

### Install / Download Instructions
- install Git for Windows
- run Git Bash anywhere and type in the following command
```
  git clone https://bitbucket.org/randy1005/3dsightchecking.git
```
- the executable file will be in *3DSightChecking/output/game.exe*
- run the executable file


## 5. Taiko Master (Fall 2016) 
### Intro
"Taiko Master" was a course project I did when attending my second program design class, which I first get in touch with C++. The coding style might seem a bit "unpolished", but it's a perfect example for me to learn timer concepts, manipulation of graphical components, processing user inputs, and creating a game scene.

### Design Statement
Taiko Master is a simple remake of the Japanese music arcade game “Taiko No Tatsujin”, which players catch up with the music rhythm and eliminate icons on the screen with drum beats. My own version of Taiko Master requires player to eliminate 4 different kind of faces with S, D, K, L on the keyboard.

First of all, for the different faces, I created the “Bigi” class inheriting “QGraphicsPixmapItem” for appearances of the faces. As for the movement of the faces, Qt provides SIGNALs and SLOTs, which are basically emitters and receivers, so I defined “advance()” as the slot in Bigi objects, and when the timer object fires a timeout, it also emits a signal that triggers “advance()”, and I simply update the position of the graphic items.

Also, instead of using the scene class provided by Qt “QGraphicsScene”, I inherited “QGraphicsScene” and put in some scene setting methods, and implemented key, mouse pressing events. The method of generating the Bigi objects “geneBigi” is also in this scene class. Furthermore, the detection of the Bigi objects hitting the hitbox is also done in this scene class.

Basically, the importance of this Taiko Master project to me is that I learned to apply object oriented concepts to making games. The “Bigi” objects  and other background objects all inherit “QGraphicsPixmapItem”, but only the “Bigi” objects possess the SLOTs “advance” so they can move around as the timer fires signals. There certainly is some optimization left to be done, but the basic framework guided me to more game programming later in college, either with real game engines or Java IDEs or Javascript component designs.

### Demo Clip
[![](http://img.youtube.com/vi/neQ5vuwoINQ/0.jpg)](http://www.youtube.com/watch?v=neQ5vuwoINQ "Taiko Master in Qt/C++")

### Repository URL
[Taiko Master](https://github.com/Randy1005/pd2-Taiko)

### Install / Download Instructions
- install Git for Windows
- run Git Bash or GUI by right-clicking anywhere
- clone the project by running the following command
```
    git clone https://github.com/Randy1005/pd2-Taiko.git
```
- the executable file taiko_master.exe will be in pd2-Taiko/taikoMasterRelease/taiko_master.exe
- run the executable file
