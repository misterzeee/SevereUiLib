# Severe Ui Severe Ui Lib

Ping @_misterzeee in the severe discord for any issues or suggestions.

As seen in https://github.com/misterzeee/cbro

## Overview

**TOGGLE KEY IS DELETE**


**To load the Ui use the following**:

```luau
bytecode = game:HttpGet("https://github.com/misterzeee/SevereUiLib/raw/refs/heads/main/MainByteCode.lua")
local func = luau.load(bytecode)
func()
local UI = zeeUi
--your code here
return zeeUi
```

## Features

### Set Theme

**You may select a theme from the following**:

- Midnight
- Emerald
- NEW Medic
- NEW Custom

**Custom Example**

```luau
UI.setTheme({
    Background = {0,0,0},
    Panel = {0,0,0},
    Accent = {0,0,0},
    Pressed = {0,0,0},
    Text = {0,0,0},
    SubText = {0,0,0},
    TabsBar = {0,0,0},
    Tooltip = {0,0,0},
})
```

**Using Theme Example**:

```luau
UI.setTheme("Emerald")
```

### Create A Window

Creating a window is a vital step to creating a ui which is required for it to work properly.

**Window Creation Example**:

```luau
local win = UI.createWindow({ title = "Example" })
```

### Creating Tabs
Tabs Are important to keep things organized on your ui. For example you would want everythig related to Aimbot to be in an Aimbot tab.

**Tab Creation Example**

```luau
local tab1 = win:addTab("Tab1")
local tab2 = win:addTab("Tab2")
```

### Creating And Modifying Text
Text is good for telling a user that a feature might be unsafe, uncompleted or just give information on a feature.

**Text Creation Example**

```lua
local title = tab1:addText({ text = "Ready" })
```

You may then want to change the text on a button press for exmaple.

**Change Text Example From Inside A Button**

```luau
local run = tab1:addButton({ text = "Run" })
run.OnClick:Connect(function()
    title:setText("Running")
end)
```

### Creating And Using Buttons

Buttons are useful for features that require activation.

**Button Example**

```luau
local run = tab1:addButton({ text = "Run" })
run.OnClick:Connect(function()
    --Code that runs once button is pressed
end)
```

### Creating And Using Check Boxes

Checkboxes are good for features that are a boolean value and need to be either true or false.

**Checkbox Example**

```luau
local enabled = tab2:addCheckbox({ text = "Enable", default = true })
enabled.OnChanged:Connect(function(v)
    print("Enable:", v) -- This Example Prints The Value When It Changes
end)
```

### Creating And Using Sliders

Sliders are used to set float or integer values like changing a volume or speed. This can be done in percent or number form which is changed with mode.

**Slider Exmaple For Percent**

```luau
local vol = tab2:addSlider({ text = "Volume", min = 0, max = 100, mode = "percent", default = 50 })
vol.OnChanged:Connect(function(v)
    print("Volume", v) -- This Example Prints When Changed
end)
```

**Slider Example For Number**

```luau
local speed = tab2:addSlider({ text = "Speed", min = 0, max = 10, mode = "number", default = 3 })
speed.OnChanged:Connect(function(v)
    print("Speed", v) -- This Example Prints When Chnaged
end)
```

### Creating Dropdowns

Dropdowns are used for selecting string values from a list.

**Dropdown Example**

```luau
local quality = tab2:addDropdown({ text = "Quality", items = {"Low","Medium","High"}, defaultIndex = 2 })
quality.OnChanged:Connect(function(value, index) print("Quality:", value, index) end)
```

**Multi Select Dropdown Example**

```luau
local multiSelect = tab2:addDropdown({ text = "Body Parts", items = {"Head","Torso","Weener"}, defaultIndices = {1, 2} })
multiSelect.OnChanged:Connect(function(indices, values) print("Selected indices:", indices, "Selected values:", values) end)
```

### Colour Picker

The colour picker is used to select colours for visuals like chams etc. Also has copy and paste to use the same colour across different colour pickers.

**Colour Picker Example**

```luau
local espColor = tab2:addColorPicker({
    text = "ESP Color",
    default = {255, 0, 0},
})
espColor.OnChanged:Connect(function(color)
    print(string.format("ESP Color: R=%d G=%d B=%d", color[1], color[2], color[3]))
end)
```

## Example
```luau
bytecode = game:HttpGet("https://github.com/misterzeee/SevereUiLib/raw/refs/heads/main/MainByteCode.lua")

func = luau.load(bytecode)
func()


-- Example
local UI = zeeUi

UI.setTheme("Midnight")

local win = UI.createWindow({ title = "My Tool" })

local tab1 = win:addTab("Tab1")
local tab2 = win:addTab("Tab2")

local title = tab1:addText({ text = "Ready" })

local run = tab1:addButton({ text = "Run" })
run.OnClick:Connect(function()
    title:setText("Running...")
end)

local enabled = tab2:addCheckbox({ text = "Enable", default = true })
enabled.OnChanged:Connect(function(v) print("Enable:", v) end)

local vol = tab2:addSlider({ text = "Volume", min = 0, max = 100, mode = "percent", default = 50 })
vol.OnChanged:Connect(function(v) print("Volume", v) end)

local speed = tab2:addSlider({ text = "Speed", min = 0, max = 10, mode = "number", default = 3 })
speed.OnChanged:Connect(function(v) print("Speed", v) end)

local quality = tab2:addDropdown({ text = "Quality", items = {"Low","Medium","High"}, defaultIndex = 2 })
quality.OnChanged:Connect(function(value, index) print("Quality:", value, index) end)

local multiSelect = tab2:addDropdown({ text = "Body Parts", items = {"Head","Torso","Weener"}, defaultIndices = {1, 2} })
multiSelect.OnChanged:Connect(function(indices, values) print("Selected indices:", indices, "Selected values:", values) end)

local espColor = tab2:addColorPicker({
    text = "ESP Color",
    default = {255, 0, 0},
})
espColor.OnChanged:Connect(function(color, opacity)
    print(string.format("ESP Color: R=%d G=%d B=%d A=%.2f", color[1], color[2], color[3], opacity or 1.0))
end)

local chamsColor = tab2:addColorPicker({
    text = "Chams Color",
    default = {0, 255, 0},
})
chamsColor.OnChanged:Connect(function(color, opacity)
    print(string.format("Chams Color: R=%d G=%d B=%d A=%.2f", color[1], color[2], color[3], opacity or 1.0))
end)

local run2 = tab2:addButton({ text = "Get Colors" })
run2.OnClick:Connect(function()
    local esp = espColor:getColor()
    local chams = chamsColor:getColor()
    print(string.format("ESP: R=%d G=%d B=%d A=%.2f", esp[1], esp[2], esp[3], esp[4] or 1.0))
    print(string.format("Chams: R=%d G=%d B=%d A=%.2f", chams[1], chams[2], chams[3], chams[4] or 1.0))
end)

return zeeUi
```
