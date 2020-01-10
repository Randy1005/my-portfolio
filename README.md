# Introduction

## Link to each section


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

## 1. Ziggy's Adventure (Spring 2020)
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

## 2. Poocman (Fall 2019)
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


## 3. Shadow Mapping / Normal Mapping / Parallax Mapping Implementation with Collision Detection (Spring 2019)
### Intro
This project was made as a final course project when I attended "Practical Skills for Technical Artists", and this was built as a team project with OpenGL. Normal Mapping and Parallax Mapping are different methods to make textures on a flat sheet "stick out", that is, to make it three-dimensional. Shadow Mapping is a method to create shadows in a scene, with the help of a depth map of the scene, and other optimization steps. As we demonstrate these implementations by making a 3D maze simulator, I coded collision detection, camera, and rendered the maze.

### Design Statement
Since textures improving and shadow mapping can be done in separate projects, first we decided to split tracks, two of us work on normal mapping and parallax mapping, the other teammate and I work on collision detection and shadow mapping. As my teammate finished the implementation of shadow mapping quite fast, we started to work on collision detections and game camera. Camera was not an initially integrated concept in OpenGL, but we browsed some tutorials and managed to code it by calculating the camera coordinates and matrices. Collision Detection was a lot more easier. Based on the maze we rendered, the cells are all consistently cubes, so we applied the basic Axis-Aligned Bounding Box (AABB) method, and this made the border checking easy enough to implement. As both tracks of our team reached our final stage of development, merging the project actually took little time, because all there was left to do was to apply the enhanced texture to the cubes in the maze, and readjust some parameters for the camera instance and shadow mapping. In summary, we managed to demonstrate all the concepts we learned in class, and it's quite fascinating that flat sprites can be converted to three-dimensional textures by calculating height maps, also I gained a basic knowledge of how shadows are created in games and CGI movies.

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


## 4. 3D Vision Check Game (Spring 2018)
### Intro
This was a project done by me and another classmate when we were taking the course "C# Programming", and it's the first project we've done with Unity Engine. We came across this game that does myopia examination with dropping objects, and the less time spent finding the opening, the higher score we get, then we decided to make a 3D version of this game.

### Design Statement
Our game can be divided to the following parts: game menu, main game, special abilities, collectables. My teammate programmed the main game, creating the game's general playability, and I programmed special abilities ,added collectable items, and added some special physical effects. Before switching to Unity Engine, which is a professional game engine, we've already used some other Graphical User Interfaces(e.g. Qt). The biggest difference we noticed is that Unity Engine has built-in timer-based methods, which normally we need to implement it ourselves in other GUIs, since they weren't meant to be used to develop games. Also, Unity Engine integrated physics bodies as components of an object, which normally we need to connect to a external physics library back in GUIs.  

### Demo Clip
### Repository URL
### Install / Download Instructions

## 5. Taiko Master (Fall 2016) 
