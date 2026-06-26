local BLACK = Color3.fromRGB(0, 0, 0)
local NEON_BLUE = Color3.fromRGB(255, 255, 255)  -- Agora branco
local DARK_BLUE = Color3.fromRGB(255, 255, 255)  -- Agora branco
local WHITE = Color3.fromRGB(255, 255, 255)
local MENU_ALPHA = 0.95

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local StarterGui = game:GetService("StarterGui")
local player = Players.LocalPlayer
local camera = workspace.CurrentCamera

local freeCamEnabled = false
local smoothCamEnabled = false
local freeCamFOV = 70
local freeCamSpeed = 10
local maxSpeed = 1000
local maxFOV = 500
local freeCamSens = 0.5
local freeCamKeysDown = {}
local freeCamRotating = false
local freeCamOriginalCameraType = nil
local freeCamOriginalSubject = nil
local freeCamOriginalCFrame = nil
local freeCamOriginalFOV = nil
local freeCamStartCFrame = nil
local targetFOV = 70
local fovLerpAlpha = 0.15
local smoothLerpAlpha = 0.4
local freeCamRenderConn = nil
local freeCamInputBeganConn = nil
local freeCamInputEndedConn = nil
local fovIncreasing = false
local fovDecreasing = false
local onMobile = not UserInputService.KeyboardEnabled
local minimized = false
local menuVisible = false
local creatorUserId = nil
local creatorThumbnail = ""
local draggingTitleBar = false
local draggingFloat = false
local dragStart, startPos = nil, nil

local success, result = pcall(function()
    return Players:GetUserIdFromNameAsync("akuramaa_xd")
end)
if success then
    creatorUserId = result
    success, result = pcall(function()
        return Players:GetUserThumbnailAsync(creatorUserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size100x100)
    end)
    if success then
        creatorThumbnail = result
    end
end

if player:WaitForChild("PlayerGui"):FindFirstChild("FreeCamMenu") then
    player:WaitForChild("PlayerGui")["FreeCamMenu"]:Destroy()
end
if player:WaitForChild("PlayerGui"):FindFirstChild("FreeCamControls") then
    player:WaitForChild("PlayerGui")["FreeCamControls"]:Destroy()
end

local main = Instance.new("ScreenGui")
main.Name = "FreeCamMenu"
main.ResetOnSpawn = false
main.DisplayOrder = 999999
main.Parent = player:WaitForChild("PlayerGui")
main.Enabled = true



Frame = Instance.new("Frame")
Frame.Name = "Frame"
Frame.Size = UDim2.new(0, 200, 0, 140)
Frame.Position = UDim2.new(0.5, 288, 0.5, -184)
Frame.BackgroundColor3 = BLACK
Frame.BackgroundTransparency = 1 - MENU_ALPHA
Frame.BorderSizePixel = 0
Frame.Active = false
Frame.Visible = false
Frame.Parent = main

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 8)
frameCorner.Parent = Frame

local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 30)
titleBar.Position = UDim2.new(0, 0, 0, 0)
titleBar.BackgroundTransparency = 1
titleBar.Parent = Frame
titleBar.Active = true

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -60, 0, 30)
title.Position = UDim2.new(0, 10, 0, 0)
title.Text = "Lyra Hub Drone"
title.TextColor3 = NEON_BLUE  -- Agora branco
title.BackgroundTransparency = 1
title.BorderSizePixel = 0
title.Font = Enum.Font.GothamBold
title.TextSize = 16
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = titleBar

local ControlFrame = Instance.new("Frame")
ControlFrame.Size = UDim2.new(1, 0, 1, -30)
ControlFrame.Position = UDim2.new(0, 0, 0, 30)
ControlFrame.BackgroundTransparency = 1
ControlFrame.Parent = Frame
ControlFrame.Visible = true

local SpeedLabel = Instance.new("TextLabel")
SpeedLabel.Name = "SpeedLabel"
SpeedLabel.Parent = ControlFrame
SpeedLabel.BackgroundTransparency = 1
SpeedLabel.Position = UDim2.new(0, 10, 0, 8)
SpeedLabel.Size = UDim2.new(0, 80, 0, 20)
SpeedLabel.Font = Enum.Font.GothamBold
SpeedLabel.Text = "Velocidade: 10"
SpeedLabel.TextColor3 = WHITE
SpeedLabel.TextSize = 12
SpeedLabel.TextXAlignment = Enum.TextXAlignment.Left

