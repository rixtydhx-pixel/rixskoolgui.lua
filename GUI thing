if not game:IsLoaded() then game.Loaded:Wait() end
local Players          = game:GetService("Players")
local RunService       = game:GetService("RunService")
local TweenService     = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Workspace        = game:GetService("Workspace")
local Lighting         = game:GetService("Lighting")
local TeleportService  = game:GetService("TeleportService")
local VirtualUser      = game:GetService("VirtualUser")
local SoundService     = game:GetService("SoundService")

local player = Players.LocalPlayer
while not player do task.wait() player = Players.LocalPlayer end

--------------------------------------------------
-- MODES
--------------------------------------------------
local Modes = {
    ESP          = false,
    FullBright   = false,
    Chams        = false,
    TracerESP    = false,
    ItemESP      = false,
    LowLighting  = false,

    InfiniteJump = false,
    TeleportTool = false,
    NoClip       = false,

    Optimization = false,
    NoShadows    = false,
    NoFog        = false,

    Rejoin       = false,
    ServerHop    = false,
    Forsaken     = false,
    ResetChar    = false,
    AntiAFK      = false,

    ChatLogger   = false,
}
_G.Modes = _G.Modes or {}

--------------------------------------------------
-- GUI PARENT
--------------------------------------------------
local parentGui
pcall(function() parentGui = gethui() end)
if not parentGui then parentGui = game:GetService("CoreGui") end

--------------------------------------------------
-- SCREEN GUI (NORMAL, NO KEY SYSTEM)
--------------------------------------------------
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "Ricksxdude"
screenGui.IgnoreGuiInset = true
screenGui.ResetOnSpawn = false
screenGui.Parent = parentGui

--------------------------------------------------
-- CINEMATIC STARTUP SEQUENCE (OPTIMIZED)
--------------------------------------------------

task.spawn(function()

    -- Container for cleanup
    local introContainer = Instance.new("Folder")
    introContainer.Name = "IntroSequence"
    introContainer.Parent = screenGui

    -- 1. Soft Ambient Fade-In
    screenGui.Enabled = false
    task.wait(0.05)
    screenGui.Enabled = true

    -- 2. Notification
    pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Cr3ativeTw1nn GUI",
            Text  = "Initializing systems...",
            Duration = 3
        })
    end)

    -- 3. Startup Sound
    pcall(function()
        local sound = Instance.new("Sound")
        sound.SoundId = "rbxassetid://4989569018"
        sound.Volume = 2.2
        sound.PlayOnRemove = true
        sound.Parent = SoundService
        sound:Destroy()
    end)

    -- 4. Cinematic Fade Flash
    local flash = Instance.new("Frame")
    flash.Size = UDim2.fromScale(1,1)
    flash.BackgroundColor3 = Color3.fromRGB(255,255,255)
    flash.BackgroundTransparency = 1
    flash.ZIndex = 9999
    flash.Parent = introContainer

    TweenService:Create(flash, TweenInfo.new(0.15, Enum.EasingStyle.Quad), {
        BackgroundTransparency = 0.6
    }):Play()

    task.wait(0.15)

    TweenService:Create(flash, TweenInfo.new(0.45, Enum.EasingStyle.Quad), {
        BackgroundTransparency = 1
    }):Play()

    task.wait(0.45)
    flash:Destroy()

    -- 5. Panel Reveal Pulse
    if panel then
        panel.BackgroundTransparency = 1
        TweenService:Create(panel, TweenInfo.new(0.35, Enum.EasingStyle.Quad), {
            BackgroundTransparency = 0
        }):Play()

        if outline then
            outline.Transparency = 1
            TweenService:Create(outline, TweenInfo.new(0.35, Enum.EasingStyle.Quad), {
                Transparency = 0.15
            }):Play()
        end
    end

    -- 6. Auto-destroy intro sequence after 2 seconds
    task.wait(2)
    introContainer:Destroy()

end)

--------------------------------------------------
-- MAIN GUI PANEL (OPTIMIZED, SAME VISUALS)
--------------------------------------------------

local panel = Instance.new("Frame")
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Position = UDim2.fromScale(0.5, 0.5)
panel.Size = UDim2.fromScale(0.56, 0.42)
panel.BackgroundTransparency = 1 -- start faded
panel.BorderSizePixel = 0
panel.ClipsDescendants = true
panel.Parent = screenGui

-- Combine BOTH gradients into ONE (same look, half the cost)
local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(25, 25, 35)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(30, 25, 60)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(55, 45, 95))
})
gradient.Rotation = 45
gradient.Parent = panel

-- UIStroke (unchanged visuals)
local outline = Instance.new("UIStroke")
outline.Color = Color3.fromRGB(200, 200, 255)
outline.Thickness = 3
outline.Transparency = 1 -- start faded
outline.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
outline.Parent = panel

-- Rounded corners
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 14)
corner.Parent = panel

-- Tween fade-in (merged into one tween call per object)
TweenService:Create(panel, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
    BackgroundTransparency = 0
}):Play()

TweenService:Create(outline, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
    Transparency = 0.15
}):Play()

--------------------------------------------------
-- TITLE (NO BACKGROUND, TEXT OUTLINE)
--------------------------------------------------
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 42)
title.Position = UDim2.new(0, 10, 0, 12)
title.BackgroundTransparency = 1 -- removed background
title.BorderSizePixel = 0
title.Text = "Ricksxdude Gui"
title.TextColor3 = Color3.fromRGB(230, 220, 255)
title.Font = Enum.Font.GothamBold
title.TextScaled = true
title.TextTransparency = 1
title.Parent = panel

-- Gradient on text (still allowed)
local titleGrad = Instance.new("UIGradient")
titleGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(85, 65, 140)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(50, 35, 85))
})
titleGrad.Rotation = 90
titleGrad.Parent = title

-- TEXT OUTLINE (renamed to avoid conflicts)
local titleOutline = Instance.new("TextLabel")
titleOutline.Size = title.Size
titleOutline.Position = title.Position
titleOutline.BackgroundTransparency = 1
titleOutline.Text = title.Text
titleOutline.TextColor3 = Color3.fromRGB(80, 60, 120)
titleOutline.Font = title.Font
titleOutline.TextScaled = true
titleOutline.TextTransparency = 1
titleOutline.ZIndex = title.ZIndex - 1
titleOutline.Parent = panel

-- Sync outline text + size
title:GetPropertyChangedSignal("Text"):Connect(function()
    titleOutline.Text = title.Text
end)

title:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
    titleOutline.Size = title.Size
end)

-- Cinematic slide + fade
title.Position = UDim2.new(0, 10, 0, 4)
titleOutline.Position = UDim2.new(0, 10, 0, 4)

TweenService:Create(title, TweenInfo.new(0.35, Enum.EasingStyle.Quad), {
    Position = UDim2.new(0, 10, 0, 12),
    TextTransparency = 0
}):Play()

TweenService:Create(titleOutline, TweenInfo.new(0.35, Enum.EasingStyle.Quad), {
    Position = UDim2.new(0, 10, 0, 12),
    TextTransparency = 0.4
}):Play()

--------------------------------------------------
-- MINIMIZE VARIABLES (MUST BE AFTER PANEL EXISTS)
--------------------------------------------------
local guiSuspended = false
local defaultSize = panel.Size
local defaultPos  = panel.Position
local isMinimized = false

--------------------------------------------------
-- MAC-STYLE DOT BUTTONS (OPTIMIZED + SMALLER)
--------------------------------------------------
local dotHolder = Instance.new("Frame")
dotHolder.Size = UDim2.new(0, 90, 0, 26)
dotHolder.Position = UDim2.new(1, -100, 0, 10)
dotHolder.BackgroundTransparency = 1
dotHolder.Parent = panel

local function createDot(color, xOffset, onClick)
    local dot = Instance.new("Frame")
    dot.Size = UDim2.new(0, 20, 0, 20)
    dot.Position = UDim2.new(0, xOffset, 0, 3)
    dot.BackgroundColor3 = color
    dot.BorderSizePixel = 0
    dot.Parent = dotHolder

    Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

    local stroke = Instance.new("UIStroke")
    stroke.Color = Color3.fromRGB(255, 255, 255)
    stroke.Thickness = 1
    stroke.Transparency = 0.2
    stroke.Parent = dot

    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 1, 0)
    btn.BackgroundTransparency = 1
    btn.Text = ""
    btn.Parent = dot

    -- Hover animation
    btn.MouseEnter:Connect(function()
        TweenService:Create(dot, TweenInfo.new(0.12, Enum.EasingStyle.Quad), {
            BackgroundColor3 = color:Lerp(Color3.new(1,1,1), 0.18)
        }):Play()
    end)

    btn.MouseLeave:Connect(function()
        TweenService:Create(dot, TweenInfo.new(0.12, Enum.EasingStyle.Quad), {
            BackgroundColor3 = color
        }):Play()
    end)

    -- Connect click action if provided
    if onClick then
        btn.MouseButton1Click:Connect(onClick)
    end

    return btn
end

--------------------------------------------------
-- MINIMIZE / RESTORE LOGIC (PATCHED)
--------------------------------------------------

local function toggleMinimize()
    if isMinimized then
        -- Restore panel size & position smoothly
        TweenService:Create(panel, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
            Size = defaultSize,
            Position = defaultPos
        }):Play()

        restoreGUI()
        isMinimized = false

    else
        -- Suspend UI for optimization
        suspendGUI()

        -- Shrink panel smoothly (dock in place)
        TweenService:Create(panel, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
            Size = UDim2.new(0, 120, 0, 40),
            Position = UDim2.new(
                panel.Position.X.Scale,
                panel.Position.X.Offset,
                panel.Position.Y.Scale,
                panel.Position.Y.Offset
            )
        }):Play()

        isMinimized = true
    end
end

--------------------------------------------------
-- DOT BUTTONS (PATCHED + CLEAN)
--------------------------------------------------

-- Green = minimize/restore
local greenBtn = createDot(Color3.fromRGB(52,199,89), 0, toggleMinimize)

-- Yellow = no action (placeholder)
local yellowBtn = createDot(Color3.fromRGB(255,204,0), 30, function()
    if playClick then pcall(playClick) end
end)

-- Red = destroy GUI
local redBtn = createDot(Color3.fromRGB(255,59,48), 60, function()
    if playClick then pcall(playClick) end
    if screenGui and screenGui.Destroy then
        screenGui:Destroy()
    end
end)

