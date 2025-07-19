# Creating Custom Levels

The levels for this game are created using an awesome [Tiled](https://www.mapeditor.org/) program. It's a general-purpose map editor.

The easiest way to understand how to create your own level is to watch this video: TODO.

## Let's start quickly

### Setup the levels environment

The tiled editor will require project assets. So the easier way (for now) is cloning the project, and putting the levels in a tree similar of in-game levels.

* Clone the project at https://github.com/quasilyte/decipherism-game
* Create the subdirectory `src/_assets/levels/levels`, which will contain your levels.
  * Note that this directory **MUST be named `levels`**.
* Set Environment variable "DECIPHERISM_DATA" to the parent path of this directory (The absolute path of `src/_assets/levels`)

* Download Tiled

### Create a level

* Create a file "xxxxx.json" in the `levels` directory created aboove, containing the following json :

```json
{ "compressionlevel":-1,
 "height":8,
 "infinite":false,
 "layers":[
        {
         "draworder":"topdown",
         "id":2,
         "name":"scheme",
         "objects":[
                {
                 "gid":11,
                 "height":96,
                 "id":51,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":192,
                 "y":384
                },
                {
                 "gid":12,
                 "height":96,
                 "id":115,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":768,
                 "y":384
                },
                {
                 "gid":21,
                 "height":96,
                 "id":116,
                 "name":"",
                 "properties":[
                        {
                         "name":"keywords",
                         "type":"string",
                         "value":"mask\nheat\nrisk\nsecure\nprice\nocean\nsea"
                        },
                        {
                         "name":"num_keywords",
                         "type":"int",
                         "value":2
                        }],
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":0,
                 "y":768
                },
                {
                 "gid":5,
                 "height":96,
                 "id":118,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":288,
                 "y":384
                },
                {
                 "gid":5,
                 "height":96,
                 "id":124,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":384,
                 "y":384
                },
                {
                 "gid":19,
                 "height":96,
                 "id":125,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":480,
                 "y":384
                },
                {
                 "gid":5,
                 "height":96,
                 "id":127,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":576,
                 "y":384
                },
                {
                 "gid":5,
                 "height":96,
                 "id":128,
                 "name":"",
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":672,
                 "y":384
                },
                {
                 "gid":57,
                 "height":96,
                 "id":131,
                 "name":"",
                 "properties":[
                        {
                         "name":"text",
                         "type":"string",
                         "value":"the encoding can\ngo in two ways here!"
                        }],
                 "rotation":0,
                 "type":"",
                 "visible":true,
                 "width":96,
                 "x":768,
                 "y":672
                }],
         "opacity":1,
         "type":"objectgroup",
         "visible":true,
         "x":0,
         "y":0
        }],
 "nextlayerid":3,
 "nextobjectid":154,
 "orientation":"orthogonal",
 "renderorder":"right-down",
 "tiledversion":"1.11.2",
 "tileheight":96,
 "tilesets":[
        {
         "firstgid":1,
         "source":"..\/..\/schemas.tsj"
        }],
 "tilewidth":96,
 "type":"map",
 "version":"1.10",
 "width":12
}
```

## Edit a custom level in Tiled

* Open this file in Tiled
* Activate View > Snapping > Snap to grid
* To add a new element :
  * select a tile in the tileset
  * press `t` to enter "tile adding" mode
  * click where you want the tile to be added
* To rotate
  * Press `s` to go back to "select" mode
  * use **horizontal** symmetry and rotation icons to put the tile like it has to be
    * rotation will not be sufficient, see below
* Only use the mouse to move tiles (keyboard movements won't snap to grid) 

### Respect the (unwritten) constraints

* normal pipes have a little arrow (I took it for a square at first glance) at their input. That's why you may need to use **horizontal** symmetry icon.
  TODO : use screenshots to be clearer
* diamond tiles have one input (where a pipe must end - without the little arrow) and two outputs: the "+" branch" (indicated with a + and a double arrow)  
  TODO : use screenshots to be clearer
* use of vertical symmetry is deprecated, only use **horizontal** symmetry

### Additional info

* The level's hint is a custom property on the "hint" element. Modify at your convenience
* The level's input words' list is a custom property on the "settings" element (separated by \n). Modify at your convenience 

## Check for errors

* if not already done, download and install the go compiler (TODO : provide link)
* build the mapcheck command :
  `cd src/cmd/mapcheck && go build -o ../../../bin/mapcheck . && cd ../../..`
* check your level file :
  `bin/mapcheck -tileset src/_assets/schemas.tsj src/_assets/levels/*.json`
  