local SpeedBox = Instance.new("TextBox")
SpeedBox.Name = "SpeedBox"
SpeedBox.Parent = ControlFrame
SpeedBox.BackgroundColor3 = DARK_BLUE  -- Agora branco
SpeedBox.Position = UDim2.new(0, 95, 0, 6)
SpeedBox.Size = UDim2.new(0, 45, 0, 22)
SpeedBox.Font = Enum.Font.GothamBold
SpeedBox.Text = "10"
SpeedBox.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
SpeedBox.TextSize = 14
SpeedBox.BorderSizePixel = 0
SpeedBox.PlaceholderText = "1-1000"
SpeedBox.ClearTextOnFocus = false

local speedBoxCorner = Instance.new("UICorner")
speedBoxCorner.CornerRadius = UDim.new(0, 6)
speedBoxCorner.Parent = SpeedBox

local FOVLabel = Instance.new("TextLabel")
FOVLabel.Name = "FOVLabel"
FOVLabel.Parent = ControlFrame
FOVLabel.BackgroundTransparency = 1
FOVLabel.Position = UDim2.new(0, 10, 0, 38)
FOVLabel.Size = UDim2.new(0, 80, 0, 20)
FOVLabel.Font = Enum.Font.GothamBold
FOVLabel.Text = "Visão: 70"
FOVLabel.TextColor3 = WHITE
FOVLabel.TextSize = 12
FOVLabel.TextXAlignment = Enum.TextXAlignment.Left

local FOVBox = Instance.new("TextBox")
FOVBox.Name = "FOVBox"
FOVBox.Parent = ControlFrame
FOVBox.BackgroundColor3 = DARK_BLUE  -- Agora branco
FOVBox.Position = UDim2.new(0, 95, 0, 36)
FOVBox.Size = UDim2.new(0, 45, 0, 22)
FOVBox.Font = Enum.Font.GothamBold
FOVBox.Text = "70"
FOVBox.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
FOVBox.TextSize = 14
FOVBox.BorderSizePixel = 0
FOVBox.PlaceholderText = "10-500"
FOVBox.ClearTextOnFocus = false

local fovBoxCorner = Instance.new("UICorner")
fovBoxCorner.CornerRadius = UDim.new(0, 6)
fovBoxCorner.Parent = FOVBox

local FOVUp = Instance.new("TextButton")
FOVUp.Name = "FOVUp"
FOVUp.Parent = ControlFrame
FOVUp.BackgroundColor3 = DARK_BLUE  -- Agora branco
FOVUp.Position = UDim2.new(0, 145, 0, 36)
FOVUp.Size = UDim2.new(0, 20, 0, 22)
FOVUp.Font = Enum.Font.GothamBold
FOVUp.Text = "+"
FOVUp.TextSize = 16
FOVUp.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
FOVUp.BorderSizePixel = 0

local fovUpCorner = Instance.new("UICorner")
fovUpCorner.CornerRadius = UDim.new(0, 4)
fovUpCorner.Parent = FOVUp

local FOVDown = Instance.new("TextButton")
FOVDown.Name = "FOVDown"
FOVDown.Parent = ControlFrame
FOVDown.BackgroundColor3 = DARK_BLUE  -- Agora branco
FOVDown.Position = UDim2.new(0, 170, 0, 36)
FOVDown.Size = UDim2.new(0, 20, 0, 22)
FOVDown.Font = Enum.Font.GothamBold
FOVDown.Text = "-"
FOVDown.TextSize = 16
FOVDown.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
FOVDown.BorderSizePixel = 0

local fovDownCorner = Instance.new("UICorner")
fovDownCorner.CornerRadius = UDim.new(0, 4)
fovDownCorner.Parent = FOVDown