--------------------------------------------------
-- REQUIRED TAB BACKBONE (THIS WAS MISSING)
--------------------------------------------------
local spacer = Instance.new("Frame")
spacer.Size = UDim2.new(1, 0, 0, 80)
spacer.Position = UDim2.new(0, 0, 0, 60)
spacer.BackgroundTransparency = 1
spacer.Parent = panel

local tabScroller = Instance.new("ScrollingFrame")
tabScroller.Size = UDim2.new(1, 0, 0, 55)
tabScroller.Position = UDim2.new(0, 0, 0, 60)
tabScroller.BackgroundColor3 = Color3.fromRGB(45,45,60)
tabScroller.BackgroundTransparency = 0.25
tabScroller.BorderSizePixel = 0
tabScroller.ScrollBarThickness = 4
tabScroller.ScrollingDirection = Enum.ScrollingDirection.X
tabScroller.CanvasSize = UDim2.new(0, 0, 0, 0)
tabScroller.Active = true
tabScroller.Selectable = true
tabScroller.ClipsDescendants = true
tabScroller.Parent = panel

local tabLayout = Instance.new("UIListLayout")
tabLayout.FillDirection = Enum.FillDirection.Horizontal
tabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Left
tabLayout.VerticalAlignment = Enum.VerticalAlignment.Center
tabLayout.Padding = UDim.new(0, 10)
tabLayout.Parent = tabScroller

local highlight = Instance.new("Frame")
highlight.Size = UDim2.new(0, 0, 0, 4)
highlight.Position = UDim2.new(0, 0, 0, 115)
highlight.BackgroundColor3 = Color3.fromRGB(215,205,255)
highlight.BorderSizePixel = 0
highlight.Parent = panel

local hlCorner = Instance.new("UICorner")
hlCorner.CornerRadius = UDim.new(0, 2)
hlCorner.Parent = highlight

--------------------------------------------------
-- TABS (FULLY PATCHED + DARK FADED PURPLE THEME)
--------------------------------------------------
local tabNames = {
    "Visual","Lighting","Player","Aimbot","Utility",
    "World","Combat","Mobility","Social"
}

local tabButtons = {}
local tabFrames  = {}
local activeTab  = nil

for _, name in ipairs(tabNames) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 140, 1, -10)

    -- DARK + FADED PURPLE BASE
    btn.BackgroundColor3 = Color3.fromRGB(60, 45, 95)
    btn.BorderSizePixel = 0
    btn.AutoButtonColor = false
    btn.Text = name

    -- LIGHT PURPLE TEXT
    btn.TextColor3 = Color3.fromRGB(230, 210, 255)
    btn.Font = Enum.Font.GothamBold
    btn.TextScaled = true
    btn.Parent = tabScroller
    tabButtons[name] = btn

    -- SQUARE TABS (NO UICorner)

    -- DARK FADED PURPLE GRADIENT
    local grad = Instance.new("UIGradient")
    grad.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(85, 65, 140)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(50, 35, 85))
    })
    grad.Rotation = 90
    grad.Parent = btn

-- PURPLE LIGHT OUTLINE (REAL, CLEAN, DOES NOT BREAK)
btn.ClipsDescendants = false

local stroke = Instance.new("UIStroke")
stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
stroke.Thickness = 2
stroke.Transparency = 0.35
stroke.Color = Color3.fromRGB(190, 130, 255)
stroke.Parent = btn

local strokeGrad = Instance.new("UIGradient")
strokeGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(230, 190, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(140, 90, 200))
})
strokeGrad.Rotation = 90
strokeGrad.Parent = stroke


    -- Content frame (unchanged)
    local scroll = Instance.new("ScrollingFrame")
    scroll.Position = UDim2.new(0,0,0,180)
    scroll.Size = UDim2.new(1,0,1,-180)
    scroll.BackgroundColor3 = Color3.fromRGB(55,55,75)
    scroll.BackgroundTransparency = 0.25
    scroll.BorderSizePixel = 0
    scroll.ScrollBarThickness = 6
    scroll.Visible = false
    scroll.CanvasSize = UDim2.new(0,0,0,0)
    scroll.Parent = panel
    tabFrames[name] = scroll
end

--------------------------------------------------
-- AUTO-EXPAND SCROLLER WIDTH
--------------------------------------------------
tabLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    tabScroller.CanvasSize = UDim2.new(0, tabLayout.AbsoluteContentSize.X + 20, 0, 0)
end)

--------------------------------------------------
-- TAB SYSTEM (FULLY PATCHED)
--------------------------------------------------
local function switchTab(name)
    if activeTab == name then return end

    for tabName, frame in pairs(tabFrames) do
        frame.Visible = (tabName == name)
    end

    activeTab = name
    local btn = tabButtons[name]
    if not btn then return end

    -- ACTIVE / INACTIVE COLORS (dark faded purple theme)
    for tabName, button in pairs(tabButtons) do
        if tabName == name then
            -- ACTIVE TAB (brighter)
            button.TextColor3 = Color3.fromRGB(255, 240, 255)
            button.BackgroundColor3 = Color3.fromRGB(90, 70, 150)
        else
            -- INACTIVE TAB (faded)
            button.TextColor3 = Color3.fromRGB(230, 210, 255)
            button.BackgroundColor3 = Color3.fromRGB(60, 45, 95)
        end
    end

    highlight:TweenSizeAndPosition(
        UDim2.new(0, btn.AbsoluteSize.X, 0, 4),
        UDim2.new(
            0,
            btn.AbsolutePosition.X - tabScroller.AbsolutePosition.X,
            0,
            115
        ),
        Enum.EasingDirection.Out,
        Enum.EasingStyle.Quad,
        0.15,
        true
    )
end

for name, btn in pairs(tabButtons) do
    btn.MouseButton1Click:Connect(function()
        if playClick then playClick() end
        switchTab(name)
    end)
end

switchTab("Visual")


--------------------------------------------------
-- PREMIUM + OPTIMIZED COMMAND BAR
--------------------------------------------------
local commandBar = Instance.new("TextBox")
commandBar.Size = UDim2.new(1, -20, 0, 34)
commandBar.Position = UDim2.new(0, 10, 0, 135)
commandBar.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
commandBar.TextColor3 = Color3.fromRGB(230, 225, 255)
commandBar.PlaceholderText = "Enter command..."
commandBar.PlaceholderColor3 = Color3.fromRGB(150, 140, 200)
commandBar.Font = Enum.Font.GothamBold
commandBar.TextScaled = true
commandBar.BorderSizePixel = 0
commandBar.ClipsDescendants = true
commandBar.Parent = panel

-- Rounded corners
local cbCorner = Instance.new("UICorner")
cbCorner.CornerRadius = UDim.new(0, 10)
cbCorner.Parent = commandBar

-- Soft vertical gradient (GPU cheap)
local cbGradient = Instance.new("UIGradient")
cbGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(55, 55, 80)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(35, 35, 55))
})
cbGradient.Rotation = 90
cbGradient.Parent = commandBar

-- Thin premium border (super cheap)
local cbStroke = Instance.new("UIStroke")
cbStroke.Color = Color3.fromRGB(180, 160, 255)
cbStroke.Thickness = 1
cbStroke.Transparency = 0.45
cbStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
cbStroke.Parent = commandBar

-- Focus animation (optimized: only 2 tweens)
commandBar.Focused:Connect(function()
    TweenService:Create(cbStroke, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
        Transparency = 0.15
    }):Play()

    TweenService:Create(cbGradient, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
        Rotation = 0
    }):Play()
end)

commandBar.FocusLost:Connect(function()
    TweenService:Create(cbStroke, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
        Transparency = 0.45
    }):Play()

    TweenService:Create(cbGradient, TweenInfo.new(0.18, Enum.EasingStyle.Quad), {
        Rotation = 90
    }):Play()
end)

--------------------------------------------------
-- PREMIUM AUTOCOMPLETE DROPDOWN (OPTIMIZED)
--------------------------------------------------
local suggestionBox = Instance.new("Frame")
suggestionBox.Size = UDim2.new(1, -20, 0, 80)
suggestionBox.Position = UDim2.new(0, 10, 0, 170)
suggestionBox.BackgroundColor3 = Color3.fromRGB(45, 45, 65)
suggestionBox.BackgroundTransparency = 0.25
suggestionBox.BorderSizePixel = 0
suggestionBox.Visible = false
suggestionBox.ClipsDescendants = true
suggestionBox.Parent = panel

-- Rounded corners (keep)
local sugCorner = Instance.new("UICorner")
sugCorner.CornerRadius = UDim.new(0, 10)
sugCorner.Parent = suggestionBox

-- Keep only ONE parent gradient & stroke (cheaper)
local sugGradient = Instance.new("UIGradient")
sugGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(60, 60, 90)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(35, 35, 55))
})
sugGradient.Rotation = 90
sugGradient.Parent = suggestionBox

local sugStroke = Instance.new("UIStroke")
sugStroke.Color = Color3.fromRGB(180, 160, 255)
sugStroke.Thickness = 1
sugStroke.Transparency = 0.45
sugStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
sugStroke.Parent = suggestionBox

-- Layout: use UIListLayout but manage sizing manually
local sugLayout = Instance.new("UIListLayout")
sugLayout.Parent = suggestionBox
sugLayout.Padding = UDim.new(0, 4)
sugLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
sugLayout.VerticalAlignment = Enum.VerticalAlignment.Top

-- Pooling for suggestion buttons (reused)
local suggestionPool = {}
local activeSuggestions = {}

local function createPooledButton()
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -10, 0, 26)
    btn.BackgroundColor3 = Color3.fromRGB(55, 55, 75)
    btn.BackgroundTransparency = 0.2
    btn.TextColor3 = Color3.fromRGB(230, 225, 255)
    btn.Font = Enum.Font.GothamBold
    btn.TextScaled = false     -- fixed size (faster)
    btn.TextSize = 14
    btn.BorderSizePixel = 0
    btn.AutoButtonColor = false
    btn.Visible = false

    -- single UICorner (cheap)
    local bCorner = Instance.new("UICorner")
    bCorner.CornerRadius = UDim.new(0, 8)
    bCorner.Parent = btn

    -- subtle stroke kept but with high transparency (one per button is ok when pooled)
    local bStroke = Instance.new("UIStroke")
    bStroke.Color = Color3.fromRGB(180, 160, 255)
    bStroke.Thickness = 1
    bStroke.Transparency = 0.85
    bStroke.Parent = btn

    return btn
