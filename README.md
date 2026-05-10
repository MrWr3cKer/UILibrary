📘 User Manual for my UI Library

This guide explains how to use the UI library to build a script menu in Roblox.

1. Initial Setup (Loading the Library)
   
To use the library, you must "call" it into your current script using loadstring. This allows you to use all the pre-made functions without having to write them yourself.
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/MrWr3cKer/UILibrary/refs/heads/main/Library"))()
```

This creates the the gui window, `Title` is your name on your cheat and `Description` is description when the gui loads.
```lua
local Window = Library:CreateWindow({
    Title = "My Master Script", -- The name shown at the top
    Description = "Loading premium systems..." -- Text shown on the loading bar
})
```

2. Organizing with Sections
   
Sections act like "tabs" in a web browser. They help you group similar functions together in the sidebar.
```lua
local Section = Window:section("SectionName") -- Create a section
```

If you got a very big code it may be easier to use this.
```lua
local Section = Window:section("SectionName", 1)
```

Thats becouse normal section comes from top to bottom like this
```lua
local Section = Window:section("SectionName")
local Section2 = Window:section("SectionName2")
```

In the gui menu Section is first, and Section2 comes under.
But if you use this:
```lua
local Section = Window:section("SectionName", 2)
local Section2 = Window:section("SectionName2", 1)
```

Then Section2 comes first, and Section comes second.

3. Adding Components (Buttons, Toggles, Sliders)
   
Inside each section, you can add different controls for the user to interact with.

The Toggle (On/Off Switch)
Use this for features that stay active, like "God Mode" or "Auto-Farm".

Important: The flag is a unique name used to save this setting in your configuration file.
```lua
Combat:create_toogle({
    text = "Aimbot Enabled", -- Label for the toggle
    flag = "AimbotToggle", -- Unique ID for saving/loading
    state = false, -- Starting position (off)
    tooltip = "Automatically aims at players", -- Description shown on hover
    Callback = function(Value)
        -- 'Value' is true if on, false if off
        print("Aimbot is now:", Value)
    end
})
```

The Slider (Value Selection)
Use this for settings that need a number, like how fast you walk or how far you can see.
```lua
Visuals:create_slider({
    text = "FOV Range",
    flag = "AimbotFOV",
    min_value = 0,
    max_value = 180,
    start_value = 90, -- The number it starts at
    increment = 1, -- How much it jumps when you drag it
    Callback = function(Value)
        print("Sighting range set to:", Value)
    end
})
```

The Dropdown (List Selection)
Use this when the user needs to choose one option from a specific list.
```lua
Combat:create_dropdown({
    text = "Target Part",
    flag = "AimTarget",
    list = {"Head", "Torso", "HumanoidRootPart"}, -- The choices
    Callback = function(Selected)
        print("Now targeting the:", Selected)
    end
})
```

The Color Picker (Not good yet, will fix it later)
```lua
Visuals:create_colorpicker({
    text = "ESP Color",
    flag = "PlayerESPColor",
    color = Color3.fromRGB(0, 255, 120), -- Default color
    alpha = 0.5, -- Default 50% transparency
    Callback = function(Color, Transparency)
        print("Color changed. Transparency is:", Transparency)
    end
})
```

The Keybind (Keyboard Shortcut)
Lets the user set a specific key to trigger a function in-game.
```lua
Combat:create_keybind({
    text = "Panic Button",
    flag = "PanicKey",
    default = Enum.KeyCode.P, -- The starting key
    Callback = function(Key)
        print("You pressed the shortcut key:", Key.Name)
    end
})
```

4. Global Utility Functions
You can use these functions anywhere in your script to send messages or change the look of the menu.

Notify: Sends a popup alert in the bottom-right corner of the screen with a timer bar.
```lua
Library:Notify("Success", "Script loaded correctly!", 5) -- Lasts 5 seconds, change 5 to a spesific time (in seconds)
```
SetTheme: Changes the color scheme of the entire menu instantly.
```lua
Library:SetTheme("Ocean") -- Options: Default, Ocean, Blood, Forest, Amethyst, Midnight
```

5. Essential Beginner Tips

1. Unique Flags: Every Toggle, Slider, Dropdown, Keybind, and ColorPicker must have a different flag name. If two items share a flag, the saving system will get confused and crash.
2. Settings Section: The library automatically adds a "Settings" tab at the bottom. This is where users can save their favorite setups (Configs), change the theme, or enable the Watermark (which shows FPS and Ping).
3. Search Bar: If you add many sections, users can type in the search box at the top of the sidebar to quickly find the tab they need.
