# Solar2D Material and Hex Colors

## Overview

This Solar2D plugin makes it easy to set a color. Supports all platforms.

## Add following to your `build.settings` to use:

```lua
{
    plugins = {
        ["plugin.materialcolors"] = {
            publisherId = "io.joehinkle",
        },
    },
}
```

## Example Use

Setup:

```lua
local materialColors = require "plugin.materialcolors"
materialColors.initHooks()
```

Examples:

```lua
-- Hex
local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( "#FF0000" )
circle.stroke = 5
circle:setStrokeColor( "#00FF00" )

-- Hex with alpha
local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( "#FF00007F" ) -- about 50% alpha because of the 7F appended at the end
circle.stroke = 5
circle:setStrokeColor( "#00FF0000" ) -- 0% alpha because of the 00 appended at the end

-- Material Color
local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( "red350" )
circle.stroke = 5
circle:setStrokeColor( "green500" )

-- Material Color with alpha
local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( "red350-50" ) -- 50% alpha because of the -50 appended at the end
circle.stroke = 5
circle:setStrokeColor( "green500-0" ) -- 0% alpha because of the -0 appended at the end
```

Advanced:

```lua
-- add your own material color to use in Corona's APIs
-- for example, you could add "azul" (Spanish for blue) to the library
materialColors.addNewMaterialColor( "azul", {
    "#E1F5FE",  -- will be used for "azul50"
    "#B3E5FC", -- will be used for "azul100"
    "#81D4FA", -- will be used for "azul200"
    "#4FC3F7", -- will be used for "azul300"
    "#29B6F6", -- will be used for "azul400"
    "#03A9F4", -- will be used for "azul500"
    "#039BE5", -- will be used for "azul600"
    "#0288D1", -- will be used for "azul700"
    "#0277BD", -- will be used for "azul800"
    "#01579B"  -- will be used for "azul900"
})
-- after running addNewMaterialColor, it will automatically work
local circle = local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( "azul350" ) -- this works now

-- you can mix colors
print( materialColors.mixColors( "red500", "blue500" ) )
-- result: 0.54313725490196    0.42549019607843    0.58235294117647    1
print( materialColors.mixColors( "red500", "blue500", .1 ) )
-- result: 0.2121568627451    0.5556862745098    0.87882352941176    1
print( materialColors.mixColors( {1,0,0}, {0,0,1} ) )
-- result: 0.5    0    0.5    nil
print( materialColors.mixColors( {1,0,0}, {0,0,1}, .1 ) )
-- result: 0.1    0    0.9    nil

-- you can get an accent color
local titleBarColor = "blue350"
local notificationBarColor = materialColors.getAccentColor( titleBarColor )
-- notificationBarColor will be a slightly darker blue

-- you can get Hex or Material Color as Corona's default RGB
print( materialColors.getColor("red350") )
-- result: 0.91764705882353    0.38823529411765    0.38235294117647    1
print( materialColors.getColor("#FF0000AA") )
-- result: 1    0    0    0.66666666666667
local circle = local circle = display.newCircle( 100, 100, 50 )
circle:setFillColor( materialColors.getColor("#FF0000AA") ) -- this works without having to run materialColors.initHooks()
```

For a list of all of Material Design's colors, see https://material.io/design/color/#tools-for-picking-colors 

## Links 

- Form post: https://forums.solar2d.com/t/plugin-to-easily-set-colors/351803