end

local function getPooledButton()
    local btn = table.remove(suggestionPool)
    if not btn then
        btn = createPooledButton()
    end
    btn.Visible = true
    btn.Parent = suggestionBox
    table.insert(activeSuggestions, btn)
    return btn
end

local function clearActiveSuggestions()
    -- move active children back to pool (no Destroy)
    for i = #activeSuggestions, 1, -1 do
        local b = activeSuggestions[i]
        b.Parent = nil
        b.Visible = false
        b.Text = ""
        table.insert(suggestionPool, b)
        activeSuggestions[i] = nil
    end
    -- update suggestionBox size to compact
    suggestionBox.Size = UDim2.new(1, -20, 0, 80)
end

-- Fade-in animation (keeps existing look, but light)
local fadeTween = nil
local function fadeInSuggestions()
    if fadeTween then fadeTween:Cancel() end
    suggestionBox.BackgroundTransparency = 1
    sugStroke.Transparency = 1
    fadeTween = TweenService:Create(suggestionBox, TweenInfo.new(0.14, Enum.EasingStyle.Quad), {
        BackgroundTransparency = 0.25
    })
    fadeTween:Play()
    TweenService:Create(sugStroke, TweenInfo.new(0.14, Enum.EasingStyle.Quad), {
        Transparency = 0.45
    }):Play()
end

-- Command list (unchanged)
local allCommands = {
    -- Visual
    "esp","chams","night","traceresp","lowlight","fullbright",
    -- Player
    "infinitejump","ij","tp","teleporttool","noclip","freecam","xray",
    -- Lighting
    "opt","optimization","noshadows","nofog",
    -- Utility
    "rejoin","reset","resetchar","antiafk","serverhop","forsaken",
    -- Social
    "chatlogger",
}

-- Debounce / throttle control for typing updates
local pendingText = nil
local debounceDelay = 0.06

local function doUpdateSuggestions(text)
    -- quickly clear old entries
    clearActiveSuggestions()

    if not text or text == "" then
        suggestionBox.Visible = false
        return
    end

    local lower = text:lower()
    local found = 0

    for _, cmd in ipairs(allCommands) do
        if cmd:sub(1, #text):lower() == lower then
            found = found + 1
            local btn = getPooledButton()
            btn.Text = cmd

            -- Hover behavior (only background transparency tweens)
            btn.MouseEnter:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.12, Enum.EasingStyle.Quad), {
                    BackgroundTransparency = 0.05
                }):Play()
            end)
            btn.MouseLeave:Connect(function()
                TweenService:Create(btn, TweenInfo.new(0.12, Enum.EasingStyle.Quad), {
                    BackgroundTransparency = 0.2
                }):Play()
            end)

            -- Click behavior (simple)
            btn.MouseButton1Click:Connect(function()
                commandBar.Text = cmd
                suggestionBox.Visible = false
                clearActiveSuggestions()
            end)
        end
    end

    -- Adjust suggestionBox size based on number of items
    if found > 0 then
        -- compute needed height: item height (26) * count + padding
        local needed = math.clamp(found * 30 + 8, 30, 26 * 6 + 8) -- max visible ~6 items
        suggestionBox.Size = UDim2.new(1, -20, 0, needed)
        suggestionBox.Visible = true
        fadeInSuggestions()
    else
        suggestionBox.Visible = false
    end
end

-- Debounced wrapper so updates only happen after typing pauses briefly
local function scheduleUpdate(text)
    pendingText = text
    task.delay(debounceDelay, function()
        if pendingText == text then
            doUpdateSuggestions(text)
        end
    end)
end

-- Live autocomplete while typing (debounced)
commandBar:GetPropertyChangedSignal("Text"):Connect(function()
    scheduleUpdate(commandBar.Text)
end)

-- Hide on focus lost / Enter (existing behavior)
commandBar.FocusLost:Connect(function(enterPressed)
    suggestionBox.Visible = false
    clearActiveSuggestions()

    if not enterPressed then return end

    local text = commandBar.Text
    commandBar.Text = ""

    if runCommand and runCommand(text) then
        if playClick then pcall(playClick) end
    else
        local s = Instance.new("Sound")
        s.SoundId = "rbxassetid://138087640"
        s.Volume = 1
        s.PlayOnRemove = true
        s.Parent = game:GetService("SoundService")
        s:Destroy()
    end
end)

switchTab("Visual")

--------------------------------------------------
-- FADE BAR (TOP SOLID → BOTTOM TRANSPARENT)
--------------------------------------------------
local fadeBar = Instance.new("Frame")
fadeBar.Size = UDim2.new(1, -20, 0, 22)
fadeBar.Position = UDim2.new(0, 10, 0, 165)
fadeBar.BackgroundColor3 = Color3.fromRGB(60, 60, 80)
fadeBar.BorderSizePixel = 0
fadeBar.Parent = panel

local grad = Instance.new("UIGradient")
grad.Rotation = 90
grad.Transparency = NumberSequence.new({
    NumberSequenceKeypoint.new(0, 0),
    NumberSequenceKeypoint.new(1, 1)
})
grad.Parent = fadeBar

--------------------------------------------------
-- GUI SUSPEND / RESTORE FUNCTIONS
--------------------------------------------------

-- MOVE THIS HERE — AFTER tabScroller, commandBar, suggestionBox, fadeBar EXIST
local heavyUI = {tabScroller, commandBar, fadeBar, suggestionBox}

local storedFrames = {}

local function suspendGUI()
    guiSuspended = true

    for _, ui in ipairs(heavyUI) do
        if ui then ui.Parent = nil end
    end

    for name, frame in pairs(tabFrames) do
        storedFrames[name] = frame.Parent
        frame.Parent = nil
    end
end

local function restoreGUI()
    guiSuspended = false

    for _, ui in ipairs(heavyUI) do
        if ui then ui.Parent = panel end
    end

    for name, frame in pairs(tabFrames) do
        frame.Parent = panel
    end

    if activeTab and tabFrames[activeTab] then
        tabFrames[activeTab].Visible = true
    end
end

--------------------------------------------------
-- DRAGGING (FIXED)
--------------------------------------------------

local dragging = false
local dragStart
local startPos

local function updateDrag(input)
    if isMinimized then return end
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        panel.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end

panel.InputBegan:Connect(function(input)
    if isMinimized then return end
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = panel.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        updateDrag(input)
    end
end)

--------------------------------------------------
-- SECTION HEADER (OPTIMIZED, NO BG / NO STROKE)
--------------------------------------------------
local function createSectionHeader(parent, text)
    local header = Instance.new("Frame")
    header.Size = UDim2.new(1, -20, 0, 40)
    header.BackgroundTransparency = 1 -- fully invisible
    header.BorderSizePixel = 0
    header.Parent = parent

    -- Rounded corners (kept for shape consistency)
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 10)
    corner.Parent = header

    -- Label (unchanged visuals)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -20, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(230, 220, 255)
    label.Font = Enum.Font.GothamBold
    label.TextScaled = true
    label.TextXAlignment = Enum.TextXAlignment.Center
    label.Parent = header

    return header
end

--------------------------------------------------
-- TOGGLE FACTORY (BUBBLE STYLE) - FULLY PATCHED
--------------------------------------------------
local function createToggle(parent, text, modeName, posY)
    if not parent then return end

    -- Ensure the toggle function exists so it NEVER errors
    local funcName = "Toggle" .. modeName
    if _G.Modes[funcName] == nil then
        _G.Modes[funcName] = function()
            print("Toggle function missing for:", funcName)
        end
    end

    -- Outer bubble container
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, -20, 0, 36)
    container.Position = UDim2.new(0, 10, 0, posY)
    container.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
    container.BackgroundTransparency = 0.1
    container.BorderSizePixel = 0
    container.Parent = parent

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 12)
    corner.Parent = container

    -- Gradient background
    local grad = Instance.new("UIGradient")
    grad.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(35, 35, 50)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(55, 55, 80))
    })
    grad.Rotation = 90
    grad.Parent = container

    -- Label (left)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0.6, 0, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(215, 205, 255)
    label.Font = Enum.Font.GothamBold
    label.TextScaled = true
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = container

    -- Toggle bubble (right)
    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0.25, 0, 0.75, 0)
    toggleBtn.Position = UDim2.new(0.72, 0, 0.125, 0)
    toggleBtn.BackgroundColor3 = Modes[modeName]
        and Color3.fromRGB(90, 120, 255)
        or  Color3.fromRGB(70, 70, 90)
    toggleBtn.Text = Modes[modeName] and "ON" or "OFF"
    toggleBtn.TextColor3 = Color3.new(1, 1, 1)
    toggleBtn.Font = Enum.Font.GothamBold
    toggleBtn.TextScaled = true
    toggleBtn.BorderSizePixel = 0
    toggleBtn.Parent = container

    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(1, 0)
    toggleCorner.Parent = toggleBtn

    -- Glow stroke
    local stroke = Instance.new("UIStroke")
    stroke.Color = Color3.fromRGB(180, 180, 255)
    stroke.Thickness = 1.5
    stroke.Transparency = 0.3
    stroke.Parent = toggleBtn

    -- Fade-in transition for toggle container
container.BackgroundTransparency = 1
label.TextTransparency = 1
toggleBtn.TextTransparency = 1
toggleBtn.BackgroundTransparency = 1

task.delay(0.02, function()
    TweenService:Create(container, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
        BackgroundTransparency = 0.1
    }):Play()

    TweenService:Create(label, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
        TextTransparency = 0
    }):Play()

    TweenService:Create(toggleBtn, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
        TextTransparency = 0,
        BackgroundTransparency = 0
    }):Play()
end)


    --------------------------------------------------
    -- TOGGLE LOGIC (FULLY PATCHED)
    --------------------------------------------------
    toggleBtn.MouseButton1Click:Connect(function()
        if playClick then playClick() end

        Modes[modeName] = not Modes[modeName]

        toggleBtn.Text = Modes[modeName] and "ON" or "OFF"

        TweenService:Create(toggleBtn, TweenInfo.new(0.15), {
            BackgroundColor3 = Modes[modeName]
                and Color3.fromRGB(90, 120, 255)
                or  Color3.fromRGB(70, 70, 90)
        }):Play()

        -- ALWAYS call the toggle function safely
        local func = _G.Modes[funcName]
        if func then
            task.spawn(function()
                pcall(func)
            end)
        end
    end)

    --------------------------------------------------
    -- AUTO EXPAND SCROLL AREA (PATCHED)
    --------------------------------------------------
    local bottom = posY + 46
    if bottom > parent.CanvasSize.Y.Offset then
        parent.CanvasSize = UDim2.new(0, 0, 0, bottom)
    end