local Toggle = Instance.new("TextButton")
Toggle.Name = "Toggle"
Toggle.Parent = ControlFrame
Toggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
Toggle.Position = UDim2.new(0, 10, 0, 68)
Toggle.Size = UDim2.new(0, 85, 0, 24)
Toggle.Font = Enum.Font.GothamBold
Toggle.Text = "Começar"
Toggle.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
Toggle.TextSize = 14
Toggle.BorderSizePixel = 0

local toggleCorner = Instance.new("UICorner")
toggleCorner.CornerRadius = UDim.new(0, 6)
toggleCorner.Parent = Toggle

local SmoothToggle = Instance.new("TextButton")
SmoothToggle.Name = "Smooth"
SmoothToggle.Parent = ControlFrame
SmoothToggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
SmoothToggle.Position = UDim2.new(0, 100, 0, 68)
SmoothToggle.Size = UDim2.new(0, 90, 0, 24)
SmoothToggle.Font = Enum.Font.GothamBold
SmoothToggle.Text = "Suave: Desligado"
SmoothToggle.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
SmoothToggle.TextSize = 12
SmoothToggle.BorderSizePixel = 0

local smoothCorner = Instance.new("UICorner")
smoothCorner.CornerRadius = UDim.new(0, 6)
smoothCorner.Parent = SmoothToggle




local controlGui = Instance.new("ScreenGui")
controlGui.Name = "FreeCamControls"
controlGui.ResetOnSpawn = false
controlGui.DisplayOrder = 999999
controlGui.Parent = player:WaitForChild("PlayerGui")
controlGui.Enabled = false

local controlFrame = Instance.new("Frame")
controlFrame.Name = "ControlPad"
controlFrame.Size = UDim2.new(0, 180, 0, 180)
controlFrame.Position = UDim2.new(0, 10, 1, -190)
controlFrame.BackgroundTransparency = 1
controlFrame.Parent = controlGui
controlFrame.Visible = true

local upBtn = Instance.new("TextButton")
upBtn.Name = "Up"
upBtn.Size = UDim2.new(0, 55, 0, 55)
upBtn.Position = UDim2.new(0.5, -30, 0, 5)
upBtn.Text = "↑"
upBtn.Font = Enum.Font.GothamBold
upBtn.TextSize = 20
upBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
upBtn.BackgroundColor3 = DARK_BLUE  -- Agora branco
upBtn.BackgroundTransparency = 0.2
upBtn.BorderSizePixel = 0
upBtn.Parent = controlFrame

local upCorner = Instance.new("UICorner")
upCorner.CornerRadius = UDim.new(0, 6)
upCorner.Parent = upBtn

local leftBtn = Instance.new("TextButton")
leftBtn.Name = "Left"
leftBtn.Size = UDim2.new(0, 55, 0, 55)
leftBtn.Position = UDim2.new(0, 5, 0.5, -30)
leftBtn.Text = "←"
leftBtn.Font = Enum.Font.GothamBold
leftBtn.TextSize = 20
leftBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
leftBtn.BackgroundColor3 = DARK_BLUE  -- Agora branco
leftBtn.BackgroundTransparency = 0.2
leftBtn.BorderSizePixel = 0
leftBtn.Parent = controlFrame

local leftCorner = Instance.new("UICorner")
leftCorner.CornerRadius = UDim.new(0, 6)
leftCorner.Parent = leftBtn

local downBtn = Instance.new("TextButton")
downBtn.Name = "Down"
downBtn.Size = UDim2.new(0, 55, 0, 55)
downBtn.Position = UDim2.new(0.5, -30, 1, -65)
downBtn.Text = "↓"
downBtn.Font = Enum.Font.GothamBold
downBtn.TextSize = 20
downBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
downBtn.BackgroundColor3 = DARK_BLUE  -- Agora branco
downBtn.BackgroundTransparency = 0.2
downBtn.BorderSizePixel = 0
downBtn.Parent = controlFrame

local downCorner = Instance.new("UICorner")
downCorner.CornerRadius = UDim.new(0, 6)
downCorner.Parent = downBtn

