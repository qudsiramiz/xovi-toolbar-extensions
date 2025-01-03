# xovi extensions for the toolbar


The QMD files in this repo add a quicktools-like floating bar, and a layer management bar. Instructions to install xovi can be found in [here](https://github.com/asivery/rmpp-xovi-extensions/blob/master/INSTALL.MD). 
After which, copy the files to 
`/home/root/xovi/exthome/qt-resource-rebuilder/` and restart xovi. The `Edit.qmd` file adds a trash-can icon to the selection helper, which lets the user delete the stroke selected instead of cutting and clearing the clipboard

These QMDs were tested to work in 3.15/16 and 3.17. Please download the respective version of the simplified.qmd file for the versions. Any bugs should be reported in the repo issues. 



## Features

- Allows adding any tool with a preset colour and thickness
- Allows anchoring to the top of the screen
- Can be placed anywhere in the screen
- Can be minimised when not in use
- NEW: Tool orders are persistent with restarts

## How-To
#### To enable the floating toolbars, use the menu in the toolbar
![Menu](images/menu.png)

## Quick-Tools 
#### Fully open(Toolbar visible)
![QuickTools](images/Quicktoolsfull.png)

#### Partially closed(Toolbar closed)
![QuickTools](images/Quicktools.png)

#### Fully minimised(Double tap the left-most icon)
![hiding](images/hiding.gif)

#### To add Tools
![hiding](images/addingtools.gif)

#### To anchor to the top
![anchor](images/topanchor.gif)

#### To change tool order
To change the tool order, press and hold on the tool buttons to show the arrows, and change the order using them
![anchor](images/moveOrder.gif)



## Layers
#### Layer-management floating toolbar
![layers](images/Layers.png)

### Moving the toolbars
#### Press and hold the left-most icon until it's highlighted. After which, press and drag the icon to move it around
![moving](images/moving.gif)