end


--------------------------------------------------
-- CHAT LOGGER GUI (inside Social tab)
--------------------------------------------------
local chatLogFrame = Instance.new("ScrollingFrame")
chatLogFrame.Size = UDim2.new(1, -20, 1, -20)
chatLogFrame.Position = UDim2.new(0, 10, 0, 10)
chatLogFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)
chatLogFrame.BackgroundTransparency = 0.2
chatLogFrame.BorderSizePixel = 0
chatLogFrame.ScrollBarThickness = 6
chatLogFrame.Visible = false
chatLogFrame.CanvasSize = UDim2.new(0,0,0,0)
chatLogFrame.Parent = tabFrames["Social"]

local chatLayout = Instance.new("UIListLayout")
chatLayout.Parent = chatLogFrame
chatLayout.Padding = UDim.new(0, 4)

--------------------------------------------------
-- AIM GUI MODES
--------------------------------------------------
_G.Modes.AimGUIEnabled = false
_G.Modes.AimTargetPart = "Body" -- "Body" | "Head"
_G.Modes.AimZoomEnabled = false
_G.Modes.AimZoomFOV = 50

------------------------------------------------------------------------------------
-- ADD TOGGLES TO TABS (ADD +40 EVERY SLOT)
------------------------------------------------------------------------------------

local visualTab = tabFrames["Visual"]

createSectionHeader(visualTab, "ESP", 10)

-- Visual
createToggle(tabFrames["Visual"], "ESP", "ESP", 40)
createToggle(tabFrames["Visual"], "Tracer ESP", "TracerESP", 80)
createToggle(tabFrames["Visual"], "Item ESP", "ItemESP", 120)
createToggle(tabFrames["Visual"], "Team Chams", "Chams", 160)
createToggle(tabFrames["Visual"], "FullBright", "FullBright", 200)

-- Lighting
createToggle(tabFrames["Lighting"], "Optimization", "Optimization", 0)
createToggle(tabFrames["Lighting"], "Low Lighting", "LowLighting", 40)
createToggle(tabFrames["Lighting"], "No Shadows", "NoShadows", 80)
createToggle(tabFrames["Lighting"], "No Fog", "NoFog", 120)

-- Player
createToggle(tabFrames["Player"], "Infinite Jump", "InfiniteJump", 0)
createToggle(tabFrames["Player"], "Teleport Tool", "TeleportTool", 40)
createToggle(tabFrames["Player"], "NoClip", "NoClip", 80)
createToggle(tabFrames["Player"], "Freecam", "Freecam", 120)
createToggle(tabFrames["Player"], "X-Ray", "XRay", 160)

-- Utility
createToggle(tabFrames["Utility"], "Rejoin Server", "Rejoin", 0)
createToggle(tabFrames["Utility"], "Reset Character", "ResetChar", 40)
createToggle(tabFrames["Utility"], "Anti-AFK", "AntiAFK", 80)
createToggle(tabFrames["Utility"], "Server Hop", "ServerHop", 120)
createToggle(tabFrames["Utility"], "Forsaken Mode", "Forsaken", 160)

-- Social
createToggle(tabFrames["Social"], "Chat Logger", "ChatLogger", 0)

createToggle(tabFrames["Aimbot"], "Aim GUI", "AimGUI", 0)


--------------------------------------------------
-- ITEM ESP WHITELISTS
--------------------------------------------------
local itemWhitelist = {
    Medkit = true,
    BloxyCola = true,
    FlareGun = true,
    Gun = true,
    KeyCard = true,
    Key = true,
    Flare = true,
}

--------------------------------------------------
-- ITEM ESP STORAGE HAHAHAHAHA-
--------------------------------------------------

local itemESPObjects = {}

local function clearItemESP()
    for obj, gui in pairs(itemESPObjects) do
        if gui then gui:Destroy() end
    end
    itemESPObjects = {}
end

--------------------------------------------------
-- ITEM ESP CREATOR
--------------------------------------------------
local function createItemESP(obj)
    if itemESPObjects[obj] then return end

    local bill = Instance.new("BillboardGui")
    bill.Size = UDim2.new(0, 120, 0, 30)
    bill.AlwaysOnTop = true
    bill.Adornee = obj
    bill.Parent = obj

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = obj.Name
    label.TextColor3 = Color3.fromRGB(230, 220, 255)
    label.Font = Enum.Font.GothamBold
    label.TextScaled = true
    label.Parent = bill

    itemESPObjects[obj] = bill
end

--------------------------------------------------
-- ITEM ESP LOOP (PUT IT RIGHT HERE)
--------------------------------------------------
task.spawn(function()
    while task.wait(0.25) do
        if not Modes.ItemESP then
            clearItemESP()
            continue
        end

        -- Scan Workspace for whitelisted items
        for _, obj in ipairs(workspace:GetDescendants()) do
            if itemWhitelist[obj.Name] then
                if obj:IsA("BasePart") or obj:IsA("Model") then
                    createItemESP(obj)
                end
            end
        end

        -- Cleanup removed items
        for obj, gui in pairs(itemESPObjects) do
            if not obj or not obj.Parent then
                gui:Destroy()
                itemESPObjects[obj] = nil
            end
        end
    end
end)
_G.Modes.ToggleESP = function()
    if Modes.ESP then

        RunService:UnbindFromRenderStep("ESP_Update")
        RunService:UnbindFromRenderStep("ESP_Render")

--------------------------------------------------
-- ESP
--------------------------------------------------
local UPDATE_RATE = 0.1
local MAX_DISTANCE = math.huge
local DetectKiller = true

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ESP_GUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local ESP_Objects = {}
local LockedKillers = {}
local ESP_ENABLED = true

player.CharacterAdded:Wait()

task.spawn(function()
    while ESP_ENABLED do
        task.wait(UPDATE_RATE)

        local myChar = player.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        if not myHRP then continue end

        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= player then

                local char = plr.Character
                local hrp  = char and char:FindFirstChild("HumanoidRootPart")
                local head = char and char:FindFirstChild("Head")
                local hum  = char and char:FindFirstChildOfClass("Humanoid")

                if not (char and hrp and head and hum) then
                    if ESP_Objects[plr] then
                        ESP_Objects[plr].Highlight:Destroy()
                        ESP_Objects[plr].Billboard:Destroy()
                        ESP_Objects[plr] = nil
                    end
                    continue
                end

                if not ESP_Objects[plr] then
                    local highlight = Instance.new("Highlight")
                    highlight.FillTransparency = 1
                    highlight.OutlineTransparency = 0
                    highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                    highlight.Parent = char

                    local billboard = Instance.new("BillboardGui")
                    billboard.Size = UDim2.new(0, 150, 0, 40)
                    billboard.Adornee = head
                    billboard.AlwaysOnTop = true
                    billboard.ExtentsOffset = Vector3.new(0, 2.5, 0)
                    billboard.Parent = screenGui

                    local text = Instance.new("TextLabel")
                    text.Size = UDim2.new(1, 0, 1, 0)
                    text.BackgroundTransparency = 1
                    text.TextColor3 = Color3.fromRGB(255, 255, 255)
                    text.TextStrokeTransparency = 0
                    text.Font = Enum.Font.GothamBold
                    text.TextSize = 14
                    text.Parent = billboard

                    ESP_Objects[plr] = {
                        Highlight = highlight,
                        Billboard = billboard,
                        Text = text,
                        CachedRole = nil,
                        CachedString = ""
                    }
                end

                local obj = ESP_Objects[plr]
                local distance = (hrp.Position - myHRP.Position).Magnitude

                local role = obj.CachedRole
                if not role then
                    if DetectKiller and hum.Health >= 600 then
                        LockedKillers[plr] = true
                        role = "Killer"
                    elseif hum.Health == 115 then
                        role = "Guest1337"
                    else
                        role = "Normal"
                    end
                    obj.CachedRole = role
                end

                local newString
                if role == "Killer" then
                    newString = string.format(
                        "KILLER\n%s | %d/%d | %d studs",
                        plr.Name, hum.Health, hum.MaxHealth, distance
                    )
                elseif role == "Guest1337" then
                    newString = string.format(
                        "GUEST 1337\n%s | %d/%d | %d studs",
                        plr.Name, hum.Health, hum.MaxHealth, distance
                    )
                else
                    newString = string.format(
                        "%s | %d/%d | %d studs",
                        plr.Name, hum.Health, hum.MaxHealth, distance
                    )
                end

                if newString ~= obj.CachedString then
                    obj.CachedString = newString
                    obj.Text.Text = newString
                end

                if role == "Killer" then
                    obj.Text.Font = Enum.Font.GothamBlack
                    obj.Text.TextColor3 = Color3.fromRGB(255, 40, 40)
                    obj.Highlight.OutlineColor = Color3.fromRGB(255, 40, 40)

                elseif role == "Guest1337" then
                    obj.Text.Font = Enum.Font.GothamBlack
                    obj.Text.TextColor3 = Color3.fromRGB(0, 140, 255)
                    obj.Highlight.OutlineColor = Color3.fromRGB(0, 140, 255)

                else
                    obj.Text.Font = Enum.Font.GothamBold
                    obj.Text.TextColor3 = Color3.fromRGB(255, 255, 255)
                    obj.Highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                end

                if hum.Health <= 0 then
                    LockedKillers[plr] = nil
                    obj.CachedRole = nil
                end
            end
        end
    end
end)

RunService:BindToRenderStep("ESP_Render", 300, function()
    if not ESP_ENABLED then return end

    local myChar = player.Character
    local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
    if not myHRP then return end

    for plr, obj in pairs(ESP_Objects) do
        local char = plr.Character
        local hrp  = char and char:FindFirstChild("HumanoidRootPart")
        if not hrp then continue end

        local distance = (hrp.Position - myHRP.Position).Magnitude
        local enabled = distance <= MAX_DISTANCE

        obj.Highlight.Enabled = enabled
        obj.Billboard.Enabled = enabled
    end
end)

--------------------------------------------------
-- AIM GUI TOGGLE FUNCTION (FIXED)
--------------------------------------------------
local Players = game:GetService("Players")
local lp = Players.LocalPlayer