local rightBtn = Instance.new("TextButton")
rightBtn.Name = "Right"
rightBtn.Size = UDim2.new(0, 55, 0, 55)
rightBtn.Position = UDim2.new(1, -65, 0.5, -30)
rightBtn.Text = "→"
rightBtn.Font = Enum.Font.GothamBold
rightBtn.TextSize = 20
rightBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
rightBtn.BackgroundColor3 = DARK_BLUE  -- Agora branco
rightBtn.BackgroundTransparency = 0.2
rightBtn.BorderSizePixel = 0
rightBtn.Parent = controlFrame

local rightCorner = Instance.new("UICorner")
rightCorner.CornerRadius = UDim.new(0, 6)
rightCorner.Parent = rightBtn

local verticalUpBtn = Instance.new("TextButton")
verticalUpBtn.Name = "VerticalUp"
verticalUpBtn.Size = UDim2.new(0, 40, 0, 40)
verticalUpBtn.Position = UDim2.new(0.5, 35, 0, 15)
verticalUpBtn.Text = "↑"
verticalUpBtn.Font = Enum.Font.GothamBold
verticalUpBtn.TextSize = 18
verticalUpBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
verticalUpBtn.BackgroundColor3 = NEON_BLUE  -- Agora branco
verticalUpBtn.BackgroundTransparency = 0.2
verticalUpBtn.BorderSizePixel = 0
verticalUpBtn.Parent = controlFrame

local verticalUpCorner = Instance.new("UICorner")
verticalUpCorner.CornerRadius = UDim.new(0, 6)
verticalUpCorner.Parent = verticalUpBtn

local verticalDownBtn = Instance.new("TextButton")
verticalDownBtn.Name = "VerticalDown"
verticalDownBtn.Size = UDim2.new(0, 40, 0, 40)
verticalDownBtn.Position = UDim2.new(0.5, -85, 0, 15)
verticalDownBtn.Text = "↓"
verticalDownBtn.Font = Enum.Font.GothamBold
verticalDownBtn.TextSize = 18
verticalDownBtn.TextColor3 = BLACK  -- Texto preto para contraste com fundo branco
verticalDownBtn.BackgroundColor3 = NEON_BLUE  -- Agora branco
verticalDownBtn.BackgroundTransparency = 0.2
verticalDownBtn.BorderSizePixel = 0
verticalDownBtn.Parent = controlFrame

local verticalDownCorner = Instance.new("UICorner")
verticalDownCorner.CornerRadius = UDim.new(0, 6)
verticalDownCorner.Parent = verticalDownBtn

local function stopFreeCam()
    freeCamEnabled = false
    smoothCamEnabled = false
    fovIncreasing = false
    fovDecreasing = false
    Toggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
    Toggle.Text = "Começar"
    SmoothToggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
    SmoothToggle.Text = "Suave: Desligado"
    if controlGui then 
        controlGui.Enabled = false 
    end

    if freeCamRenderConn then 
        freeCamRenderConn:Disconnect() 
        freeCamRenderConn = nil 
    end
    if freeCamInputBeganConn then 
        freeCamInputBeganConn:Disconnect() 
        freeCamInputBeganConn = nil 
    end
    if freeCamInputEndedConn then 
        freeCamInputEndedConn:Disconnect() 
        freeCamInputEndedConn = nil 
    end

    camera.CameraType = Enum.CameraType.Custom
    if freeCamOriginalSubject then
        camera.CameraSubject = freeCamOriginalSubject
    else
        local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then 
            camera.CameraSubject = humanoid 
        end
    end
    camera.FieldOfView = freeCamOriginalFOV or 70
    freeCamFOV = camera.FieldOfView
    FOVBox.Text = tostring(math.floor(freeCamFOV))
    FOVLabel.Text = "Visão: " .. math.floor(freeCamFOV)
    player.CameraMaxZoomDistance = 400
    targetFOV = freeCamFOV
    freeCamKeysDown = {}
    freeCamRotating = false
end

local function sendNotif(titleT, textT, image)
    pcall(function()
        StarterGui:SetCore("SendNotification", {
            Title = titleT,
            Text = textT,
            Duration = 6,
            Icon = image or ""
        })
    end)
end

upBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.W] = true 
end)
upBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.W] = false 
end)
upBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.W] = false 
end)

verticalUpBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.Space] = true 
end)
verticalUpBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.Space] = false 
end)
verticalUpBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.Space] = false 
end)

verticalDownBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.LeftShift] = true 
end)
verticalDownBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.LeftShift] = false 
end)
verticalDownBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.LeftShift] = false 
end)

leftBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.A] = true 
end)
leftBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.A] = false 
end)
leftBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.A] = false 
end)

downBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.S] = true 
end)
downBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.S] = false 
end)
downBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.S] = false 
end)

rightBtn.MouseButton1Down:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.D] = true 
end)
rightBtn.MouseButton1Up:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.D] = false 
end)
rightBtn.MouseLeave:Connect(function() 
    freeCamKeysDown[Enum.KeyCode.D] = false 
end)

SpeedBox.FocusLost:Connect(function(enterPressed)
    local value = tonumber(SpeedBox.Text)
    if value then
        value = math.clamp(value, 1, maxSpeed)
        freeCamSpeed = value
        SpeedBox.Text = tostring(math.floor(value))
        SpeedLabel.Text = "Velocidade: " .. math.floor(value)
    else
        SpeedBox.Text = tostring(math.floor(freeCamSpeed))
    end
end)

FOVBox.FocusLost:Connect(function(enterPressed)
    local value = tonumber(FOVBox.Text)
    if value then
        value = math.clamp(value, 10, maxFOV)
        freeCamFOV = value
        targetFOV = value
        FOVBox.Text = tostring(math.floor(value))
        FOVLabel.Text = "Visão: " .. math.floor(value)
        if freeCamEnabled then
            camera.FieldOfView = value
        end
    else
        FOVBox.Text = tostring(math.floor(freeCamFOV))
    end
end)

SmoothToggle.MouseButton1Click:Connect(function()
    smoothCamEnabled = not smoothCamEnabled
    if smoothCamEnabled then
        SmoothToggle.BackgroundColor3 = NEON_BLUE  -- Agora branco
        SmoothToggle.Text = "Suave: Ativo"
    else
        SmoothToggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
        SmoothToggle.Text = "Suave: Desligado"
    end
end)

FOVUp.MouseButton1Down:Connect(function()
    fovIncreasing = true
end)
FOVUp.MouseButton1Up:Connect(function()
    fovIncreasing = false
end)
FOVUp.MouseLeave:Connect(function()
    fovIncreasing = false
end)

FOVDown.MouseButton1Down:Connect(function()
    fovDecreasing = true
end)
FOVDown.MouseButton1Up:Connect(function()
    fovDecreasing = false
end)
FOVDown.MouseLeave:Connect(function()
    fovDecreasing = false
end)