-- defaults (safe)
_G.Modes.AimGUIEnabled   = _G.Modes.AimGUIEnabled   or false
_G.Modes.AimTargetPart  = _G.Modes.AimTargetPart  or "Body"
_G.Modes.AimZoomEnabled = _G.Modes.AimZoomEnabled or false

local AimGui -- reference holder

function _G.Modes.ToggleAimGUI(state)
    -- state comes from createToggle
    _G.Modes.AimGUIEnabled = state

    -- ================== ENABLE ==================
    if state then
        -- prevent double-create
        if AimGui and AimGui.Parent then
            return
        end

        AimGui = Instance.new("ScreenGui")
        AimGui.Name = "Aim GUI"
        AimGui.ResetOnSpawn = false
        AimGui.Parent = lp:WaitForChild("PlayerGui")

        local frame = Instance.new("Frame")
        frame.Size = UDim2.fromOffset(220, 160)
        frame.Position = UDim2.new(0, 40, 0.5, -80)
        frame.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
        frame.BorderSizePixel = 0
        frame.Parent = AimGui

        Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 12)

        -- TITLE
        local title = Instance.new("TextLabel")
        title.Size = UDim2.new(1, -20, 0, 30)
        title.Position = UDim2.fromOffset(10, 10)
        title.BackgroundTransparency = 1
        title.Text = "Aim Settings"
        title.TextColor3 = Color3.fromRGB(255, 255, 255)
        title.Font = Enum.Font.GothamBold
        title.TextSize = 16
        title.TextXAlignment = Enum.TextXAlignment.Left
        title.Parent = frame

        -- AIM PART TOGGLE
        local partBtn = Instance.new("TextButton")
        partBtn.Size = UDim2.new(1, -20, 0, 36)
        partBtn.Position = UDim2.fromOffset(10, 50)
        partBtn.Font = Enum.Font.Gotham
        partBtn.TextSize = 14
        partBtn.TextColor3 = Color3.new(1, 1, 1)
        partBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
        partBtn.BorderSizePixel = 0
        partBtn.AutoButtonColor = false
        partBtn.Parent = frame

        Instance.new("UICorner", partBtn).CornerRadius = UDim.new(0, 8)

        local function updatePartText()
            partBtn.Text = "Aim Part: " .. _G.Modes.AimTargetPart
        end
        updatePartText()

        partBtn.MouseButton1Click:Connect(function()
            _G.Modes.AimTargetPart =
                (_G.Modes.AimTargetPart == "Body") and "Head" or "Body"
            updatePartText()
        end)

        -- ZOOM TOGGLE
        local zoomBtn = Instance.new("TextButton")
        zoomBtn.Size = UDim2.new(1, -20, 0, 36)
        zoomBtn.Position = UDim2.fromOffset(10, 96)
        zoomBtn.Font = Enum.Font.Gotham
        zoomBtn.TextSize = 14
        zoomBtn.TextColor3 = Color3.new(1, 1, 1)
        zoomBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
        zoomBtn.BorderSizePixel = 0
        zoomBtn.AutoButtonColor = false
        zoomBtn.Parent = frame

        Instance.new("UICorner", zoomBtn).CornerRadius = UDim.new(0, 8)

        local function updateZoomText()
            zoomBtn.Text = _G.Modes.AimZoomEnabled and "Zoom: ON" or "Zoom: OFF"
        end
        updateZoomText()

        zoomBtn.MouseButton1Click:Connect(function()
            _G.Modes.AimZoomEnabled = not _G.Modes.AimZoomEnabled
            updateZoomText()
        end)

    -- ================== DISABLE ==================
    else
        if AimGui then
            AimGui:Destroy()
            AimGui = nil
        end
    end
end


--------------------------------------------------
-- CHAT LOGGER UTILITIES
--------------------------------------------------

local function getNameColor(name)
    local hash = 0
    for i = 1, #name do
        hash = (hash + string.byte(name, i) * i) % 255
    end
    return Color3.fromHSV((hash / 255), 0.7, 1)
end

--------------------------------------------------
-- CHAT LOGGER FUNCTION (FIXED + UNIVERSAL)
--------------------------------------------------
local function addChatMessage(speaker, message, isPrivate, target)
    if not Modes.ChatLogger then return end
    if not chatLogFrame or not chatLayout then return end

    -- Convert speaker to Player if needed
    if typeof(speaker) == "string" then
        speaker = Players:FindFirstChild(speaker)
    end
    if not speaker or not speaker:IsA("Player") then return end

    -- Sanitize message for RichText
    message = tostring(message)
        :gsub("<", "&lt;")
        :gsub(">", "&gt;")

    -- Distance calculation
    local myHRP = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    local theirHRP = speaker.Character and speaker.Character:FindFirstChild("HumanoidRootPart")

    local distance = 0
    if myHRP and theirHRP then
        distance = math.floor((theirHRP.Position - myHRP.Position).Magnitude)
    end

    -- Timestamp
    local timestamp = os.date("%H:%M:%S")

    -- Create entry
    local entry = Instance.new("TextLabel")
    entry.Size = UDim2.new(1, -10, 0, 22)
    entry.BackgroundTransparency = 1
    entry.Font = Enum.Font.Gotham
    entry.TextScaled = false
    entry.TextSize = 14
    entry.TextXAlignment = Enum.TextXAlignment.Left
    entry.TextColor3 = Color3.fromRGB(255,255,255)
    entry.RichText = true

    -- Username color
    local nameColor = getNameColor(speaker.Name)
    local nameTag = string.format(
        "<font color='#%02X%02X%02X'>%s</font>",
        nameColor.R * 255,
        nameColor.G * 255,
        nameColor.B * 255,
        speaker.Name
    )

    -- Private tag
    local privateTag = ""
    if isPrivate then
        privateTag = string.format(" <font color='#FF5555'>(PRIVATE → %s)</font>", target or "Unknown")
    end

    -- Final text
    entry.Text = string.format(
        "[%s] (%d studs) %s%s: %s",
        timestamp, distance, nameTag, privateTag, message
    )

    entry.Parent = chatLogFrame

    -- Auto-scroll
    task.wait()
    chatLogFrame.CanvasSize = UDim2.new(0,0,0,chatLayout.AbsoluteContentSize.Y + 10)
    chatLogFrame.CanvasPosition = Vector2.new(0, chatLayout.AbsoluteContentSize.Y)
end

--------------------------------------------------
-- CHAT LOGGER LISTENERS (UNIVERSAL)
--------------------------------------------------

-- Legacy Chat
for _, plr in ipairs(Players:GetPlayers()) do
    plr.Chatted:Connect(function(msg)
        addChatMessage(plr, msg, false)
    end)
end

Players.PlayerAdded:Connect(function(plr)
    plr.Chatted:Connect(function(msg)
        addChatMessage(plr, msg, false)
    end)
end)

-- DefaultChatSystemChatEvents (Classic Filtering)
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local defaultChatEvents = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents")

if defaultChatEvents and defaultChatEvents.OnMessageDoneFiltering then
    defaultChatEvents.OnMessageDoneFiltering.OnClientEvent:Connect(function(data)
        local speaker = Players:FindFirstChild(data.FromSpeaker)
        if not speaker then return end

        local msg = data.Message
        local isPrivate = false
        local target = nil

        if data.OriginalChannel == "Whisper" then
            isPrivate = true
            target = data.ToSpeaker
        end

        addChatMessage(speaker, msg, isPrivate, target)
    end)
end

-- NEW CHAT SYSTEM (TextChatService)
local TextChatService = game:GetService("TextChatService")

if TextChatService.ChatInputBarConfiguration then
    TextChatService.MessageReceived:Connect(function(msg)
        local speaker = Players:FindFirstChild(msg.TextSource.Name)
        if not speaker then return end

        local isPrivate = msg.TextChannel and msg.TextChannel.Name == "RBXWhisper"
        local target = nil

        if isPrivate then
            target = msg.TargetTextSource and msg.TargetTextSource.Name
        end

        addChatMessage(speaker, msg.Text, isPrivate, target)
    end)
end

--------------------------------------------------
-- X-RAY MODE (Optimized)
--------------------------------------------------

local XRayEnabled = false
local XRayTransparency = 0.7  -- how see-through the world becomes

local storedTransparency = {} -- stores original transparency

_G.Modes.ToggleXRay = function()
    XRayEnabled = not XRayEnabled

    if XRayEnabled then
        -- APPLY X-RAY
        for _, obj in ipairs(Workspace:GetDescendants()) do
            if obj:IsA("BasePart") and obj.Transparency < XRayTransparency then
                storedTransparency[obj] = obj.Transparency
                obj.Transparency = XRayTransparency
            end
        end

        -- LIVE UPDATE (for new parts)
        RunService:BindToRenderStep("XRay_Update", 300, function()
            for _, obj in ipairs(Workspace:GetDescendants()) do
                if obj:IsA("BasePart") then
                    if XRayEnabled then
                        if not storedTransparency[obj] then
                            storedTransparency[obj] = obj.Transparency
                        end
                        obj.Transparency = math.max(obj.Transparency, XRayTransparency)
                    end
                end
            end
        end)

    else
        -- RESTORE ORIGINAL TRANSPARENCY
        RunService:UnbindFromRenderStep("XRay_Update")

        for obj, original in pairs(storedTransparency) do
            if obj and obj.Parent then
                obj.Transparency = original
            end
        end

        storedTransparency = {}
    end
end

--------------------------------------------------
-- FREECAM (FAST + YGHJ + Auto UI)
--------------------------------------------------

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local cam = workspace.CurrentCamera

local FreecamEnabled = false
local moveDir = Vector3.zero
local conns = {}
local ui

local baseSpeed = 3
local fastSpeed = 12

--------------------------------------------------
-- CREATE UI WHEN FREECAM ENABLES
--------------------------------------------------
local function createUI()
    ui = Instance.new("ScreenGui")
    ui.Name = "FreecamUI"
    ui.ResetOnSpawn = false
    ui.Parent = player:WaitForChild("PlayerGui")

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 40)
    frame.Position = UDim2.new(0.5, -100, 0, 20)
    frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    frame.BackgroundTransparency = 0.2
    frame.BorderSizePixel = 0
    frame.Parent = ui

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = frame

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = "FREECAM ACTIVE (Y G H J + U/N)"
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 14
    label.Parent = frame
end

--------------------------------------------------
-- DESTROY UI WHEN FREECAM DISABLES
--------------------------------------------------
local function destroyUI()
    if ui then
        ui:Destroy()
        ui = nil
    end
end

--------------------------------------------------
-- START FREECAM
--------------------------------------------------
local function startFreecam()
    FreecamEnabled = true
    cam.CameraType = Enum.CameraType.Scriptable

    createUI()

    conns.inputBegin = UserInputService.InputBegan:Connect(function(input, gpe)
        if gpe then return end

        if input.KeyCode == Enum.KeyCode.Y then moveDir += Vector3.new(0,0,-1) end
        if input.KeyCode == Enum.KeyCode.H then moveDir += Vector3.new(0,0,1) end
        if input.KeyCode == Enum.KeyCode.G then moveDir += Vector3.new(-1,0,0) end
        if input.KeyCode == Enum.KeyCode.J then moveDir += Vector3.new(1,0,0) end
        if input.KeyCode == Enum.KeyCode.U then moveDir += Vector3.new(0,1,0) end
        if input.KeyCode == Enum.KeyCode.N then moveDir += Vector3.new(0,-1,0) end
    end)

    conns.inputEnd = UserInputService.InputEnded:Connect(function(input)
        if input.KeyCode == Enum.KeyCode.Y then moveDir -= Vector3.new(0,0,-1) end
        if input.KeyCode == Enum.KeyCode.H then moveDir -= Vector3.new(0,0,1) end
        if input.KeyCode == Enum.KeyCode.G then moveDir -= Vector3.new(-1,0,0) end
        if input.KeyCode == Enum.KeyCode.J then moveDir -= Vector3.new(1,0,0) end
        if input.KeyCode == Enum.KeyCode.U then moveDir -= Vector3.new(0,1,0) end
        if input.KeyCode == Enum.KeyCode.N then moveDir -= Vector3.new(0,-1,0) end
    end)

    conns.render = RunService.RenderStepped:Connect(function(dt)
        local speed = UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) and fastSpeed or baseSpeed
        local move = cam.CFrame:VectorToWorldSpace(moveDir) * speed
        cam.CFrame = cam.CFrame + move * dt
    end)
end

--------------------------------------------------
-- STOP FREECAM
--------------------------------------------------
local function stopFreecam()
    FreecamEnabled = false
    cam.CameraType = Enum.CameraType.Custom

    destroyUI()

    for _, c in pairs(conns) do
        if typeof(c) == "RBXScriptConnection" then
            c:Disconnect()
        end
    end

    conns = {}
    moveDir = Vector3.zero
end

--------------------------------------------------
-- PUBLIC TOGGLE FOR YOUR GUI
--------------------------------------------------
_G.Modes = _G.Modes or {}
_G.Modes.ToggleFreecam = function()
    if FreecamEnabled then
        stopFreecam()
    else
        startFreecam()
    end
end

--------------------------------------------------
-- SERVER HOP (Auto-detect current game)
--------------------------------------------------