Toggle.MouseButton1Down:Connect(function()
    if freeCamEnabled then
        stopFreeCam()
    else
        freeCamEnabled = true
        smoothCamEnabled = false
        Toggle.BackgroundColor3 = NEON_BLUE  -- Agora branco
        Toggle.Text = "Para"
        SmoothToggle.BackgroundColor3 = DARK_BLUE  -- Agora branco
        SmoothToggle.Text = "Suave: Desligado"
        if controlGui then 
            controlGui.Enabled = true 
        end

        freeCamOriginalCameraType = camera.CameraType
        freeCamOriginalSubject = camera.CameraSubject
        freeCamOriginalCFrame = camera.CFrame
        freeCamOriginalFOV = camera.FieldOfView
        freeCamStartCFrame = camera.CFrame
        targetFOV = freeCamFOV
        if onMobile then 
            freeCamSens = 0.8 
        else 
            freeCamSens = 0.5 
        end

        camera.CameraType = Enum.CameraType.Scriptable
        camera.FieldOfView = freeCamFOV
        player.CameraMaxZoomDistance = 9999

        freeCamKeysDown = {}
        freeCamRotating = false

        freeCamRenderConn = RunService.RenderStepped:Connect(function()
            local currentCF = camera.CFrame
            local targetCF = currentCF

            if freeCamRotating then
                local delta = UserInputService:GetMouseDelta()
                local cf = targetCF
                local yAngle = cf:ToEulerAngles(Enum.RotationOrder.YZX)
                local newAmount = math.deg(yAngle) + delta.Y
                if newAmount > 65 or newAmount < -65 then
                    if not (yAngle < 0 and delta.Y < 0) and not (yAngle > 0 and delta.Y > 0) then
                        delta = Vector2.new(delta.X, 0)
                    end
                end
                local rotCF = cf * CFrame.Angles(-math.rad(delta.Y), 0, 0)
                rotCF = CFrame.Angles(0, -math.rad(delta.X), 0) * (rotCF - rotCF.Position) + rotCF.Position
                rotCF = CFrame.lookAt(rotCF.Position, rotCF.Position + rotCF.LookVector)
                if delta.Magnitude > 0 then
                    targetCF = targetCF:Lerp(rotCF, freeCamSens)
                end
                UserInputService.MouseBehavior = Enum.MouseBehavior.LockCurrentPosition
            else
                UserInputService.MouseBehavior = Enum.MouseBehavior.Default
            end

            local moveSpeed = freeCamSpeed / 10
            if freeCamKeysDown[Enum.KeyCode.W] then
                targetCF = targetCF * CFrame.new(0, 0, -moveSpeed)
            end
            if freeCamKeysDown[Enum.KeyCode.S] then
                targetCF = targetCF * CFrame.new(0, 0, moveSpeed)
            end
            if freeCamKeysDown[Enum.KeyCode.A] then
                targetCF = targetCF * CFrame.new(-moveSpeed, 0, 0)
            end
            if freeCamKeysDown[Enum.KeyCode.D] then
                targetCF = targetCF * CFrame.new(moveSpeed, 0, 0)
            end
            if freeCamKeysDown[Enum.KeyCode.Space] then
                targetCF = targetCF * CFrame.new(0, moveSpeed, 0)
            end
            if freeCamKeysDown[Enum.KeyCode.LeftShift] then
                targetCF = targetCF * CFrame.new(0, -moveSpeed, 0)
            end

            local movementLerpAlpha = smoothCamEnabled and smoothLerpAlpha or 1
            camera.CFrame = currentCF:Lerp(targetCF, movementLerpAlpha)

            if fovIncreasing then
                targetFOV = math.max(10, targetFOV - 1)
                freeCamFOV = targetFOV
                FOVBox.Text = tostring(math.floor(freeCamFOV))
                FOVLabel.Text = "Visão: " .. math.floor(freeCamFOV)
            end
            if fovDecreasing then
                targetFOV = math.min(maxFOV, targetFOV + 1)
                freeCamFOV = targetFOV
                FOVBox.Text = tostring(math.floor(freeCamFOV))
                FOVLabel.Text = "Visão: " .. math.floor(freeCamFOV)
            end
            camera.FieldOfView = camera.FieldOfView + (targetFOV - camera.FieldOfView) * fovLerpAlpha
        end)

        freeCamInputBeganConn = UserInputService.InputBegan:Connect(function(input)
            if input.KeyCode then
                freeCamKeysDown[input.KeyCode] = true
            end
            if input.UserInputType == Enum.UserInputType.MouseButton2 or (input.UserInputType == Enum.UserInputType.Touch and UserInputService:GetMouseLocation().X > (camera.ViewportSize.X / 2)) then
                freeCamRotating = true
            end
        end)

        freeCamInputEndedConn = UserInputService.InputEnded:Connect(function(input)
            if input.KeyCode then
                freeCamKeysDown[input.KeyCode] = false
            end
            if input.UserInputType == Enum.UserInputType.MouseButton2 or (input.UserInputType == Enum.UserInputType.Touch and UserInputService:GetMouseLocation().X > (camera.ViewportSize.X / 2)) then
                freeCamRotating = false
            end
        end)
    end
end)


titleBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        draggingTitleBar = true
        dragStart = input.Position
        startPos = Frame.Position
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        draggingTitleBar = false
        draggingFloat = false
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if draggingTitleBar and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        Frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
    if draggingFloat and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local delta = input.Position - dragStart
        FloatingButton.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

player.CharacterAdded:Connect(function()
    task.wait(0.7)
    if freeCamEnabled then 
        stopFreeCam() 
    end
end)