_G.Modes.ToggleServerHop = function()
    if not Modes.ServerHop then return end

    local placeId = game.PlaceId
    local cursor = ""
    local servers = {}

    local function getServers()
        local url = "https://games.roblox.com/v1/games/"..placeId.."/servers/Public?sortOrder=Asc&limit=100"..cursor
        local response = game:HttpGet(url)
        return game:GetService("HttpService"):JSONDecode(response)
    end

    -- Collect non-full servers
    while true do
        local data = getServers()

        for _, server in ipairs(data.data) do
            if server.playing < server.maxPlayers and server.id ~= game.JobId then
                table.insert(servers, server.id)
            end
        end

        if data.nextPageCursor then
            cursor = "&cursor="..data.nextPageCursor
        else
            break
        end
    end

    -- Hop to a random non-full server
    if #servers > 0 then
        local chosen = servers[math.random(1, #servers)]
        TeleportService:TeleportToPlaceInstance(placeId, chosen, player)
    else
        warn("No available non-full servers found.")
    end
end

--------------------------------------------------
-- TEAM COLORED CHAMS
--------------------------------------------------
local ChamsObjects = {}

_G.Modes.ToggleChams = function()
    if Modes.Chams then
        RunService:UnbindFromRenderStep("Chams_Update")
        RunService:BindToRenderStep("Chams_Update", 201, function()
            for _, plr in pairs(Players:GetPlayers()) do
                if plr ~= player then
                    local char = plr.Character
                    local hum  = char and char:FindFirstChildOfClass("Humanoid")

                    if char and hum then
                        if not ChamsObjects[plr] then
                            local highlight = Instance.new("Highlight")
                            highlight.FillTransparency = 0.5
                            highlight.OutlineTransparency = 0
                            highlight.Parent = char
                            ChamsObjects[plr] = highlight
                        end

                        local highlight = ChamsObjects[plr]
                        if highlight then
                            if plr.Team and plr.Team.TeamColor then
                                local c = plr.Team.TeamColor.Color
                                highlight.FillColor = c
                                highlight.OutlineColor = c
                            else
                                highlight.FillColor = Color3.fromRGB(255,255,255)
                                highlight.OutlineColor = Color3.fromRGB(255,255,255)
                            end
                        end
                    else
                        if ChamsObjects[plr] then
                            ChamsObjects[plr]:Destroy()
                            ChamsObjects[plr] = nil
                        end
                    end
                end
            end
        end)
    else
        RunService:UnbindFromRenderStep("Chams_Update")
        for _, obj in pairs(ChamsObjects) do
            obj:Destroy()
        end
        ChamsObjects = {}
    end
end

--------------------------------------------------
-- OPTIMIZATION MODE
--------------------------------------------------
_G.Modes.ToggleOptimization = function()
    if Modes.Optimization then
        for _, obj in pairs(Workspace:GetDescendants()) do
            if obj:IsA("BasePart") then
                obj.CastShadow = false
                obj.Material = Enum.Material.Plastic
            end
        end
    end
end

--------------------------------------------------
-- NO SHADOWS MODE
--------------------------------------------------
_G.Modes.ToggleNoShadows = function()
    if Modes.NoShadows then
        for _, obj in pairs(Workspace:GetDescendants()) do
            if obj:IsA("BasePart") then
                obj.CastShadow = false
            end
        end
    else
        for _, obj in pairs(Workspace:GetDescendants()) do
            if obj:IsA("BasePart") then
                obj.CastShadow = true
            end
        end
    end
end

--------------------------------------------------
-- LOW LIGHTING MODE
--------------------------------------------------
local SavedLighting = nil

_G.Modes.ToggleLowLighting = function()
    if Modes.LowLighting then
        if not SavedLighting then
            SavedLighting = {
                Brightness = Lighting.Brightness,
                ClockTime = Lighting.ClockTime,
                Ambient = Lighting.Ambient,
                OutdoorAmbient = Lighting.OutdoorAmbient,
                GlobalShadows = Lighting.GlobalShadows,
                ShadowSoftness = Lighting.ShadowSoftness,
                FogEnd = Lighting.FogEnd,
                FogStart = Lighting.FogStart,
                EnvironmentDiffuseScale = Lighting.EnvironmentDiffuseScale,
                EnvironmentSpecularScale = Lighting.EnvironmentSpecularScale,
            }
        end

        Lighting.Brightness = 1
        Lighting.ClockTime = 14
        Lighting.Ambient = Color3.fromRGB(128,128,128)
        Lighting.OutdoorAmbient = Color3.fromRGB(128,128,128)
        Lighting.GlobalShadows = false
        Lighting.ShadowSoftness = 0
        Lighting.FogStart = 0
        Lighting.FogEnd = 100000
        Lighting.EnvironmentDiffuseScale = 0
        Lighting.EnvironmentSpecularScale = 0
    else
        if SavedLighting then
            for prop, val in pairs(SavedLighting) do
                Lighting[prop] = val
            end
        end
        SavedLighting = nil
    end
end

--------------------------------------------------
-- TRACER ESP
--------------------------------------------------
_G.Modes.ToggleTracerESP = function()
    if Modes.TracerESP then
        -- ENABLE TRACERS
        local RunService = game:GetService("RunService")
        local Players = game:GetService("Players")
        local LocalPlayer = Players.LocalPlayer
        local Camera = workspace.CurrentCamera

        -- Create folder for tracers
        if not workspace:FindFirstChild("Cr3ative_Tracers") then
            local folder = Instance.new("Folder")
            folder.Name = "Cr3ative_Tracers"
            folder.Parent = workspace
        end

        -- Connection
        _G.TracerConnection = RunService.RenderStepped:Connect(function()
            local folder = workspace:FindFirstChild("Cr3ative_Tracers")
            if not folder then return end

            -- Clear old tracers
            folder:ClearAllChildren()

            for _, plr in ipairs(Players:GetPlayers()) do
                if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                    local hrp = plr.Character.HumanoidRootPart
                    local screenPos, onScreen = Camera:WorldToViewportPoint(hrp.Position)

                    if onScreen then
                        local tracer = Drawing.new("Line")
                        tracer.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)
                        tracer.To = Vector2.new(screenPos.X, screenPos.Y)
                        tracer.Color = Color3.fromRGB(200, 160, 255)
                        tracer.Thickness = 2
                        tracer.Transparency = 1
                        tracer.Visible = true

                        -- Auto-remove each frame
                        task.delay(0.016, function()
                            tracer:Remove()
                        end)
                    end
                end
            end
        end)

    else
        -- DISABLE TRACERS
        if _G.TracerConnection then
            _G.TracerConnection:Disconnect()
            _G.TracerConnection = nil
        end

        if workspace:FindFirstChild("Cr3ative_Tracers") then
            workspace.Cr3ative_Tracers:Destroy()
        end
    end
end


--------------------------------------------------
-- INFINITE JUMP
--------------------------------------------------
local InfiniteJumpEnabled = false

_G.Modes.ToggleInfiniteJump = function()
    InfiniteJumpEnabled = not InfiniteJumpEnabled
end

UserInputService.JumpRequest:Connect(function()
    if InfiniteJumpEnabled and player.Character then
        local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
        if humanoid and humanoid:GetState() ~= Enum.HumanoidStateType.Dead then
            humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end
end)

--------------------------------------------------
-- TELEPORT TOOL
--------------------------------------------------
_G.Modes.ToggleTeleportTool = function()
    local backpack = player:FindFirstChildOfClass("Backpack")
    if not backpack then return end

    if not Modes.TeleportTool then
        local old = backpack:FindFirstChild("TeleportTool")
        if old then old:Destroy() end
        return
    end

    local old = backpack:FindFirstChild("TeleportTool")
    if old then old:Destroy() end

    local tool = Instance.new("Tool")
    tool.Name = "TeleportTool"
    tool.RequiresHandle = false
    tool.CanBeDropped = false
    tool.Parent = backpack

    local mouse = player:GetMouse()

    tool.Activated:Connect(function()
        if not player.Character then return end
        local hrp = player.Character:FindFirstChild("HumanoidRootPart")
        if not hrp then return end
        local hit = mouse.Hit
        if not hit then return end
        local targetPos = hit.Position + Vector3.new(0,3,0)
        hrp.CFrame = CFrame.new(targetPos)
    end)
end

--------------------------------------------------
-- NO FOG MODE
--------------------------------------------------

local SavedFog = nil

_G.Modes.ToggleNoFog = function()
    if Modes.NoFog then
        -- Save original fog settings
        if not SavedFog then
            SavedFog = {
                FogStart = Lighting.FogStart,
                FogEnd = Lighting.FogEnd
            }
        end

        -- Disable fog completely
        Lighting.FogStart = 0
        Lighting.FogEnd = 1000000

    else
        -- Restore original fog
        if SavedFog then
            Lighting.FogStart = SavedFog.FogStart
            Lighting.FogEnd = SavedFog.FogEnd
        end
        SavedFog = nil
    end
end

--------------------------------------------------
-- FULLBRIGHT MODE
--------------------------------------------------

local SavedBrightness = nil

_G.Modes.ToggleFullBright = function()
    if Modes.FullBright then
        -- Save original lighting
        if not SavedBrightness then
            SavedBrightness = {
                Brightness = Lighting.Brightness,
                Ambient = Lighting.Ambient,
                OutdoorAmbient = Lighting.OutdoorAmbient
            }
        end

        -- Apply fullbright
        Lighting.Brightness = 2
        Lighting.Ambient = Color3.new(1,1,1)
        Lighting.OutdoorAmbient = Color3.new(1,1,1)

    else
        -- Restore original lighting
        if SavedBrightness then
            Lighting.Brightness = SavedBrightness.Brightness
            Lighting.Ambient = SavedBrightness.Ambient
            Lighting.OutdoorAmbient = SavedBrightness.OutdoorAmbient
        end

        SavedBrightness = nil
    end
end

--------------------------------------------------
-- NOCLIP
--------------------------------------------------
local NoClipActive = false

local function setNoClip(character, state)
    if not character then return end
    for _, part in ipairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.CanCollide = not state
        end
    end
end

_G.Modes.ToggleNoClip = function()
    NoClipActive = not NoClipActive

    local character = player.Character

    if NoClipActive then
        -- Apply immediately
        setNoClip(character, true)

        -- Keep enforcing every frame
        RunService:BindToRenderStep("NoClip_Update", 100, function()
            if not NoClipActive then
                RunService:UnbindFromRenderStep("NoClip_Update")
                return
            end

            local char = player.Character
            setNoClip(char, true)
        end)
    else
        -- Turn off and restore collisions
        RunService:UnbindFromRenderStep("NoClip_Update")
        setNoClip(character, false)
    end
end

-- Re-apply noclip on respawn if still active
player.CharacterAdded:Connect(function(char)
    if NoClipActive then
        task.wait(0.1) -- let Roblox finish building the character
        setNoClip(char, true)
    end
end)

    
--------------------------------------------------
-- FORSAKEN MODE (FULL PACKAGE — TELEPORT INTRO, LOCK-IN, LMS)
--------------------------------------------------
local camera = Workspace.CurrentCamera

local DIST_RADIUS           = 400
local CHECK_INTERVAL        = 0.25

local LMS_SOUND_ID          = 119591769079104
local LOCKIN_SOUND_ID       = 128166619127132
local DEATH_SOUND_ID        = 6932519682
local HP50_SOUND_ID         = 121848088329098
local HP20_SOUND_ID         = 6999993863

local TELEPORT_MIN_DIST     = 200
local TELEPORT_DEBOUNCE     = 5

local INTRO_SOUND_ID        = 9072304992
local INTRO_DURATION        = 6

local MOTIVATION_TEXT_AGGRESSIVE = {
    "THEY STAND WITH ME.",
    "NO ESCAPE.",
    "EVERY ECHO REMEMBERS YOU.",
    "ONE OF US WILL MAKE IT OUT ALIVE."
}

local INTRO_LINES = {
    "HUNT.",
    "BREAK.",
    "END THEM.",
    "FINISH IT."
}

-- connections + state
local deathConnections      = {}
local healthConnections     = {}
local lastHealthState       = {}

local LMS_CheckConnection   = nil
local LMS_State             = "none"
local LMS_Sound             = nil

local savedOptimization     = nil
local lastCheckAccum        = 0

local teleportWatcherConn   = nil
local prevHRPPos            = nil
local lastTeleportTime      = 0

local introGui              = nil
local introText             = nil
local flashFrame            = nil
local introSoundInstance    = nil
local introActive           = false
local introPlayedThisRound  = false

local playerAddedConn
local charAddedConns        = {}
local myDeathConn           = nil

-- forward declarations
local destroyIntro
local playForsakenIntro
local setState

--------------------------------------------------
-- HELPERS
--------------------------------------------------
local function safeDestroy(obj)
    if obj and obj.Destroy then
        pcall(function() obj:Destroy() end)
    end
end

local function playOneShot(id, vol)
    local s = Instance.new("Sound")
    s.SoundId = "rbxassetid://" .. tostring(id)
    s.Volume = vol or 3
    s.PlayOnRemove = true
    s.Parent = SoundService
    s:Destroy()
end

local function startLoopSound(id, vol)
    if LMS_Sound then
        pcall(function()
            LMS_Sound:Stop()
            LMS_Sound:Destroy()
        end)
        LMS_Sound = nil
    end
    local s = Instance.new("Sound")
    s.SoundId = "rbxassetid://" .. tostring(id)
    s.Volume = vol or 3
    s.Looped = true
    s.Parent = SoundService
    s:Play()
    LMS_Sound = s
end

local function stopLoopSound()
    if LMS_Sound then
        pcall(function()
            LMS_Sound:Stop()
            LMS_Sound:Destroy()
        end)
        LMS_Sound = nil
    end
end

local function muteGameMusic()
    for _, s in ipairs(SoundService:GetDescendants()) do
        if s:IsA("Sound") and s.Looped and s ~= LMS_Sound then
            pcall(function() s.Volume = 0 end)
        end
    end
end

local function restoreGameMusic()
    for _, s in ipairs(SoundService:GetDescendants()) do
        if s:IsA("Sound") and s.Looped and s ~= LMS_Sound then
            pcall(function() s.Volume = 1 end)
        end
    end
end

--------------------------------------------------
-- AUDIO HOOKS ON OTHER PLAYERS
--------------------------------------------------
local function attachToCharacterForPlayer(plr, char)
    if not plr or not char then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hum or not hrp then return end

    if deathConnections[plr] then
        pcall(function() deathConnections[plr]:Disconnect() end)
        deathConnections[plr] = nil
    end
    if healthConnections[plr] then
        pcall(function() healthConnections[plr]:Disconnect() end)
        healthConnections[plr] = nil
    end

    deathConnections[plr] = hum.Died:Connect(function()
        local myChar = player.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        if myHRP then
            local dist = (myHRP.Position - hrp.Position).Magnitude
            if dist <= DIST_RADIUS then
                playOneShot(DEATH_SOUND_ID)
            end
        end
    end)

    lastHealthState[plr] = "normal"
    healthConnections[plr] = hum.HealthChanged:Connect(function()
        local hp = hum.Health
        local myChar = player.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        if not myHRP then return end

        local dist = (myHRP.Position - hrp.Position).Magnitude
        if dist > DIST_RADIUS then return end

        if hp <= 50 and hp > 20 and lastHealthState[plr] ~= "50" then
            lastHealthState[plr] = "50"
            playOneShot(HP50_SOUND_ID)
        end
        if hp <= 20 and lastHealthState[plr] ~= "20" then
            lastHealthState[plr] = "20"
            playOneShot(HP20_SOUND_ID)
        end
    end)
end

local function startForsakenAudio()
    for _, c in pairs(deathConnections) do pcall(function() c:Disconnect() end) end
    for _, c in pairs(healthConnections) do pcall(function() c:Disconnect() end) end
    deathConnections = {}
    healthConnections = {}
    lastHealthState = {}

    for plr, conn in pairs(charAddedConns) do
        pcall(function() conn:Disconnect() end)
        charAddedConns[plr] = nil
    end
    if playerAddedConn then
        pcall(function() playerAddedConn:Disconnect() end)
        playerAddedConn = nil
    end

    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= player then
            if plr.Character then
                attachToCharacterForPlayer(plr, plr.Character)
            end
            charAddedConns[plr] = plr.CharacterAdded:Connect(function(char)
                attachToCharacterForPlayer(plr, char)
            end)
        end
    end

    playerAddedConn = Players.PlayerAdded:Connect(function(plr)
        if plr ~= player then
            charAddedConns[plr] = plr.CharacterAdded:Connect(function(char)
                attachToCharacterForPlayer(plr, char)
            end)
        end
    end)
end

local function stopForsakenAudio()
    for _, c in pairs(deathConnections) do pcall(function() c:Disconnect() end) end
    for _, c in pairs(healthConnections) do pcall(function() c:Disconnect() end) end
    deathConnections = {}
    healthConnections = {}
    lastHealthState = {}

    for plr, conn in pairs(charAddedConns) do
        pcall(function() conn:Disconnect() end)
        charAddedConns[plr] = nil
    end
    if playerAddedConn then
        pcall(function() playerAddedConn:Disconnect() end)
        playerAddedConn = nil
    end
end

--------------------------------------------------
-- INTRO GUI
--------------------------------------------------
destroyIntro = function()
    if introSoundInstance then
        pcall(function()
            introSoundInstance:Stop()
            introSoundInstance:Destroy()
        end)
        introSoundInstance = nil
    end

    if introGui then
        pcall(function() introGui:Destroy() end)
        introGui = nil
        introText = nil
        flashFrame = nil
    end

    introActive = false
end

playForsakenIntro = function()
    if introActive then return end
    introActive = true

    introGui = Instance.new("ScreenGui")
    introGui.IgnoreGuiInset = true
    introGui.ResetOnSpawn = false
    introGui.Parent = parentGui

    flashFrame = Instance.new("Frame")
    flashFrame.Size = UDim2.fromScale(1,1)
    flashFrame.BackgroundColor3 = Color3.fromRGB(255,0,0)
    flashFrame.BackgroundTransparency = 1
    flashFrame.ZIndex = 50
    flashFrame.Parent = introGui

    introText = Instance.new("TextLabel")
    introText.Size = UDim2.fromScale(1,0.18)
    introText.Position = UDim2.fromScale(0,0.41)
    introText.BackgroundTransparency = 1
    introText.TextColor3 = Color3.fromRGB(255,40,40)
    introText.Font = Enum.Font.GothamBlack
    introText.TextScaled = true
    introText.TextStrokeTransparency = 0
    introText.ZIndex = 51
    introText.Text = ""
    introText.Parent = introGui

    TweenService:Create(
        flashFrame,
        TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
        {BackgroundTransparency = 0.35}
    ):Play()

    introSoundInstance = Instance.new("Sound")
    introSoundInstance.SoundId = "rbxassetid://" .. tostring(INTRO_SOUND_ID)
    introSoundInstance.Volume = 4
    introSoundInstance.Parent = SoundService
    introSoundInstance:Play()

    task.spawn(function()
        for _, line in ipairs(INTRO_LINES) do
            if not introText then break end
            introText.Text = ""
            for i = 1, #line do
                if not introText then break end
                introText.Text = string.sub(line, 1, i)
                task.wait(0.035)
            end
            task.wait(0.35)
        end
    end)

    task.delay(INTRO_DURATION, function()
        if not introText then
            destroyIntro()
            return
        end

        local txt = introText.Text
        for i = #txt, 0, -1 do
            if not introText then break end
            introText.Text = string.sub(txt, 1, i)
            task.wait(0.02)
        end

        TweenService:Create(
            flashFrame,
            TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
            {BackgroundTransparency = 1}
        ):Play()

        task.delay(0.45, function()
            destroyIntro()
        end)
    end)
end

--------------------------------------------------
-- STATE MACHINE (NONE / LOCKIN / LMS)
--------------------------------------------------
setState = function(newState)
    if newState == LMS_State then return end

    -- leaving LMS
    if LMS_State == "lms" then
        if savedOptimization ~= nil then
            Modes.Optimization = savedOptimization
            if _G.Modes.ToggleOptimization then
                pcall(_G.Modes.ToggleOptimization)
            end
            savedOptimization = nil
        end
        restoreGameMusic()
    end

    -- leaving LOCKIN
    if LMS_State == "lockin" then
        stopLoopSound()
    end

    LMS_State = newState

    if newState == "none" then
        stopLoopSound()
        return
    end

    if newState == "lockin" then
        stopLoopSound()
        startLoopSound(LOCKIN_SOUND_ID, 3)
        return
    end

    if newState == "lms" then
        stopLoopSound()
        muteGameMusic()
        startLoopSound(LMS_SOUND_ID, 3)

        if savedOptimization == nil then
            savedOptimization = Modes.Optimization
        end
        Modes.Optimization = true
        if _G.Modes.ToggleOptimization then
            pcall(_G.Modes.ToggleOptimization)
        end

        if introActive then
            destroyIntro()
        end

        -- LMS motivational text
        task.spawn(function()
            local g = Instance.new("ScreenGui")
            g.IgnoreGuiInset = true
            g.ResetOnSpawn = false
            g.Parent = parentGui

            local tlabel = Instance.new("TextLabel")
            tlabel.Size = UDim2.fromScale(0.8,0.12)
            tlabel.Position = UDim2.fromScale(0.1,0.82)
            tlabel.BackgroundTransparency = 1
            tlabel.TextColor3 = Color3.fromRGB(255,30,30)
            tlabel.Font = Enum.Font.GothamBlack
            tlabel.TextScaled = true
            tlabel.TextStrokeTransparency = 0
            tlabel.Parent = g

            for _, line in ipairs(MOTIVATION_TEXT_AGGRESSIVE) do
                if not tlabel then break end
                tlabel.Text = ""
                for i = 1, #line do
                    if not tlabel then break end
                    tlabel.Text = string.sub(line,1,i)
                    task.wait(0.03)
                end
                task.wait(0.25)
            end

            task.delay(2, function()
                if not tlabel then return end
                local txt = tlabel.Text or ""
                for i = #txt, 0, -1 do
                    if not tlabel then break end
                    tlabel.Text = string.sub(txt,1,i)
                    task.wait(0.02)
                end
                safeDestroy(g)
            end)
        end)
    end
end

--------------------------------------------------
-- LMS CHECK LOOP
--------------------------------------------------
local function startLMSCheck()
    if LMS_CheckConnection then
        pcall(function() LMS_CheckConnection:Disconnect() end)
    end
    LMS_CheckConnection = nil

    LMS_State = "none"
    stopLoopSound()
    lastCheckAccum = 0

    if myDeathConn then
        pcall(function() myDeathConn:Disconnect() end)
        myDeathConn = nil
    end

    if player.Character then
        local hum = player.Character:FindFirstChildOfClass("Humanoid")
        if hum then
            myDeathConn = hum.Died:Connect(function()
                setState("none")
                introPlayedThisRound = false

                stopForsakenAudio()
                Modes.ESP = false
                if _G.Modes.ToggleESP then
                    pcall(_G.Modes.ToggleESP)
                end
            end)
        end
    end

    LMS_CheckConnection = RunService.Heartbeat:Connect(function(dt)
        lastCheckAccum += dt
        if lastCheckAccum < CHECK_INTERVAL then return end
        lastCheckAccum = 0

        local myChar = player.Character
        local myHRP = myChar and myChar:FindFirstChild("HumanoidRootPart")
        local myHum = myChar and myChar:FindFirstChildOfClass("Humanoid")
        if not (myHRP and myHum and myHum.Health > 0) then
            setState("none")
            return
        end

        -- LOBBY CHECK (tune Y as needed)
        local inLobby = myHRP.Position.Y > 250
        if inLobby then
            setState("none")
            return
        end

        local closeCount = 0
        local aliveOthers = 0

        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= player then
                local char = plr.Character
                local hum = char and char:FindFirstChildOfClass("Humanoid")
                local hrp = char and char:FindFirstChild("HumanoidRootPart")
                if hum and hum.Health > 0 then
                    aliveOthers += 1
                    if hrp then
                        local dist = (myHRP.Position - hrp.Position).Magnitude
                        if dist <= DIST_RADIUS then
                            closeCount += 1
                        end
                    end
                end
            end
        end

        if aliveOthers == 0 then
            setState("none")
            return
        end

        if aliveOthers == 1 and closeCount == 1 then
            setState("lms")
        elseif closeCount >= 2 then
            setState("lockin")
        else
            setState("none")
        end
    end)
end

local function stopLMSCheck()
    if LMS_CheckConnection then
        pcall(function() LMS_CheckConnection:Disconnect() end)
        LMS_CheckConnection = nil
    end
    if myDeathConn then
        pcall(function() myDeathConn:Disconnect() end)
        myDeathConn = nil
    end
    setState("none")
end

--------------------------------------------------
-- TOGGLE FORSAKEN MODE (ON/OFF)
--------------------------------------------------
_G.Modes.ToggleForsaken = function()
    if not Modes.Forsaken then
        -- turning OFF
        stopLMSCheck()

        if teleportWatcherConn then
            pcall(function() teleportWatcherConn:Disconnect() end)
            teleportWatcherConn = nil
        end

        stopForsakenAudio()
        stopLoopSound()
        restoreGameMusic()

        if savedOptimization ~= nil then
            Modes.Optimization = savedOptimization
            if _G.Modes.ToggleOptimization then
                pcall(_G.Modes.ToggleOptimization)
            end
            savedOptimization = nil
        end

        destroyIntro()

        LMS_State = "none"
        introActive = false
        introPlayedThisRound = false

        -- FORCE ESP OFF
        Modes.ESP = false
        if _G.Modes.ToggleESP then
            pcall(_G.Modes.ToggleESP)
        end

        return
    end

    -- turning ON
    LMS_State = "none"
    introPlayedThisRound = false

    startForsakenAudio()
    startLMSCheck()

    -- FORCE ESP ON WHEN FORSAKEN ENABLED
    Modes.ESP = true
    if _G.Modes.ToggleESP then
        pcall(_G.Modes.ToggleESP)
    end

    if teleportWatcherConn then
        pcall(function() teleportWatcherConn:Disconnect() end)
    end

    teleportWatcherConn = RunService.Heartbeat:Connect(function()
        local char = player.Character
        local hrp = char and char:FindFirstChild("HumanoidRootPart")
        if not hrp then return end

        if not prevHRPPos then
            prevHRPPos = hrp.Position
            return
        end

        local dist = (hrp.Position - prevHRPPos).Magnitude
        prevHRPPos = hrp.Position

        -- don't trigger intro in lobby
        local inLobby = hrp.Position.Y > 250
        if inLobby then return end

        if dist >= TELEPORT_MIN_DIST then
            local now = tick()
            if now - lastTeleportTime >= TELEPORT_DEBOUNCE then
                lastTeleportTime = now
                introPlayedThisRound = true
                playForsakenIntro()
            end
        end
    end)
end

--------------------------------------------------
-- UTILITY: REJOIN / RESET / ANTI-AFK
--------------------------------------------------
_G.Modes.ToggleRejoin = function()
    if Modes.Rejoin then
        local placeId = game.PlaceId
        local jobId = game.JobId
        if jobId ~= "" then
            TeleportService:TeleportToPlaceInstance(placeId, jobId, player)
        else
            TeleportService:Teleport(placeId, player)
        end
    end
end

_G.Modes.ToggleResetChar = function()
    if Modes.ResetChar and player.Character then
        local hum = player.Character:FindFirstChildOfClass("Humanoid")
        if hum then hum.Health = 0 end
    end
end

local antiAFKConnection

_G.Modes.ToggleAntiAFK = function()
    if Modes.AntiAFK then
        if antiAFKConnection then antiAFKConnection:Disconnect() end
        antiAFKConnection = player.Idled:Connect(function()
            VirtualUser:Button2Down(Vector2.new(0,0), Workspace.CurrentCamera.CFrame)
            task.wait(0.1)
            VirtualUser:Button2Up(Vector2.new(0,0), Workspace.CurrentCamera.CFrame)
        end)
    else
        if antiAFKConnection then
            antiAFKConnection:Disconnect()
            antiAFKConnection = nil
        end
    end
end
