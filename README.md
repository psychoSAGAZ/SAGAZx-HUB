--// SERVIÇOS
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

--// GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "RedzHubIntro"
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = PlayerGui

-- Fundo
local bg = Instance.new("Frame")
bg.Size = UDim2.fromScale(1,1)
bg.BackgroundColor3 = Color3.fromRGB(0,0,0)
bg.BackgroundTransparency = 1
bg.Parent = screenGui

-- Logo
local logo = Instance.new("TextLabel")
logo.Size = UDim2.new(0.6,0,0.2,0)
logo.Position = UDim2.new(0.5,0,-0.2,0)
logo.AnchorPoint = Vector2.new(0.5,0.5)
logo.BackgroundTransparency = 1
logo.Text = "SAGAZx HUB"
logo.TextScaled = true
logo.Font = Enum.Font.GothamBold
logo.TextColor3 = Color3.fromRGB(128, 86, 255)
logo.TextStrokeTransparency = 0.3
logo.TextStrokeColor3 = Color3.fromRGB(128, 86, 255)
logo.Parent = screenGui

local logoGradient = Instance.new("UIGradient")
logoGradient.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(128, 86, 255)),
	ColorSequenceKeypoint.new(0.5, Color3.fromRGB(60,0,0)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(128, 86, 255))
}
logoGradient.Rotation = 45
logoGradient.Parent = logo

-- Subtítulo
local subtitle = Instance.new("TextLabel")
subtitle.Size = UDim2.new(0,200,0,25)
subtitle.Position = UDim2.new(0.5,0,0.58,0)
subtitle.AnchorPoint = Vector2.new(0.5,0.5)
subtitle.BackgroundTransparency = 1
subtitle.Text = "by SAGAZx"
subtitle.TextColor3 = Color3.fromRGB(128, 86, 255)
subtitle.TextTransparency = 1
subtitle.TextScaled = true
subtitle.Font = Enum.Font.Gotham
subtitle.Parent = screenGui

-- Barra de carregamento
local loadFrame = Instance.new("Frame")
loadFrame.Size = UDim2.new(0,0,0.02,0)
loadFrame.Position = UDim2.new(0.5,0,0.85,0)
loadFrame.AnchorPoint = Vector2.new(0.5,0)
loadFrame.BackgroundColor3 = Color3.fromRGB(128, 86, 255)
loadFrame.BorderSizePixel = 0
loadFrame.Parent = screenGui

-- Função Tween
local function tween(obj, info, props)
	return TweenService:Create(obj, info, props)
end

-- Fade fundo
tween(bg, TweenInfo.new(0.5), {BackgroundTransparency = 0}):Play()
task.wait(0.6)

-- Entrada logo
tween(logo, TweenInfo.new(1, Enum.EasingStyle.Quart, Enum.EasingDirection.Out), {
	Position = UDim2.new(0.5,0,0.4,0)
}):Play()

task.wait(1)

-- Subtítulo aparece
tween(subtitle, TweenInfo.new(1), {TextTransparency = 0}):Play()

-- Barra carrega
tween(loadFrame, TweenInfo.new(2, Enum.EasingStyle.Linear), {
	Size = UDim2.new(0.8,0,0.02,0)
}):Play()

-- Som
local sound = Instance.new("Sound")
sound.SoundId = "rbxassetid://107004225739474"
sound.Volume = 2
sound.Parent = screenGui
sound:Play()

-- Saída
task.wait(2.5)

tween(bg, TweenInfo.new(0.8), {BackgroundTransparency = 1}):Play()
tween(logo, TweenInfo.new(0.8), {TextTransparency = 1}):Play()
tween(subtitle, TweenInfo.new(0.8), {TextTransparency = 1}):Play()
tween(loadFrame, TweenInfo.new(0.8), {BackgroundTransparency = 1}):Play()

task.wait(1)
screenGui:Destroy()

--nome roleplay

local args = {
    "RolePlayName",
    "SAGAZx HUB"
}
game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1RPNam1eTex1t"):FireServer(unpack(args))
local args = {
    "PickingRPNameColor",
    Color3.fromRGB(128, 86, 255)
}
game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1RPNam1eColo1r"):FireServer(unpack(args))
local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer

local args1 = {
    "RolePlayBio",
    "BEM-VINDO " .. localPlayer.DisplayName
}
game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1RPNam1eTex1t"):FireServer(unpack(args1))

local args2 = {
    "PickingRPBioColor",
    Color3.fromRGB(87, 191, 255)
}
game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1RPNam1eColo1r"):FireServer(unpack(args2))

local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/ndjdjfhfbdbbdd/refs/heads/main/README.md"))()

-- CONFIG DO SOM
local ClickSoundSettings = {
    Enabled = true,
    SoundId = "rbxassetid://18998603679", -- pode trocar
    Volume = 0.1
}

-- FUNÇÃO DO SOM
local function PlayClickSound()
    if ClickSoundSettings.Enabled then
        local sound = Instance.new("Sound")
        sound.SoundId = ClickSoundSettings.SoundId
        sound.Volume = ClickSoundSettings.Volume
        sound.Parent = game:GetService("SoundService")
        sound:Play()
        sound.Ended:Connect(function()
            sound:Destroy()
        end)
    end
end

-- CONECTA SOM EM TODOS OS BOTÕES
local function ConnectButtons(parent)
    local function check(obj)
        if obj:IsA("TextButton") or obj:IsA("ImageButton") then
            obj.Activated:Connect(PlayClickSound)
        end
    end

    for _, v in pairs(parent:GetDescendants()) do
        check(v)
    end

    parent.DescendantAdded:Connect(check)
end

local Window = redzlib:MakeWindow({
    Title = "SAGAZx HUB| brookhaven",
    SubTitle = "| by SAGAZx",
    SaveFolder = "SAGAZxConfig"
})

ConnectButtons(game:GetService("CoreGui"))

Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://86050226751861", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(0, 8) },
})



----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Home-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab1 = Window:MakeTab({ "| Ini­cio", "menu" })



Tab1:AddSection({Name = "Perfil"})


local function detectExecutor()
    if identifyexecutor then
        return identifyexecutor()
    elseif syn then
        return "Synapse X4"
    elseif KRNL_LOADED then
        return "KRNL4"
    elseif is_sirhurt_closure then
        return "SirHurt"
    elseif pebc_execute then
        return "ProtoSmasher"
    elseif getexecutorname then
        return getexecutorname()
    else
        return "Executor Desconhecido"
    end
end

local executorName = detectExecutor()



local Paragraph = Tab1:AddParagraph({"Execultor", executorName})

local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Pega nickname do jogador
local nickname = player.Name 

-- Novo bloco igual ao do Executor
Tab1:AddParagraph({"Nickname", nickname})
Tab1:AddParagraph({"Versão", "1.0.0"})

----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Cliente-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

local Tab2 = Window:MakeTab({ "| Cliente", "user" })

Tab2:AddSlider({
    Name = "VELOCIDADE",
    Increase = 1,
    MinValue = 16,
    MaxValue = 1000,
    Default = 16,
    Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if humanoid then
            humanoid.WalkSpeed = Value
        end
    end
 })
 
 Tab2:AddSlider({
    Name = "PULO",
    Increase = 1,
    MinValue = 50,
    MaxValue = 500,
    Default = 50,
    Callback = function(Value)
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        
        if humanoid then
            humanoid.JumpPower = Value
        end
    end
 })
 
 Tab2:AddSlider({
    Name = "GRAVIDADE",
    Increase = 1,
    MinValue = 0,
    MaxValue = 10000,
    Default = 196.2,
    Callback = function(Value)
        game.Workspace.Gravity = Value
    end
 })
 
 local InfiniteJumpEnabled = false
 
 game:GetService("UserInputService").JumpRequest:Connect(function()
    if InfiniteJumpEnabled then
       local character = game.Players.LocalPlayer.Character
       if character and character:FindFirstChild("Humanoid") then
          character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
       end
    end
 end)

 Tab2:AddButton({
    Name = "REDEFINIR VELOCIDADE/GRAVIDADE/ PULO",
    Callback = function()
        -- Resetar Speed
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = 16 -- Valor padrÃ£o do Speed
            humanoid.JumpPower = 50 -- Valor padrÃ£o do JumpPower
        end
        
        -- Resetar Gravity
        game.Workspace.Gravity = 196.2 -- Valor padrÃ£o da gravidade
        
        -- Desativar Infinite Jump
        InfiniteJumpEnabled = false
    end
})
 
 Tab2:AddToggle({
    Name = "PULO INFINITO",
    Default = false,
    Callback = function(Value)
       InfiniteJumpEnabled = Value
    end
 })

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local noclipEnabled = false

-- Atualiza o personagem caso respawn
player.CharacterAdded:Connect(function(char)
    character = char
end)

Tab2:AddToggle({
    Name = "NOCLIP",
    Description = "ATRAVESSA PAREDES",
    Default = false,
    Callback = function(v)
        noclipEnabled = v
        if noclipEnabled then
            print("Noclip Ativado!")
        else
            print("Noclip Desativado!")
        end
    end
})

-- Loop do noclip
RunService.Stepped:Connect(function()
    if noclipEnabled and character then
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") and part.CanCollide == true then
                part.CanCollide = false
            end
        end
    end
end)

-- Serviços
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Variáveis
local selectedColor = "RGB"
local espEnabled = false
local billboardGuis = {}
local connections = {}

-- Dropdown de cores
Tab2:AddDropdown({
    Name = "COR DO ESP",
    Default = "RGB",
    Options = {"RGB", "Branco", "Preto", "Vermelho", "Verde", "Azul", "Amarelo", "Rosa", "Roxo"},
    Callback = function(value)
        selectedColor = value
        -- Atualiza cores imediatamente
        for _, gui in pairs(billboardGuis) do
            if gui and gui:FindFirstChild("TextLabel") then
                gui.TextLabel.TextColor3 = (selectedColor == "RGB" and gui.TextLabel.TextColor3) or getESPColor()
            end
        end
    end
})

-- Função para obter a cor
local function getESPColor()
    if selectedColor == "RGB" then
        local h = (tick() % 5) / 5
        return Color3.fromHSV(h, 1, 1)
    elseif selectedColor == "Preto" then return Color3.fromRGB(0,0,0)
    elseif selectedColor == "Branco" then return Color3.fromRGB(255,255,255)
    elseif selectedColor == "Vermelho" then return Color3.fromRGB(255,0,0)
    elseif selectedColor == "Verde" then return Color3.fromRGB(0,255,0)
    elseif selectedColor == "Azul" then return Color3.fromRGB(0,170,255)
    elseif selectedColor == "Amarelo" then return Color3.fromRGB(255,255,0)
    elseif selectedColor == "Rosa" then return Color3.fromRGB(255,105,180)
    elseif selectedColor == "Roxo" then return Color3.fromRGB(128,0,128)
    end
    return Color3.new(1,1,1)
end

-- Função para criar ou atualizar ESP
local function updateESP(player)
    if player == Players.LocalPlayer or not espEnabled then return end
    local character = player.Character
    if not character then return end
    local head = character:FindFirstChild("Head")
    if not head then return end

    local gui = billboardGuis[player]
    if gui and gui:FindFirstChild("TextLabel") then
        -- Atualiza apenas a cor
        gui.TextLabel.TextColor3 = getESPColor()
        return
    elseif gui then
        gui:Destroy()
    end

    -- Cria novo BillboardGui
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "ESP_Billboard"
    billboard.Parent = head
    billboard.Adornee = head
    billboard.Size = UDim2.new(0, 200, 0, 50)
    billboard.StudsOffset = Vector3.new(0,3,0)
    billboard.AlwaysOnTop = true

    local textLabel = Instance.new("TextLabel")
    textLabel.Name = "TextLabel"
    textLabel.Parent = billboard
    textLabel.Size = UDim2.new(1,0,1,0)
    textLabel.BackgroundTransparency = 1
    textLabel.TextStrokeTransparency = 0.5
    textLabel.Font = Enum.Font.SourceSansBold
    textLabel.TextSize = 14
    textLabel.Text = player.Name .. " | " .. player.AccountAge .. " dias"
    textLabel.TextColor3 = getESPColor()

    billboardGuis[player] = billboard
end

-- Função para remover ESP
local function removeESP(player)
    if billboardGuis[player] then
        billboardGuis[player]:Destroy()
        billboardGuis[player] = nil
    end
end

-- Toggle ESP
Tab2:AddToggle({
    Name = "ESP",
    Description = "MOSTRA NOME E DIAS DOS PLAYERS",
    Default = false,
    Callback = function(value)
        espEnabled = value

        if espEnabled then
            -- Atualiza todos os jogadores
            for _, player in pairs(Players:GetPlayers()) do
                updateESP(player)
            end

            -- Atualiza cores RGB
            table.insert(connections, RunService.Heartbeat:Connect(function()
                if selectedColor == "RGB" then
                    for _, player in pairs(Players:GetPlayers()) do
                        local gui = billboardGuis[player]
                        if gui and gui:FindFirstChild("TextLabel") then
                            gui.TextLabel.TextColor3 = getESPColor()
                        end
                    end
                end
            end))

            -- Conexão PlayerAdded
            table.insert(connections, Players.PlayerAdded:Connect(function(player)
                updateESP(player)
                table.insert(connections, player.CharacterAdded:Connect(function()
                    updateESP(player)
                end))
            end))

            -- Conexão PlayerRemoving
            table.insert(connections, Players.PlayerRemoving:Connect(function(player)
                removeESP(player)
            end))
        else
            -- Desliga ESP
            for _, player in pairs(Players:GetPlayers()) do
                removeESP(player)
            end
            for _, conn in pairs(connections) do
                conn:Disconnect()
            end
            connections = {}
            billboardGuis = {}
        end
    end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Jogadores-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

local Tab3= Window:MakeTab({ "| Jogadores", "users" })









local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local selectedPlayer = nil  -- substitui Target

-- 🔔 SISTEMA DE NOTIFICAÇÃO (HEADER STYLE)
local function CreateNotification(title, message, duration)
    duration = duration or 4

    local playerGui = LocalPlayer:WaitForChild("PlayerGui")

    if playerGui:FindFirstChild("SimpleNotify") then
        playerGui.SimpleNotify:Destroy()
    end

    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "SimpleNotify"
    screenGui.ResetOnSpawn = false
    screenGui.Parent = playerGui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 420, 0, 42)
    frame.Position = UDim2.new(0.5, -210, 0, -50)
    frame.BackgroundColor3 = Color3.fromRGB(27,5, 25, 30)
    frame.BorderSizePixel = 0
    frame.Parent = screenGui

    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 6)

    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -45, 1, 0)
    textLabel.Position = UDim2.new(0, 10, 0, 0)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = string.upper(title)..": "..message
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.SourceSansSemibold
    textLabel.TextSize = 16
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.Parent = frame

    local close = Instance.new("TextButton")
    close.Size = UDim2.new(0, 30, 1, 0)
    close.Position = UDim2.new(1, -30, 0, 0)
    close.BackgroundTransparency = 1
    close.Text = "X"
    close.TextColor3 = Color3.fromRGB(255,255,255)
    close.Font = Enum.Font.SourceSansBold
    close.TextSize = 18
    close.Parent = frame

    TweenService:Create(
        frame,
        TweenInfo.new(0.35, Enum.EasingStyle.Quint, Enum.EasingDirection.Out),
        {Position = UDim2.new(0.5, -210, 0, 5)}
    ):Play()

    local closed = false
    local function Close()
        if closed then return end
        closed = true

        TweenService:Create(
            frame,
            TweenInfo.new(0.25, Enum.EasingStyle.Quint, Enum.EasingDirection.In),
            {Position = UDim2.new(0.5, -210, 0, -50)}
        ):Play()

        task.delay(0.3, function()
            screenGui:Destroy()
        end)
    end

    close.MouseButton1Click:Connect(Close)
    task.delay(duration, Close)
end

-- 📋 LISTA DE PLAYERS
local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

-- 🎯 DROPDOWN DE TARGET
local DropdownJogadores = Tab3:AddDropdown({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = nil,
    Callback = function(Value)
        selectedPlayer = Value  -- aqui é a mudança principal
        print("Alvo selecionado: " .. tostring(selectedPlayer))

        CreateNotification("Notificação", "Player selecionado: "..Value, 3)
    end
})

-- 🔁 ATUALIZAÇÃO AUTOMÁTICA
local function UpdateDropdown()
    task.wait(0.5)
    if DropdownJogadores then
        local selecionadoAntes = selectedPlayer
        local nomesAtualizados = GetPlayerNames()

        if DropdownJogadores.Set then
            DropdownJogadores:Set(nomesAtualizados)
        elseif DropdownJogadores.Refresh then
            DropdownJogadores:Refresh(nomesAtualizados, true)
        end

        if selecionadoAntes then
            local aindaEstaNoJogo = false
            for _, nome in ipairs(nomesAtualizados) do
                if nome == selecionadoAntes then
                    aindaEstaNoJogo = true
                    break
                end
            end

            if aindaEstaNoJogo then
                selectedPlayer = selecionadoAntes
                if DropdownJogadores.Set then
                    DropdownJogadores:Set(selecionadoAntes)
                end
            else
                selectedPlayer = nil
            end
        end
    end
end

-- PLAYER ENTROU
Players.PlayerAdded:Connect(UpdateDropdown)

-- PLAYER SAIU
Players.PlayerRemoving:Connect(function(plr)
    if selectedPlayer and plr.Name == selectedPlayer then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
    end

    UpdateDropdown()
end)



local viewing = false
local cam = workspace.CurrentCamera
local player = game.Players.LocalPlayer

-- Função de notificação com imagem
local function ShowPlayerNotification(plr)
    local username = plr.Name
    local displayname = plr.DisplayName

    local thumbUrl = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. plr.UserId .. "&width=150&height=150&format=png"

    local playerGui = player:WaitForChild("PlayerGui")
    local screenGui = playerGui:FindFirstChild("AnexedNotificationUI")
    if not screenGui then
        screenGui = Instance.new("ScreenGui")
        screenGui.IgnoreGuiInset = true
        screenGui.Name = "AnexedNotificationUI"
        screenGui.ResetOnSpawn = false
        screenGui.Parent = playerGui
    end

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 60)
    frame.Position = UDim2.new(1, 0, 0, -10)
    frame.AnchorPoint = Vector2.new(1, 0)
    frame.BackgroundTransparency = 1
    frame.BorderSizePixel = 0
    frame.ZIndex = 20
    frame.Parent = screenGui

    local image = Instance.new("ImageLabel", frame)
    image.Size = UDim2.new(0, 40, 0, 40)
    image.Position = UDim2.new(0, 10, 0, 10)
    image.BackgroundTransparency = 1
    image.Image = thumbUrl

    local title = Instance.new("TextLabel", frame)
    title.Size = UDim2.new(1, -60, 0, 20)
    title.Position = UDim2.new(0, 60, 0, 8)
    title.BackgroundTransparency = 1
    title.Text = "Visualizando " .. displayname
    title.TextColor3 = Color3.new(1, 1, 1)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 14
    title.TextXAlignment = Enum.TextXAlignment.Left

    local subtitle = Instance.new("TextLabel", frame)
    subtitle.Size = UDim2.new(1, -60, 0, 18)
    subtitle.Position = UDim2.new(0, 60, 0, 30)
    subtitle.BackgroundTransparency = 1
    subtitle.Text = "@" .. username
    subtitle.TextColor3 = Color3.new(1, 1, 1)
    subtitle.Font = Enum.Font.Gotham
    subtitle.TextSize = 12
    subtitle.TextXAlignment = Enum.TextXAlignment.Left

    local TweenService = game:GetService("TweenService")
    local enterTween = TweenService:Create(frame, TweenInfo.new(0.4, Enum.EasingStyle.Quart), {
        Position = UDim2.new(1, -10, 0, 10)
    })
    enterTween:Play()

    task.delay(3, function()
        local exitTween = TweenService:Create(frame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Position = UDim2.new(1, 0, 0, -60)
        })
        exitTween:Play()
        exitTween.Completed:Wait()
        frame:Destroy()
    end)
end

-- Notificação de saida
local function ShowLeaveNotification(playerName)
    local playerGui = player:WaitForChild("PlayerGui")
    local screenGui = playerGui:FindFirstChild("AnexedNotificationUI")
    if not screenGui then
        screenGui = Instance.new("ScreenGui")
        screenGui.IgnoreGuiInset = true
        screenGui.Name = "AnexedNotificationUI"
        screenGui.ResetOnSpawn = false
        screenGui.Parent = playerGui
    end

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 240, 0, 40)
    frame.Position = UDim2.new(1, 0, 0, -10)
    frame.AnchorPoint = Vector2.new(1, 0)
    frame.BackgroundTransparency = 1
    frame.BorderSizePixel = 0
    frame.ZIndex = 20
    frame.Parent = screenGui

    local title = Instance.new("TextLabel", frame)
    title.Size = UDim2.new(1, -20, 1, -10)
    title.Position = UDim2.new(0, 10, 0, 5)
    title.BackgroundTransparency = 1
    title.Text = "@" .. playerName .. " saiu do jogo"
    title.TextColor3 = Color3.fromRGB(255, 120, 120)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 14
    title.TextXAlignment = Enum.TextXAlignment.Left

    local TweenService = game:GetService("TweenService")
    local enterTween = TweenService:Create(frame, TweenInfo.new(0.4, Enum.EasingStyle.Quart), {
        Position = UDim2.new(1, -10, 0, 10)
    })
    enterTween:Play()

    task.delay(3, function()
        local exitTween = TweenService:Create(frame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Position = UDim2.new(1, 0, 0, -60)
        })
        exitTween:Play()
        exitTween.Completed:Wait()
        frame:Destroy()
    end)
end

-- Toggle View com notificação e auto-unview
Tab3:AddToggle({
    Name = "Visualizar  Jogador",
    Callback = function(Value)
        viewing = Value
        if viewing then
            task.spawn(function()
                local shown = false
                while viewing do
                    local target = game.Players:FindFirstChild(selectedPlayer)
                    if target then
                        if not shown then
                            ShowPlayerNotification(target)
                            shown = true
                        end
                        local character = target.Character or target.CharacterAdded:Wait()
                        local humanoid = character:FindFirstChild("Humanoid")
                        if humanoid then
                            cam.CameraSubject = humanoid
                        end
                    else
                        -- Jogador saiu
                        ShowLeaveNotification(selectedPlayer)
                        viewing = false
                        local myChar = player.Character
                        if myChar and myChar:FindFirstChild("Humanoid") then
                            cam.CameraSubject = myChar.Humanoid
                        end
                        break
                    end
                    task.wait(0.1)
                end
            end)
        else
            local myChar = player.Character
            if myChar and myChar:FindFirstChild("Humanoid") then
                cam.CameraSubject = myChar.Humanoid
            end
        end
    end
})

Tab3:AddToggle({
    Name = "Head Sit (Cavalinho)",
    Default = false,
    Callback = function(bool)
        local Players = game:GetService("Players")
        local RunService = game:GetService("RunService")

        local player = Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        local humanoid = character:WaitForChild("Humanoid")

        -- usa o selectedPlayer do outro script
        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            return false
        end

        local targetPlayer = Players:FindFirstChild(selectedPlayer)

        if bool then
            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("Head") then
                humanoid.Sit = true

                -- ZERA VELOCIDADE ANTES (anti fling preventivo)
                humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
                humanoidRootPart.AssemblyAngularVelocity = Vector3.zero

                if headSitConnection then
                    headSitConnection:Disconnect()
                end

                headSitConnection = RunService.Heartbeat:Connect(function()
                    if targetPlayer.Character
                        and targetPlayer.Character:FindFirstChild("Head")
                        and humanoid.Sit then

                        local head = targetPlayer.Character.Head
                        humanoidRootPart.CFrame =
                            head.CFrame * CFrame.new(0, 1.6, 0.4)

                        -- mantém zerado durante o loop (anti fling total)
                        humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
                        humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
                    else
                        if headSitConnection then
                            headSitConnection:Disconnect()
                            headSitConnection = nil
                        end
                        humanoid.Sit = false
                    end
                end)
            else
                warn("Player alvo inválido ou sem character!")
                return false
            end
        else
            -- DESLIGANDO HEAD SIT
            if headSitConnection then
                headSitConnection:Disconnect()
                headSitConnection = nil
            end

            humanoid.Sit = false

            -- ANTI FLING DEFINITIVO
            humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
            humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
        end
    end
})

Tab3:AddToggle({
    Name = "Loop TP  Jogador",
    Callback = function(Value)
        loopTP = Value
        if loopTP then
            task.spawn(function()
                while loopTP do
                    local target = game.Players:FindFirstChild(selectedPlayer)
                    if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                        local myChar = player.Character
                        if myChar and myChar:FindFirstChild("HumanoidRootPart") then
                            -- Teleporta exatamente para a posiÃƒÂ§ÃƒÂ£o do HumanoidRootPart do alvo
                            myChar.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame
                        end
                    end
                    task.wait(0.02)
                end
            end)
        end
    end
})

Tab3:AddButton({
    Name = "Tp Jogador",
    Callback = function ()
    
        local Players = game:GetService("Players")
        local Workspace = game:GetService("Workspace")
        local LocalPlayer = Players.LocalPlayer
        local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
        local HRP = Character:FindFirstChild("HumanoidRootPart")

        if not selectedPlayer then
            warn("Nenhum jogador selecionado.")
            return
        end

        local target = Players:FindFirstChild(selectedPlayer)
        if not target or not target.Character or not target.Character:FindFirstChild("HumanoidRootPart") then
            warn("User no Found")
            return
        end

        local targetHRP = target.Character:FindFirstChild("HumanoidRootPart")
        HRP.CFrame = targetHRP.CFrame + Vector3.new(0, 3, 0) -- TP acima do player
    end
})

    










-----------kills

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualInputManager = game:GetService("VirtualInputManager")
local RunService = game:GetService("RunService")
local cam = workspace.CurrentCamera


local selectedPlayerName = nil
local methodKill = nil
getgenv().Target = nil
local Character = LocalPlayer.Character
local Humanoid = Character and Character:WaitForChild("Humanoid")
local RootPart = Character and Character:WaitForChild("HumanoidRootPart")

-- Função para limpar o sofá (couch)
local function cleanupCouch()
    local char = LocalPlayer.Character
    if char then
        local couch = char:FindFirstChild("Chaos.Couch") or LocalPlayer.Backpack:FindFirstChild("Chaos.Couch")
        if couch then
            couch:Destroy()
        end
    end
    -- Limpar ferramentas via remoto
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
end

-- Conectar evento CharacterAdded
LocalPlayer.CharacterAdded:Connect(function(newCharacter)
    Character = newCharacter
    Humanoid = newCharacter:WaitForChild("Humanoid")
    RootPart = newCharacter:WaitForChild("HumanoidRootPart")
    cleanupCouch()
    
    -- Conectar evento Died para o novo Humanoid
    Humanoid.Died:Connect(function()
        cleanupCouch()
    end)
end)

-- Conectar evento Died para o Humanoid inicial, se existir
if Humanoid then
    Humanoid.Died:Connect(function()
        cleanupCouch()
    end)
end

-- Função KillPlayerCouch
local function KillPlayerCouch()
    if not selectedPlayerName then
        warn("Erro: Nenhum jogador selecionado")
        return
    end
    local target = Players:FindFirstChild(selectedPlayerName)
    if not target or not target.Character then
        warn("Erro: Jogador alvo não encontrado ou sem personagem")
        return
    end

    local char = LocalPlayer.Character
    if not char then
        warn("Erro: Personagem do jogador local não encontrado")
        return
    end
    local hum = char:FindFirstChildOfClass("Humanoid")
    local root = char:FindFirstChild("HumanoidRootPart")
    local tRoot = target.Character and target.Character:FindFirstChild("HumanoidRootPart")
    if not hum or not root or not tRoot then
        warn("Erro: Componentes necessários não encontrados")
        return
    end

    local originalPos = root.Position 
    local sitPos = Vector3.new(145.51, -350.09, 21.58)

    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
    task.wait(0.2)

    ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "Couch")
    task.wait(0.3)

    local tool = LocalPlayer.Backpack:FindFirstChild("Couch")
    if tool then tool.Parent = char end
    task.wait(0.1)

    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.F, false, game)
    task.wait(0.1)

    hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
    hum.PlatformStand = false
    cam.CameraSubject = target.Character:FindFirstChild("Head") or tRoot or hum

    local align = Instance.new("BodyPosition")
    align.Name = "BringPosition"
    align.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    align.D = 10
    align.P = 30000
    align.Position = root.Position
    align.Parent = tRoot

    task.spawn(function()
        local angle = 0
        local startTime = tick()
        while tick() - startTime < 5 and target and target.Character and target.Character:FindFirstChildOfClass("Humanoid") do
            local tHum = target.Character:FindFirstChildOfClass("Humanoid")
            if not tHum or tHum.Sit then break end

            local hrp = target.Character.HumanoidRootPart
            local adjustedPos = hrp.Position + (hrp.Velocity / 1.5)

            angle += 50
            root.CFrame = CFrame.new(adjustedPos + Vector3.new(0, 2, 0)) * CFrame.Angles(math.rad(angle), 0, 0)
            align.Position = root.Position + Vector3.new(2, 0, 0)

            task.wait()
        end

        align:Destroy()
        hum:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
        hum.PlatformStand = false
        cam.CameraSubject = hum

        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then
                p.Velocity = Vector3.zero
                p.RotVelocity = Vector3.zero
            end
        end

        task.wait(0.1)
        root.CFrame = CFrame.new(sitPos)
        task.wait(0.3)

        local tool = char:FindFirstChild("Couch")
        if tool then tool.Parent = LocalPlayer.Backpack end

        task.wait(0.01)
        ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "Couch")
        task.wait(0.2)
        root.CFrame = CFrame.new(originalPos)
    end)
end

-- Função BringPlayerLLL
local function BringPlayerLLL()
    if not selectedPlayerName then
        warn("Erro: Nenhum jogador selecionado")
        return
    end
    local target = Players:FindFirstChild(selectedPlayerName)
    if not target or not target.Character then
        warn("Erro: Jogador alvo não encontrado ou sem personagem")
        return
    end

    local char = LocalPlayer.Character
    if not char then
        warn("Erro: Personagem do jogador local não encontrado")
        return
    end
    local hum = char:FindFirstChildOfClass("Humanoid")
    local root = char:FindFirstChild("HumanoidRootPart")
    local tRoot = target.Character and target.Character:FindFirstChild("HumanoidRootPart")
    if not hum or not root or not tRoot then
        warn("Erro: Componentes necessários não encontrados")
        return
    end

    local originalPos = root.Position 
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
    task.wait(0.2)

    ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "Couch")
    task.wait(0.3)

    local tool = LocalPlayer.Backpack:FindFirstChild("Couch")
    if tool then
        tool.Parent = char
    end
    task.wait(0.1)

    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.F, false, game)
    task.wait(0.1)

    hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
    hum.PlatformStand = false
    cam.CameraSubject = target.Character:FindFirstChild("Head") or tRoot or hum

    local align = Instance.new("BodyPosition")
    align.Name = "BringPosition"
    align.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    align.D = 10
    align.P = 30000
    align.Position = root.Position
    align.Parent = tRoot

    task.spawn(function()
        local angle = 0
        local startTime = tick()
        while tick() - startTime < 5 and target and target.Character and target.Character:FindFirstChildOfClass("Humanoid") do
            local tHum = target.Character:FindFirstChildOfClass("Humanoid")
            if not tHum or tHum.Sit then break end

            local hrp = target.Character.HumanoidRootPart
            local adjustedPos = hrp.Position + (hrp.Velocity / 1.5)

            angle += 50
            root.CFrame = CFrame.new(adjustedPos + Vector3.new(0, 2, 0)) * CFrame.Angles(math.rad(angle), 0, 0)
            align.Position = root.Position + Vector3.new(2, 0, 0)

            task.wait()
        end

        align:Destroy()
        hum:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
        hum.PlatformStand = false
        cam.CameraSubject = hum

        for _, p in pairs(char:GetDescendants()) do
            if p:IsA("BasePart") then
                p.Velocity = Vector3.zero
                p.RotVelocity = Vector3.zero
            end
        end

        task.wait(0.1)
        root.Anchored = true
        root.CFrame = CFrame.new(originalPos)
        task.wait(0.001)
        root.Anchored = false

        task.wait(0.7)
        local tool = char:FindFirstChild("Couch")
        if tool then
            tool.Parent = LocalPlayer.Backpack
        end

        task.wait(0.001)
        ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "Couch")
    end)
end

-- Função BringWithCouch
local function BringWithCouch()
    local targetPlayer = Players:FindFirstChild(getgenv().Target)
    if not targetPlayer then
        warn("Erro: Nenhum jogador alvo selecionado")
        return
    end
    if not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        warn("Erro: Jogador alvo sem personagem ou HumanoidRootPart")
        return
    end

    local args = { [1] = "ClearAllTools" }
    ReplicatedStorage.RE["1Clea1rTool1s"]:FireServer(unpack(args))
    local args = { [1] = "PickingTools", [2] = "Couch" }
    ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

    local couch = LocalPlayer.Backpack:WaitForChild("Couch", 2)
    if not couch then
        warn("Erro: Sofá não encontrado no Backpack")
        return
    end

    couch.Name = "Chaos.Couch"
    local seat1 = couch:FindFirstChild("Seat1")
    local seat2 = couch:FindFirstChild("Seat2")
    local handle = couch:FindFirstChild("Handle")
    if seat1 and seat2 and handle then
        seat1.Disabled = true
        seat2.Disabled = true
        handle.Name = "Handle "
    else
        warn("Erro: Componentes do sofá não encontrados")
        return
    end
    couch.Parent = LocalPlayer.Character

    local tet = Instance.new("BodyVelocity", seat1)
    tet.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    tet.P = 1250
    tet.Velocity = Vector3.new(0, 0, 0)
    tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"

    repeat
        for m = 1, 35 do
            local pos = { x = 0, y = 0, z = 0 }
            local tRoot = targetPlayer.Character and targetPlayer.Character.HumanoidRootPart
            if not tRoot then break end
            pos.x = tRoot.Position.X + (tRoot.Velocity.X / 2)
            pos.y = tRoot.Position.Y + (tRoot.Velocity.Y / 2)
            pos.z = tRoot.Position.Z + (tRoot.Velocity.Z / 2)
            seat1.CFrame = CFrame.new(Vector3.new(pos.x, pos.y, pos.z)) * CFrame.new(-2, 2, 0)
            task.wait()
        end
        tet:Destroy()
        couch.Parent = LocalPlayer.Backpack
        task.wait()
        couch:FindFirstChild("Handle ").Name = "Handle"
        task.wait(0.2)
        couch.Parent = LocalPlayer.Character
        task.wait()
        couch.Parent = LocalPlayer.Backpack
        couch.Handle.Name = "Handle "
        task.wait(0.2)
        couch.Parent = LocalPlayer.Character
        tet = Instance.new("BodyVelocity", seat1)
        tet.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        tet.P = 1250
        tet.Velocity = Vector3.new(0, 0, 0)
        tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"
    until targetPlayer.Character and targetPlayer.Character.Humanoid and targetPlayer.Character.Humanoid.Sit == true
    task.wait()
    tet:Destroy()
    couch.Parent = LocalPlayer.Backpack
    task.wait()
    couch:FindFirstChild("Handle ").Name = "Handle"
    task.wait(0.3)
    couch.Parent = LocalPlayer.Character
    task.wait(0.3)
    couch.Grip = CFrame.new(Vector3.new(0, 0, 0))
    task.wait(0.3)
    ReplicatedStorage.RE["1Clea1rTool1s"]:FireServer("ClearAllTools")
end

-- Função KillWithCouch
local function KillWithCouch()
    local targetPlayer = Players:FindFirstChild(getgenv().Target)
    if not targetPlayer then
        warn("Erro: Nenhum jogador alvo selecionado")
        return
    end
    if not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        warn("Erro: Jogador alvo sem personagem ou HumanoidRootPart")
        return
    end

    local args = { [1] = "ClearAllTools" }
    ReplicatedStorage.RE["1Clea1rTool1s"]:FireServer(unpack(args))
    local args = { [1] = "PickingTools", [2] = "Couch" }
    ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

    local couch = LocalPlayer.Backpack:WaitForChild("Couch", 2)
    if not couch then
        warn("Erro: Sofá não encontrado no Backpack")
        return
    end

    couch.Name = "Chaos.Couch"
    local seat1 = couch:FindFirstChild("Seat1")
    local seat2 = couch:FindFirstChild("Seat2")
    local handle = couch:FindFirstChild("Handle")
    if seat1 and seat2 and handle then
        seat1.Disabled = true
        seat2.Disabled = true
        handle.Name = "Handle "
    else
        warn("Erro: Componentes do sofá não encontrados")
        return
    end
    couch.Parent = LocalPlayer.Character

    local tet = Instance.new("BodyVelocity", seat1)
    tet.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    tet.P = 1250
    tet.Velocity = Vector3.new(0, 0, 0)
    tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"

    repeat
        for m = 1, 35 do
            local pos = { x = 0, y = 0, z = 0 }
            local tRoot = targetPlayer.Character and targetPlayer.Character.HumanoidRootPart
            if not tRoot then break end
            pos.x = tRoot.Position.X + (tRoot.Velocity.X / 2)
            pos.y = tRoot.Position.Y + (tRoot.Velocity.Y / 2)
            pos.z = tRoot.Position.Z + (tRoot.Velocity.Z / 2)
            seat1.CFrame = CFrame.new(Vector3.new(pos.x, pos.y, pos.z)) * CFrame.new(-2, 2, 0)
            task.wait()
        end
        tet:Destroy()
        couch.Parent = LocalPlayer.Backpack
        task.wait()
        couch:FindFirstChild("Handle ").Name = "Handle"
        task.wait(0.2)
        couch.Parent = LocalPlayer.Character
        task.wait()
        couch.Parent = LocalPlayer.Backpack
        couch.Handle.Name = "Handle "
        task.wait(0.2)
        couch.Parent = LocalPlayer.Character
        tet = Instance.new("BodyVelocity", seat1)
        tet.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        tet.P = 1250
        tet.Velocity = Vector3.new(0, 0, 0)
        tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"
    until targetPlayer.Character and targetPlayer.Character.Humanoid and targetPlayer.Character.Humanoid.Sit == true
    task.wait()
    couch.Parent = LocalPlayer.Backpack
    seat1.CFrame = CFrame.new(Vector3.new(9999, -450, 9999))
    seat2.CFrame = CFrame.new(Vector3.new(9999, -450, 9999))
    couch.Parent = LocalPlayer.Character
    task.wait(0.1)
    couch.Parent = LocalPlayer.Backpack
    task.wait(2)
    local bv = seat1:FindFirstChild("#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W")
    if bv then bv:Destroy() end
    ReplicatedStorage.RE["1Clea1rTool1s"]:FireServer("ClearAllTools")
end

local MethodSection = Tab3:AddSection({ Name = "Métodos kill/puxar" })

Tab3:AddDropdown({
        Name = "Selecionar Método para Matar",
        Options = {"Bus", "Couch", "Couch Sem ir até o alvo [BETA]"},
        Default = "",
        Callback = function(value)
            methodKill = value
            print("Método selecionado: " .. tostring(value))
        end
    })



Tab3:AddButton({
        Name = "Puxar Jogador",
        Callback = function()
            if not selectedPlayerName or not Players:FindFirstChild(selectedPlayerName) then
                print("Erro: Player não selecionado ou não existe")
                return
            end
            if methodKill == "Couch" then
                BringPlayerLLL()
            elseif methodKill == "Couch Sem ir até o alvo [BETA]" then
                BringWithCouch()
            else
                -- Método de ônibus
                local character = LocalPlayer.Character
                local humanoidRootPart = character and character:FindFirstChild("HumanoidRootPart")
                if not humanoidRootPart then
                    warn("Erro: HumanoidRootPart do jogador local não encontrado")
                    return
                end

                local originalPosition = humanoidRootPart.CFrame

                local function GetBus()
                    local vehicles = game.Workspace:FindFirstChild("Vehicles")
                    if vehicles then
                        return vehicles:FindFirstChild(LocalPlayer.Name .. "Car")
                    end
                    return nil
                end

                local bus = GetBus()

                if not bus then
                    humanoidRootPart.CFrame = CFrame.new(1118.81, 75.998, -1138.61)
                    task.wait(0.5)
                    local remoteEvent = ReplicatedStorage:FindFirstChild("RE")
                    if remoteEvent and remoteEvent:FindFirstChild("1Ca1r") then
                        remoteEvent["1Ca1r"]:FireServer("PickingCar", "SchoolBus")
                    end
                    task.wait(1)
                    bus = GetBus()
                end

                if bus then
                    local seat = bus:FindFirstChild("Body") and bus.Body:FindFirstChild("VehicleSeat")
                    if seat and character:FindFirstChildOfClass("Humanoid") and not character.Humanoid.Sit then
                        repeat
                            humanoidRootPart.CFrame = seat.CFrame * CFrame.new(0, 2, 0)
                            task.wait()
                        until character.Humanoid.Sit or not bus.Parent
                    end
                end

                local function TrackPlayer()
                    while true do
                        if selectedPlayerName then
                            local targetPlayer = Players:FindFirstChild(selectedPlayerName)
                            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                                local targetHumanoid = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
                                if targetHumanoid and targetHumanoid.Sit then
                                    if character.Humanoid then
                                        bus:SetPrimaryPartCFrame(originalPosition)
                                        task.wait(0.7)
                                        local args = { [1] = "DeleteAllVehicles" }
                                        ReplicatedStorage.RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
                                    end
                                    break
                                else
                                    local targetRoot = targetPlayer.Character.HumanoidRootPart
                                    local time = tick() * 35
                                    local lateralOffset = math.sin(time) * 4
                                    local frontBackOffset = math.cos(time) * 20
                                    bus:SetPrimaryPartCFrame(targetRoot.CFrame * CFrame.new(lateralOffset, 0, frontBackOffset))
                                end
                            end
                        end
                        RunService.RenderStepped:Wait()
                    end
                end

                spawn(TrackPlayer)
            end
        end
    })



Tab3:AddButton({
        Name = "Matar Player",
        Callback = function()
            if not selectedPlayerName or not Players:FindFirstChild(selectedPlayerName) then
                print("Erro: Player não selecionado ou não existe")
                return
            end
            if methodKill == "Couch" then
                KillPlayerCouch()
            elseif methodKill == "Couch Sem ir até o alvo [BETA]" then
                KillWithCouch()
            else
                -- Método de ônibus
                local character = LocalPlayer.Character
                local humanoidRootPart = character and character:FindFirstChild("HumanoidRootPart")
                if not humanoidRootPart then
                    warn("Erro: HumanoidRootPart do jogador local não encontrado")
                    return
                end

                local originalPosition = humanoidRootPart.CFrame

                local function GetBus()
                    local vehicles = game.Workspace:FindFirstChild("Vehicles")
                    if vehicles then
                        return vehicles:FindFirstChild(LocalPlayer.Name .. "Car")
                    end
                    return nil
                end

                local bus = GetBus()

                if not bus then
                    humanoidRootPart.CFrame = CFrame.new(1118.81, 75.998, -1138.61)
                    task.wait(0.5)
                    local remoteEvent = ReplicatedStorage:FindFirstChild("RE")
                    if remoteEvent and remoteEvent:FindFirstChild("1Ca1r") then
                        remoteEvent["1Ca1r"]:FireServer("PickingCar", "SchoolBus")
                    end
                    task.wait(1)
                    bus = GetBus()
                end

                if bus then
                    local seat = bus:FindFirstChild("Body") and bus.Body:FindFirstChild("VehicleSeat")
                    if seat and character:FindFirstChildOfClass("Humanoid") and not character.Humanoid.Sit then
                        repeat
                            humanoidRootPart.CFrame = seat.CFrame * CFrame.new(0, 2, 0)
                            task.wait()
                        until character.Humanoid.Sit or not bus.Parent
                        if character.Humanoid.Sit or not bus.Parent then
                            for k, v in pairs(bus.Body:GetChildren()) do
                                if v:IsA("Seat") then
                                    v.CanTouch = false
                                end
                            end
                        end
                    end
                end

                local function TrackPlayer()
                    while true do
                        if selectedPlayerName then
                            local targetPlayer = Players:FindFirstChild(selectedPlayerName)
                            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                                local targetHumanoid = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
                                if targetHumanoid and targetHumanoid.Sit then
                                    if character.Humanoid then
                                        bus:SetPrimaryPartCFrame(CFrame.new(Vector3.new(9999, -450, 9999)))
                                        print("Jogador sentou, levando ônibus para o void!")
                                        task.wait(0.2)

                                        local function simulateJump()
                                            local humanoid = character and character:FindFirstChildWhichIsA("Humanoid")
                                            if humanoid then
                                                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                                            end
                                        end

                                        simulateJump()
                                        print("Simulando pulo!")
                                        task.wait(0.5)
                                        humanoidRootPart.CFrame = originalPosition
                                        print("Player voltou para a posição inicial.")
                                    end
                                    break
                                else
                                    local targetRoot = targetPlayer.Character.HumanoidRootPart
                                    local time = tick() * 35
                                    local lateralOffset = math.sin(time) * 4
                                    local frontBackOffset = math.cos(time) * 20
                                    bus:SetPrimaryPartCFrame(targetRoot.CFrame * CFrame.new(lateralOffset, 0, frontBackOffset))
                                end
                            end
                        end
                        RunService.RenderStepped:Wait()
                    end
                end

                spawn(TrackPlayer)
            end
        end
    })


    -- 🛠️ SINCRONIZADOR FORÇADO (COLA NO FINAL)
task.spawn(function()
    while task.wait(0.1) do
        -- Se o dropdown definiu um player, nós espelhamos para as outras variáveis
        if selectedPlayer ~= nil then
            _G.selectedPlayerName = selectedPlayer
            _G.Target = selectedPlayer
            
            -- Tenta atualizar também as locais se elas existirem no ambiente
            selectedPlayerName = selectedPlayer
            getgenv().Target = selectedPlayer
        end
        
        -- Se o dropdown foi limpo (player saiu), limpamos o resto
        if selectedPlayer == nil then
            selectedPlayerName = nil
            _G.selectedPlayerName = nil
            getgenv().Target = nil
        end
    end
end)

local MethodSection = Tab3:AddSection({ Name = "Métodos flings" })

-- 🎛 Aba de Flings
local FlingTab = Tab3 -- ou Window:MakeTab({Name = "| Flings"}) se ainda não existir

-- 🔹 Lista de métodos de Fling
local FlingMethods = {
    "fling Croch",
    "Fling Ball",
    "Fling Canoe",
    "fling - Boat",
    "fling V2 - boat"
}

local SelectedFling = nil

-- 📥 Dropdown de seleção de Fling
local DropdownFling = FlingTab:AddDropdown({
    Name = "Selecionar Fling",
    Options = FlingMethods,
    Default = nil,
    Callback = function(Value)
        SelectedFling = Value
        print("Fling selecionado: "..tostring(SelectedFling))
        CreateNotification("Notificação", "Fling selecionado: "..Value, 3)
    end
})

-- 🔹 Botão de ativar o Fling selecionado
FlingTab:AddButton({
    Name = "Ativar Fling",
    Description = "Executa o Fling selecionado no jogador escolhido",
    Callback = function()
        if not SelectedFling then
            warn("Nenhum fling selecionado!")
            CreateNotification("Notificação", "Escolha um método de Fling antes!", 3)
            return
        end

        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            CreateNotification("Notificação", "Escolha um jogador antes!", 3)
            return
        end

        -- 🔹 Executa o fling correspondente
        if SelectedFling == "fling Croch" then
            -- Código do fling Croch
            -- (colocar aqui exatamente o código que você me mandou para fling Croch)
            local Players = game:GetService("Players")
		local LocalPlayer = Players.LocalPlayer
		local cam = workspace.CurrentCamera
		if not selectedPlayer then return end

		local target = Players:FindFirstChild(selectedPlayer)
		if not target or not target.Character then return end

		local char = LocalPlayer.Character
		local root = char and char:FindFirstChild("HumanoidRootPart")
		local tRoot = target.Character:FindFirstChild("HumanoidRootPart")
		local tHum = target.Character:FindFirstChildOfClass("Humanoid")
		local hum = char and char:FindFirstChildOfClass("Humanoid")
		if not (root and tRoot and tHum and hum) then return end

		local args = { [1] = "ClearAllTools" }
		game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer(unpack(args))
		task.wait(0.3)
		game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools","Couch")

		local original = root.CFrame
		local tool = LocalPlayer.Backpack:FindFirstChildOfClass("Tool")
		if tool then tool.Parent = char end

		workspace.FallenPartsDestroyHeight = -math.huge

		local bv = Instance.new("BodyVelocity")
		bv.Name = "FlingForce"
		bv.Velocity = Vector3.new(9e8,9e8,9e8)
		bv.MaxForce = Vector3.new(math.huge,math.huge,math.huge)
		bv.Parent = root

		hum:SetStateEnabled(Enum.HumanoidStateType.Seated,false)
		hum.PlatformStand = false
		cam.CameraSubject = tRoot

		local angle = 0
		local t = tick()
		while tick() - t < 3 and target and target.Character and target.Character:FindFirstChildOfClass("Humanoid") do
			tHum = target.Character:FindFirstChildOfClass("Humanoid")
			tRoot = target.Character:FindFirstChild("HumanoidRootPart")
			if not tRoot then break end
			angle += 30
			root.CFrame = CFrame.new(tRoot.Position + Vector3.new(0, 1, 0)) * CFrame.Angles(math.rad(angle), 0, 0)
			root.Velocity = Vector3.new(9e8,9e8,9e8)
			root.RotVelocity = Vector3.new(9e8,9e8,9e8)
			task.wait()
		end

		bv:Destroy()
		hum:SetStateEnabled(Enum.HumanoidStateType.Seated,true)
		hum.PlatformStand = false
		root.CFrame = original
		cam.CameraSubject = hum
		for _, p in pairs(char:GetDescendants()) do
			if p:IsA("BasePart") then
				p.Velocity = Vector3.zero
				p.RotVelocity = Vector3.zero
			end
		end
		hum:UnequipTools()
		game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools","Couch")
        elseif SelectedFling == "Fling Ball" then
            -- Código do Fling Ball
            -- (usar exatamente o código do Fling Ball)
            local Players = game:GetService("Players")
        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local Workspace = game:GetService("Workspace")

        local player = Players.LocalPlayer
        local targetPlayer = Players:FindFirstChild(selectedPlayer)
        print("FOUND your USER:", selectedPlayer)

        if not targetPlayer or not targetPlayer.Character then
            warn("Jogador alvo invÃƒÂ¡lido.")
            return
        end

        local character = player.Character or player.CharacterAdded:Wait()
        local backpack = player:WaitForChild("Backpack")
        local ServerBalls = Workspace:WaitForChild("WorkspaceCom"):WaitForChild("001_SoccerBalls")

        -- Solicita e equipa a bola
        if not backpack:FindFirstChild("SoccerBall") and not character:FindFirstChild("SoccerBall") then
            ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "SoccerBall")
        end

        repeat task.wait() until backpack:FindFirstChild("SoccerBall") or character:FindFirstChild("SoccerBall")

        local ballTool = backpack:FindFirstChild("SoccerBall")
        if ballTool then
            ballTool.Parent = character
        end

        repeat task.wait() until ServerBalls:FindFirstChild("Soccer" .. player.Name)
        local Ball = ServerBalls:FindFirstChild("Soccer" .. player.Name)

        Ball.CanCollide = false
        Ball.Massless = true
        Ball.CustomPhysicalProperties = PhysicalProperties.new(0.0001, 0, 0)

        -- Aplicar o fling
        local tchar = targetPlayer.Character
        local troot = tchar and tchar:FindFirstChild("HumanoidRootPart")
        local thum = tchar and tchar:FindFirstChild("Humanoid")
        if not troot or not thum then return end

        if Ball:FindFirstChildWhichIsA("BodyVelocity") then
            Ball:FindFirstChildWhichIsA("BodyVelocity"):Destroy()
        end

        local bv = Instance.new("BodyVelocity")
        bv.Name = "FlingPower"
        bv.Velocity = Vector3.new(9e8, 9e8, 9e8)
        bv.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        bv.P = 9e900
        bv.Parent = Ball

        -- loop a colar no alvo
        task.spawn(function()
            repeat
                if troot.Velocity.Magnitude > 0 then
                    local pos = troot.Position + (troot.Velocity / 1.5)
                    Ball.CFrame = CFrame.new(pos)
                    Ball.Orientation += Vector3.new(45, 60, 30)
                else
                    for _, v in pairs(tchar:GetChildren()) do
                        if v:IsA("BasePart") and v.CanCollide and not v.Anchored then
                            Ball.CFrame = v.CFrame
                            task.wait(1/6000)
                        end
                    end
                end
                task.wait(1/6000)
            until troot.Velocity.Magnitude > 1000 or thum.Health <= 0 or not tchar:IsDescendantOf(Workspace) or targetPlayer.Parent ~= Players
        end)
        elseif SelectedFling == "Fling Canoe" then
            -- Código do Fling Canoe
            local nome = selectedPlayer
        if not nome then
            warn("Nenhum jogador definido.")
            return
        end

        local AlvoSelecionado = game.Players:FindFirstChild(nome)
        if not AlvoSelecionado then
            warn("Jogador nÃƒÂ£o encontrado.")
            return
        end

        local player = game.Players.LocalPlayer
        local char = player.Character or player.CharacterAdded:Wait()
        local humanoid = char:WaitForChild("Humanoid")
        local root = char:WaitForChild("HumanoidRootPart")

        if humanoid.Sit then
            humanoid.Sit = false
            task.wait(0.5)
        end

        root.CFrame = workspace.WorkspaceCom["001_CanoeCloneButton"].Button.CFrame
        task.wait(0.4)
        fireclickdetector(workspace.WorkspaceCom["001_CanoeCloneButton"].Button.ClickDetector, 0)
        task.wait(0.4)

        local canoe = workspace.WorkspaceCom["001_CanoeStorage"].Canoe
        local seat = canoe:FindFirstChild("VehicleSeat")

        if not canoe.PrimaryPart then
            canoe.PrimaryPart = seat
        end

        -- Sentar
        local tentativas = 0
        repeat
            char:MoveTo(seat.Position + Vector3.new(0, 3, 0))
            task.wait(0.05)
            seat:Sit(humanoid)
            tentativas += 1
        until humanoid.Sit or tentativas > 100

        if not humanoid.Sit then
            warn("Falhou em sentar no barco.")
            return
        end

        -- Alvo
        local alvoChar = AlvoSelecionado.Character or AlvoSelecionado.CharacterAdded:Wait()
        local alvoRoot = alvoChar:WaitForChild("HumanoidRootPart")
        local alvoHum = alvoChar:WaitForChild("Humanoid")

        local force = Instance.new("BodyForce", canoe.PrimaryPart)
        local angular = Instance.new("BodyAngularVelocity", canoe.PrimaryPart)
        angular.MaxTorque = Vector3.new(1e9, 1e9, 1e9)
        angular.AngularVelocity = Vector3.new(1000, 5000, 1000)
        angular.P = 1e9

        local distancia = 10
        local sentido = 1

        local start = tick()
        while tick() - start < 10 and humanoid.Sit and alvoChar and alvoHum and alvoHum.Health > 0 do
            local offset = alvoRoot.CFrame.LookVector * distancia * sentido
            local pos = alvoRoot.Position + offset
            canoe:SetPrimaryPartCFrame(CFrame.new(pos, alvoRoot.Position))
            sentido = -sentido

            local dir = (alvoRoot.Position - canoe.PrimaryPart.Position).Unit
            force.Force = dir * 1e6 + Vector3.new(0, workspace.Gravity * canoe.PrimaryPart:GetMass(), 0)
            task.wait()
        end

        force:Destroy()
        angular:Destroy()
        elseif SelectedFling == "fling - Boat" then
            -- Código do fling - Boat
            local TargetName = selectedPlayer
        local Player = game.Players.LocalPlayer
        local Character = Player.Character
        local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
        local RootPart = Character and Character:FindFirstChild("HumanoidRootPart")
        local Vehicles = workspace:FindFirstChild("Vehicles")

        if not TargetName or not Humanoid or not RootPart then return end

        local function spawnBoat()
            RootPart.CFrame = CFrame.new(1754, -2, 58)
            task.wait(0.5)
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer("PickingBoat", "MilitaryBoatFree")
            task.wait(1)
            return Vehicles and Vehicles:FindFirstChild(Player.Name.."Car")
        end

        local PCar = Vehicles and Vehicles:FindFirstChild(Player.Name.."Car") or spawnBoat()
        if not PCar then return end

        local Seat = PCar:FindFirstChild("Body") and PCar.Body:FindFirstChild("VehicleSeat")
        if not Seat then return end

        repeat 
            task.wait()
            RootPart.CFrame = Seat.CFrame * CFrame.new(0, math.random(-1, 1), 0)
        until Humanoid.Sit

        local SpinGyro = Instance.new("BodyGyro")
        SpinGyro.Parent = PCar.PrimaryPart
        SpinGyro.MaxTorque = Vector3.new(1e7, 1e7, 1e7)
        SpinGyro.P = 1e7
        SpinGyro.CFrame = PCar.PrimaryPart.CFrame * CFrame.Angles(0, math.rad(90), 0)

        workspace.Gravity = 0.1

        local TargetPlayer = game.Players:FindFirstChild(TargetName)
        if not TargetPlayer or not TargetPlayer.Character then return end

        local TargetC = TargetPlayer.Character
        local TargetH = TargetC:FindFirstChildOfClass("Humanoid")
        local TargetRP = TargetC:FindFirstChild("HumanoidRootPart")

        if not TargetRP or not TargetH then return end

        local function flingTarget()
            local vel = TargetRP.Velocity.Magnitude
            local dir = TargetH.MoveDirection

            local function kill(alvo, pos)
                if PCar and PCar.PrimaryPart then
                    PCar:SetPrimaryPartCFrame(CFrame.new(alvo.Position) * pos)
                end
            end

            kill(TargetRP, CFrame.new(0, 3, 0) + dir * vel / 1.05)
            kill(TargetRP, CFrame.new(0, -2.25, 5) + dir * vel / 1.05)
            kill(TargetRP, CFrame.new(0, 2.25, 0.25) + dir * vel / 1.10)
            kill(TargetRP, CFrame.new(-2.25, -1.5, 2.25) + dir * vel / 1.10)
            kill(TargetRP, CFrame.new(0, 1.5, 0) + dir * vel / 1.05)
            kill(TargetRP, CFrame.new(0, -1.5, 0) + dir * vel / 1.05)
        end

        task.spawn(function()
            local teleportCount = 0
            local spawnPos = CFrame.new(1754, 5, 58)

            while teleportCount < 5 do
                task.wait(0.5)
                if not PCar or not PCar.Parent then
                    if SpinGyro then SpinGyro:Destroy() end
                    RootPart.CFrame = spawnPos
                    teleportCount += 1
                    Humanoid.PlatformStand = true
                    task.wait(0.5)
                    SpinGyro = Instance.new("BodyGyro")
                    SpinGyro.Parent = PCar.PrimaryPart
                    SpinGyro.MaxTorque = Vector3.new(1e7, 1e7, 1e7)
                    SpinGyro.P = 1e7
                    SpinGyro.CFrame = PCar.PrimaryPart.CFrame * CFrame.Angles(0, math.rad(90), 0)
                else
                    break
                end
            end

            while true do
                task.wait(0.5)
                if PCar and PCar.Parent then
                    flingTarget()
                else
                    break
                end
            end
        end)

        game:GetService("RunService").Heartbeat:Connect(function()
            if not PCar or not PCar.Parent then
                workspace.Gravity = 196.2
            end
        end)
        elseif SelectedFling == "fling V2 - boat" then
            -- Código do fling V2 - boat
                  if not selectedPlayer or not game.Players:FindFirstChild(selectedPlayer) then
            warn("Nenhum jogador selecionado ou nÃ£o existe")
            return
        end

        local Player = game.Players.LocalPlayer
        local Character = Player.Character
        local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
        local RootPart = Character and Character:FindFirstChild("HumanoidRootPart")
        local Vehicles = game.Workspace:FindFirstChild("Vehicles")

        if not Humanoid or not RootPart then
            warn("Humanoid ou RootPart invÃ¡lido")
            return
        end

        -- FunÃ§Ã£o para spawnar barco
        local function spawnBoat()
            RootPart.CFrame = CFrame.new(1754, -2, 58)
            task.wait(0.5)
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer("PickingBoat", "MilitaryBoatFree")
            task.wait(1)
            return Vehicles:FindFirstChild(Player.Name.."Car")
        end

        local PCar = Vehicles:FindFirstChild(Player.Name.."Car") or spawnBoat()
        if not PCar then
            warn("Falha ao spawnar o barco")
            return
        end

        local Seat = PCar:FindFirstChild("Body") and PCar.Body:FindFirstChild("VehicleSeat")
        if not Seat then
            warn("Assento nÃ£o encontrado")
            return
        end

        -- sentar
        repeat 
            task.wait(0.1)
            RootPart.CFrame = Seat.CFrame * CFrame.new(0, 1, 0)
        until Humanoid.SeatPart == Seat

        print("Barco spawnado!")

        local TargetPlayer = game.Players:FindFirstChild(selectedPlayer)
        if not TargetPlayer or not TargetPlayer.Character then
            warn("Jogador nÃ£o encontrado")
            return
        end

        local TargetC = TargetPlayer.Character
        local TargetH = TargetC:FindFirstChildOfClass("Humanoid")
        local TargetRP = TargetC:FindFirstChild("HumanoidRootPart")

        if not TargetRP or not TargetH then
            warn("Humanoid ou RootPart do alvo nÃ£o encontrado")
            return
        end

        -- spin infinito
        local Spin = Instance.new("BodyAngularVelocity")
        Spin.Name = "Spinning"
        Spin.Parent = PCar.PrimaryPart
        Spin.MaxTorque = Vector3.new(0, math.huge, 0)
        Spin.AngularVelocity = Vector3.new(0, 369, 0) 

        print("Fling ativo!")

        local function moveCar(TargetRP, offset)
            if PCar and PCar.PrimaryPart then
                PCar:SetPrimaryPartCFrame(CFrame.new(TargetRP.Position + offset))
            end
        end

        -- loop de segurar + girar aleatÃ³rio
        task.spawn(function()
            while PCar and PCar.Parent and TargetRP and TargetRP.Parent do
                task.wait(0.01) 
                
                -- seguir sempre 7 studs Ã  frente
                local front = TargetRP.CFrame.LookVector * 2
                moveCar(TargetRP, front + Vector3.new(0, 1.5, 0))

                -- se alvo subir muito (flingado)
                if TargetRP.Position.Y > 7000 then
                    if Spin and Spin.Parent then
                        Spin:Destroy()
                    end
                    PCar:Destroy()
                    print("Fling encerrado - alvo jÃ¡ foi lanÃ§ado!")
                    break
                end

                -- rotaÃ§Ãµes aleatÃ³rias para bagunÃ§ar o alvo
                if PCar and PCar.PrimaryPart then
                    local Rotation = CFrame.Angles(
                        math.rad(math.random(-369, 369)),  
                        math.rad(math.random(-369, 369)), 
                        math.rad(math.random(-369, 369))
                    )
                    PCar:SetPrimaryPartCFrame(CFrame.new(TargetRP.Position + front + Vector3.new(0, 1.5, 0)) * Rotation)
                end
            end
        end)
        else
            warn("Fling não encontrado!")
        end
    end
})

local Tab4= Window:MakeTab({ "| Antis", "shield" })

Tab4:AddToggle({
    Name = "Anti-Sit",
    Description = "Impede o jogador de sentar",
    Default = false,
    Callback = function(state)
        antiSitEnabled = state
        local LocalPlayer = game:GetService("Players").LocalPlayer

        if state then
            local function applyAntiSit(character)
                local humanoid = character:FindFirstChild("Humanoid")
                if humanoid then
                    humanoid.Sit = false
                    humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)
                    if antiSitConnection then
                        antiSitConnection:Disconnect()
                    end
                    antiSitConnection = humanoid.Seated:Connect(function(isSeated)
                        if isSeated then
                            humanoid.Sit = false
                            humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
                        end
                    end)
                end
            end

            if LocalPlayer.Character then
                applyAntiSit(LocalPlayer.Character)
            end

            local characterAddedConnection
            characterAddedConnection = LocalPlayer.CharacterAdded:Connect(function(character)
                if not antiSitEnabled then
                    characterAddedConnection:Disconnect()
                    return
                end
                local humanoid = character:WaitForChild("Humanoid", 5)
                if humanoid then
                    applyAntiSit(character)
                end
            end)
        else
            if antiSitConnection then
                antiSitConnection:Disconnect()
                antiSitConnection = nil
            end

            if LocalPlayer.Character then
                local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
                if humanoid then
                    humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
                end
            end
        end
    end
})

-- Toggle Anti Fling Ball (Noclip apenas para as bolas)
Tab4:AddToggle({
    Name = "Anti Fling Ball",
    Description = "As bolas de futebol não vão mais te empurrar!",
    Default = false,
    Callback = function(state)
        _G.AntiBall = state
        
        local player = game:GetService("Players").LocalPlayer
        
        -- Loop para garantir que as bolas novas e antigas não te toquem
        task.spawn(function()
            while _G.AntiBall do
                -- Procura em todo o Workspace por SoccerBall
                for _, obj in pairs(workspace:GetDescendants()) do
                    if obj:IsA("BasePart") and (obj.Name == "SoccerBall" or obj.Name:find("Soccer")) then
                        -- Desativa a colisão da bola com o seu personagem
                        obj.CanCollide = false
                    end
                end
                task.wait(1) -- Verifica a cada 1 segundo para não dar lag
            end
            
            -- Se desligar o toggle, as bolas voltam ao normal (opcional)
            if not _G.AntiBall then
                for _, obj in pairs(workspace:GetDescendants()) do
                    if obj:IsA("BasePart") and (obj.Name == "SoccerBall" or obj.Name:find("Soccer")) then
                        obj.CanCollide = true
                    end
                end
            end
        end)
    end
})


local RunService = game:GetService("RunService")

local doorParts = {}
local doorConnection

-- identifica se é porta
local function isDoor(part)
    if not part:IsA("BasePart") then return false end
    local name = part.Name:lower()
    return name:find("door") or name:find("porta")
end

-- aplica noclip nas portas
local function applyDoorNoclip(state)
    for _, part in ipairs(workspace:GetDescendants()) do
        if isDoor(part) then
            doorParts[part] = true
            part.CanCollide = not state
        end
    end
end

Tab4:AddToggle({
    Name = "Anti fling portas",
    Description = "As portas não vão mais te empurrar!",
    Default = false,
    Callback = function(Value)

        -- aplica nas portas existentes
        applyDoorNoclip(Value)

        -- auto-update (portas novas)
        if Value then
            doorConnection = workspace.DescendantAdded:Connect(function(obj)
                if isDoor(obj) then
                    doorParts[obj] = true
                    obj.CanCollide = false
                end
            end)
        else
            -- restaura colisão
            for part in pairs(doorParts) do
                if part and part.Parent then
                    part.CanCollide = true
                end
            end
            doorParts = {}

            if doorConnection then
                doorConnection:Disconnect()
                doorConnection = nil
            end
        end
    end
})


-- Variável para guardar o estado
local VoidConnection

local function ToggleVoidProtection(bool)
	if bool then
		game.Workspace.FallenPartsDestroyHeight = 0/0
	else
		game.Workspace.FallenPartsDestroyHeight = -500
	end
end

-- Toggle na RedzLib
Tab4:AddToggle({
	Name = "Anti Void",
	Description = "Não deixar você morrer para o void",
	Default = false,
	Callback = function(Value)
		ToggleVoidProtection(Value)
	end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Avatar---------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab5= Window:MakeTab({ "| Avatar", "shirt" })

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local SelectedPlayerAvatar = nil -- alterado aqui

-- 🔔 SISTEMA DE NOTIFICAÇÃO (HEADER STYLE)
local function CreateNotification(title, message, duration)
    duration = duration or 4

    local playerGui = LocalPlayer:WaitForChild("PlayerGui")

    if playerGui:FindFirstChild("SimpleNotify") then
        playerGui.SimpleNotify:Destroy()
    end

    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "SimpleNotify"
    screenGui.ResetOnSpawn = false
    screenGui.Parent = playerGui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 420, 0, 42)
    frame.Position = UDim2.new(0.5, -210, 0, -50)
    frame.BackgroundColor3 = Color3.fromRGB(27,5, 25, 30)
    frame.BorderSizePixel = 0
    frame.Parent = screenGui

    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 6)

    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -45, 1, 0)
    textLabel.Position = UDim2.new(0, 10, 0, 0)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = string.upper(title)..": "..message
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.SourceSansSemibold
    textLabel.TextSize = 16
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.Parent = frame

    local close = Instance.new("TextButton")
    close.Size = UDim2.new(0, 30, 1, 0)
    close.Position = UDim2.new(1, -30, 0, 0)
    close.BackgroundTransparency = 1
    close.Text = "X"
    close.TextColor3 = Color3.fromRGB(255,255,255)
    close.Font = Enum.Font.SourceSansBold
    close.TextSize = 18
    close.Parent = frame

    TweenService:Create(
        frame,
        TweenInfo.new(0.35, Enum.EasingStyle.Quint, Enum.EasingDirection.Out),
        {Position = UDim2.new(0.5, -210, 0, 5)}
    ):Play()

    local closed = false
    local function Close()
        if closed then return end
        closed = true

        TweenService:Create(
            frame,
            TweenInfo.new(0.25, Enum.EasingStyle.Quint, Enum.EasingDirection.In),
            {Position = UDim2.new(0.5, -210, 0, -50)}
        ):Play()

        task.delay(0.3, function()
            screenGui:Destroy()
        end)
    end

    close.MouseButton1Click:Connect(Close)
    task.delay(duration, Close)
end

local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

local DropdownJogadores = Tab5:AddDropdown({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = nil,
    Callback = function(Value)
        SelectedPlayerAvatar = Value -- alterado aqui
        print("Alvo selecionado: " .. tostring(SelectedPlayerAvatar))
        CreateNotification("Notificação", "Player selecionado: "..Value, 3)
    end
})

local function UpdateDropdown()
    task.wait(0.5)
    if DropdownJogadores then
        local selecionadoAntes = SelectedPlayerAvatar
        local nomesAtualizados = GetPlayerNames()

        if DropdownJogadores.Set then
            DropdownJogadores:Set(nomesAtualizados)
        elseif DropdownJogadores.Refresh then
            DropdownJogadores:Refresh(nomesAtualizados, true)
        end

        if selecionadoAntes then
            local aindaEstaNoJogo = false
            for _, nome in ipairs(nomesAtualizados) do
                if nome == selecionadoAntes then
                    aindaEstaNoJogo = true
                    break
                end
            end

            if aindaEstaNoJogo then
                SelectedPlayerAvatar = selecionadoAntes
                if DropdownJogadores.Set then
                    DropdownJogadores:Set(selecionadoAntes)
                end
            else
                SelectedPlayerAvatar = nil
            end
        end
    end
end

Players.PlayerAdded:Connect(UpdateDropdown)

Players.PlayerRemoving:Connect(function(plr)
    if SelectedPlayerAvatar and plr.Name == SelectedPlayerAvatar then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
    end
    UpdateDropdown()
end)

Tab5:AddButton({
    Name = "Copiar Avatar",
    Callback = function()

        if not SelectedPlayerAvatar then
            warn("Nenhum jogador selecionado")
            return
        end

        local Players = game:GetService("Players")
        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local Remotes = ReplicatedStorage:WaitForChild("Remotes")

        local LP = Players.LocalPlayer
        local LChar = LP.Character or LP.CharacterAdded:Wait()

        local TPlayer = Players:FindFirstChild(SelectedPlayerAvatar)
        if not TPlayer then
            warn("Jogador não encontrado")
            return
        end

        local TChar = TPlayer.Character or TPlayer.CharacterAdded:Wait()
        if not TChar then
            warn("Character do alvo não carregado")
            return
        end

        local LHumanoid = LChar:FindFirstChildOfClass("Humanoid")
        local THumanoid = TChar:FindFirstChildOfClass("Humanoid")

        if not LHumanoid or not THumanoid then
            warn("Humanoid não encontrado")
            return
        end

        -- RESETAR LOCALPLAYER
        local LDesc = LHumanoid:GetAppliedDescription()

        for _, acc in ipairs(LDesc:GetAccessories(true)) do
            if acc.AssetId and tonumber(acc.AssetId) then
                Remotes.Wear:InvokeServer(tonumber(acc.AssetId))
                task.wait(0.2)
            end
        end

        if tonumber(LDesc.Shirt) then
            Remotes.Wear:InvokeServer(tonumber(LDesc.Shirt))
            task.wait(0.2)
        end

        if tonumber(LDesc.Pants) then
            Remotes.Wear:InvokeServer(tonumber(LDesc.Pants))
            task.wait(0.2)
        end

        if tonumber(LDesc.Face) then
            Remotes.Wear:InvokeServer(tonumber(LDesc.Face))
            task.wait(0.2)
        end

        -- COPIAR DO ALVO
        local PDesc = THumanoid:GetAppliedDescription()

        local argsBody = {
            [1] = {
                [1] = PDesc.Torso,
                [2] = PDesc.RightArm,
                [3] = PDesc.LeftArm,
                [4] = PDesc.RightLeg,
                [5] = PDesc.LeftLeg,
                [6] = PDesc.Head
            }
        }

        Remotes.ChangeCharacterBody:InvokeServer(unpack(argsBody))
        task.wait(0.5)

        if tonumber(PDesc.Shirt) then
            Remotes.Wear:InvokeServer(tonumber(PDesc.Shirt))
            task.wait(0.3)
        end

        if tonumber(PDesc.Pants) then
            Remotes.Wear:InvokeServer(tonumber(PDesc.Pants))
            task.wait(0.3)
        end

        if tonumber(PDesc.Face) then
            Remotes.Wear:InvokeServer(tonumber(PDesc.Face))
            task.wait(0.3)
        end

        for _, v in ipairs(PDesc:GetAccessories(true)) do
            if v.AssetId and tonumber(v.AssetId) then
                Remotes.Wear:InvokeServer(tonumber(v.AssetId))
                task.wait(0.3)
            end
        end

        local SkinColor = TChar:FindFirstChild("Body Colors")
        if SkinColor then
            Remotes.ChangeBodyColor:FireServer(tostring(SkinColor.HeadColor))
            task.wait(0.3)
        end

        if tonumber(PDesc.IdleAnimation) then
            Remotes.Wear:InvokeServer(tonumber(PDesc.IdleAnimation))
            task.wait(0.3)
        end

        local Bag = TPlayer:FindFirstChild("PlayersBag")
        if Bag then
            if Bag:FindFirstChild("RPName") and Bag.RPName.Value ~= "" then
                Remotes.RPNameText:FireServer("RolePlayName", Bag.RPName.Value)
                task.wait(0.3)
            end
            if Bag:FindFirstChild("RPBio") and Bag.RPBio.Value ~= "" then
                Remotes.RPNameText:FireServer("RolePlayBio", Bag.RPBio.Value)
                task.wait(0.3)
            end
            if Bag:FindFirstChild("RPNameColor") then
                Remotes.RPNameColor:FireServer("PickingRPNameColor", Bag.RPNameColor.Value)
                task.wait(0.3)
            end
            if Bag:FindFirstChild("RPBioColor") then
                Remotes.RPNameColor:FireServer("PickingRPBioColor", Bag.RPBioColor.Value)
                task.wait(0.3)
            end
        end

        print("Avatar copiado com sucesso de:", SelectedPlayerAvatar)

    end
})

Tab5:AddSection({ "Salva skins" })

-- =========================
-- SKIN MANAGER COMPLETO
-- =========================

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local HttpService = game:GetService("HttpService")

local Remotes = ReplicatedStorage:WaitForChild("Remotes")

local FILE_NAME = "SAGAZxAvataLoad.json"
local Skins = {}

if not isfile(FILE_NAME) then
    writefile(FILE_NAME, "{}")
end

local function LoadFile()
    local success, result = pcall(function()
        return HttpService:JSONDecode(readfile(FILE_NAME))
    end)

    if success and type(result) == "table" then
        Skins = result
    else
        Skins = {}
        writefile(FILE_NAME, "{}")
    end
end

local function SaveFile()
    writefile(FILE_NAME, HttpService:JSONEncode(Skins))
end

LoadFile()

-- =========================
-- PEGAR AVATAR ATUAL
-- =========================

local function GetCurrentAvatarData()

    local LP = Players.LocalPlayer
    local Char = LP.Character or LP.CharacterAdded:Wait()
    local Humanoid = Char:FindFirstChildOfClass("Humanoid")

    if not Humanoid then return nil end

    local Desc = Humanoid:GetAppliedDescription()

    local SkinData = {
        Body = {
            Torso = Desc.Torso,
            RightArm = Desc.RightArm,
            LeftArm = Desc.LeftArm,
            RightLeg = Desc.RightLeg,
            LeftLeg = Desc.LeftLeg,
            Head = Desc.Head
        },

        Clothing = {
            Shirt = Desc.Shirt,
            Pants = Desc.Pants,
            Face = Desc.Face
        },

        Accessories = {},
        Animation = Desc.IdleAnimation
    }

    for _, acc in ipairs(Desc:GetAccessories(true)) do
        if acc.AssetId and tonumber(acc.AssetId) then
            table.insert(SkinData.Accessories, tonumber(acc.AssetId))
        end
    end

    local BodyColor = Char:FindFirstChild("Body Colors")
    if BodyColor then
        SkinData.BodyColor = tostring(BodyColor.HeadColor)
    end

    return SkinData
end

-- =========================
-- APLICAR SKIN (CORRIGIDO)
-- =========================

local function AplicarSkin(data)

    if not data then return end

    local LP = Players.LocalPlayer
    local Char = LP.Character or LP.CharacterAdded:Wait()
    local Humanoid = Char:FindFirstChildOfClass("Humanoid")

    if not Humanoid then 
        warn("Humanoid não encontrado")
        return 
    end

    -- RESETAR ACESSÓRIOS ATUAIS
    local CurrentDesc = Humanoid:GetAppliedDescription()

    for _, acc in ipairs(CurrentDesc:GetAccessories(true)) do
        if acc.AssetId and tonumber(acc.AssetId) then
            Remotes.Wear:InvokeServer(tonumber(acc.AssetId))
            task.wait(0.3)
        end
    end

    task.wait(0.4)

    -- CORPO (FORMATO CORRETO)
    if data.Body then

        local argsBody = {
            [1] = {
                data.Body.Torso,
                data.Body.RightArm,
                data.Body.LeftArm,
                data.Body.RightLeg,
                data.Body.LeftLeg,
                data.Body.Head
            }
        }

        Remotes.ChangeCharacterBody:InvokeServer(unpack(argsBody))
        task.wait(0.6)
    end

    -- ROUPAS
    if data.Clothing then

        if tonumber(data.Clothing.Shirt) then
            Remotes.Wear:InvokeServer(tonumber(data.Clothing.Shirt))
            task.wait(0.3)
        end

        if tonumber(data.Clothing.Pants) then
            Remotes.Wear:InvokeServer(tonumber(data.Clothing.Pants))
            task.wait(0.3)
        end

        if tonumber(data.Clothing.Face) then
            Remotes.Wear:InvokeServer(tonumber(data.Clothing.Face))
            task.wait(0.3)
        end
    end

    -- ACESSÓRIOS
    if data.Accessories then
        for _, id in ipairs(data.Accessories) do
            if tonumber(id) then
                Remotes.Wear:InvokeServer(tonumber(id))
                task.wait(0.3)
            end
        end
    end

    -- COR
    if data.BodyColor then
        Remotes.ChangeBodyColor:FireServer(tostring(data.BodyColor))
        task.wait(0.3)
    end

    -- ANIMAÇÃO
    if tonumber(data.Animation) then
        Remotes.Wear:InvokeServer(tonumber(data.Animation))
    end

    print("Skin aplicada com sucesso!")
end

-- =========================
-- AUXILIARES
-- =========================

local function GetSkinList()
    local list = {}
    for name,_ in pairs(Skins) do
        table.insert(list, name)
    end
    table.sort(list)
    return list
end

local SkinName = ""
local SelectedSkin = nil
local Dropdown

local function RefreshDropdown()
    if not Dropdown then return end

    local novaLista = GetSkinList()

    if Dropdown.Set then
        Dropdown:Set(novaLista)
    elseif Dropdown.Refresh then
        Dropdown:Refresh(novaLista, true)
    end

    SelectedSkin = nil
end

-- =========================
-- UI
-- =========================

Tab5:AddTextBox({
    Name = "Nome da Skin",
    PlaceholderText = "Digite o nome...",
    Callback = function(value)
        SkinName = value
    end
})

Dropdown = Tab5:AddDropdown({
    Name = "Skins Salvas",
    Options = GetSkinList(),
    Callback = function(option)
        SelectedSkin = option
    end
})

-- =========================
-- PEGAR AVATAR DE OUTRO PLAYER
-- =========================

local function GetAvatarDataFromPlayer(targetPlayer)

    if not targetPlayer then return nil end

    local Char = targetPlayer.Character or targetPlayer.CharacterAdded:Wait()
    local Humanoid = Char:FindFirstChildOfClass("Humanoid")
    if not Humanoid then return nil end

    local Desc = Humanoid:GetAppliedDescription()

    local SkinData = {
        Body = {
            Torso = Desc.Torso,
            RightArm = Desc.RightArm,
            LeftArm = Desc.LeftArm,
            RightLeg = Desc.RightLeg,
            LeftLeg = Desc.LeftLeg,
            Head = Desc.Head
        },

        Clothing = {
            Shirt = Desc.Shirt,
            Pants = Desc.Pants,
            Face = Desc.Face
        },

        Accessories = {},
        Animation = Desc.IdleAnimation
    }

    for _, acc in ipairs(Desc:GetAccessories(true)) do
        if acc.AssetId and tonumber(acc.AssetId) then
            table.insert(SkinData.Accessories, tonumber(acc.AssetId))
        end
    end

    local BodyColor = Char:FindFirstChild("Body Colors")
    if BodyColor then
        SkinData.BodyColor = tostring(BodyColor.HeadColor)
    end

    return SkinData
end


-- =========================
-- SALVAR SKIN DO PLAYER SELECIONADO
-- =========================

Tab5:AddButton({
    Name = "Salvar Skin do Player Selecionado",
    Callback = function()
        if not SelectedPlayerAvatar then
            warn("Nenhum player selecionado.")
            return
        end

        local targetPlayer = Players:FindFirstChild(SelectedPlayerAvatar)
        if not targetPlayer then
            warn("Player não encontrado.")
            return
        end

        -- Se PlayerSkinName estiver vazio ou nil, usa o nome do player
        local nomeFinal = (PlayerSkinName and PlayerSkinName:match("%S")) and PlayerSkinName or SelectedPlayerAvatar

        local PlayerData = GetAvatarDataFromPlayer(targetPlayer)
        if not PlayerData then
            warn("Não foi possível capturar a skin.")
            return
        end

        Skins[nomeFinal] = PlayerData
        SaveFile()
        RefreshDropdown()

        CreateNotification("Sucesso", "Skin salva de "..SelectedPlayerAvatar, 3)
        print("Skin salva do player:", nomeFinal)
    end
})

-- =========================
-- SALVAR
-- =========================

Tab5:AddButton({
    Name = "Salvar Skin",
    Callback = function()

        local nomeLimpo = tostring(SkinName):gsub("^%s*(.-)%s*$", "%1")

        if nomeLimpo == "" then
            warn("Digite um nome válido.")
            return
        end

        local CurrentData = GetCurrentAvatarData()
        if not CurrentData then return end

        Skins[nomeLimpo] = CurrentData
        SaveFile()
        RefreshDropdown()

        print("Skin salva:", nomeLimpo)
    end
})



-- =========================
-- CARREGAR
-- =========================

Tab5:AddButton({
    Name = "Carregar Skin",
    Callback = function()
        if SelectedSkin and Skins[SelectedSkin] then
            AplicarSkin(Skins[SelectedSkin])
        else
            warn("Nenhuma skin selecionada.")
        end
    end
})

-- =========================
-- DELETAR
-- =========================

Tab5:AddButton({
    Name = "Deletar Skin",
    Callback = function()
        if SelectedSkin and Skins[SelectedSkin] then
            Skins[SelectedSkin] = nil
            SaveFile()
            SelectedSkin = nil
            RefreshDropdown()
            print("Skin deletada.")
        end
    end
})

Tab5:AddSection({ "FIRE FE COLOR" })

-- Dropdown para escolher a cor do fogo
Tab5:AddDropdown({
    Name = "Fire Colors",
    Description = "Select the <font color='rgb(255, 100, 100)'>Fire Color</font>",
    Options = {"White", "Orange", "Green", "Blue", "Purple", "Black"},
    Default = "White",
    Flag = "fire_color_dropdown",
    Callback = function(Value)
        -- Tabela com as cores e seus respectivos IDs e códigos
        local fireColors = {
            ["White"] = {
                id = "18637074370",
                code = "030FireWhite"
            },
            ["Orange"] = {
                id = "18637025451", 
                code = "031FireOrange"
            },
            ["Green"] = {
                id = "18637078598",
                code = "032FireGreen"
            },
            ["Blue"] = {
                id = "18637076370",
                code = "033FireBlue"
            },
            ["Purple"] = {
                id = "18637070174",
                code = "034FirePurple"
            },
            ["Black"] = {
                id = "18637072603",
                code = "035FireBlack"
            }
        }
        
        -- Armazena globalmente a cor selecionada
        _G.selectedColor = Value
        print("" .. Value)
    end
})

-- Botão para equipar a cor escolhida
Tab5:AddButton({
    Name = "Equip Fire Color",
    Callback = function()
        -- Tabela com as cores e seus respectivos IDs e códigos
        local fireColors = {
            ["White"] = {
                id = "18637074370",
                code = "030FireWhite"
            },
            ["Orange"] = {
                id = "18637025451", 
                code = "031FireOrange"
            },
            ["Green"] = {
                id = "18637078598",
                code = "032FireGreen"
            },
            ["Blue"] = {
                id = "18637076370",
                code = "033FireBlue"
            },
            ["Purple"] = {
                id = "18637070174",
                code = "034FirePurple"
            },
            ["Black"] = {
                id = "18637072603",
                code = "035FireBlack"
            }
        }
        
        local selectedColor = _G.selectedColor or "White"
        
        if selectedColor and fireColors[selectedColor] then
            local colorData = fireColors[selectedColor]
            
            local args = {
                [1] = colorData.id,
                [2] = colorData.code
            }
            
            -- Aplica o emmiter com a cor selecionada
            game:GetService("ReplicatedStorage").Remotes.ApplyEmmiter:InvokeServer(unpack(args))
            
            print("Equipado: " .. selectedColor .. " Fire")
        else
            warn("Erro: Cor não encontrada!")
        end
    end
})


-- Dropdown para escolher a cor do smoke
Tab5:AddDropdown({
    Name = "Smoke Colors",
    Description = "Select the <font color='rgb(150, 150, 150)'>Smoke Color</font>",
    Options = {"White", "Yellow", "Orange", "Green", "Blue", "Purple", "Red", "Black"},
    Default = "White",
    Flag = "smoke_color_dropdown",
    Callback = function(Value)
        -- Tabela com as cores de smoke e seus respectivos IDs e códigos
        local smokeColors = {
            ["White"] = {
                id = "18637791748",
                code = "080SmokeWhite"
            },
            ["Yellow"] = {
                id = "18637800482",
                code = "081SmokeYellow"
            },
            ["Orange"] = {
                id = "18637793920",
                code = "082SmokeOrange"
            },
            ["Green"] = {
                id = "18637789299",
                code = "083SmokeGreen"
            },
            ["Blue"] = {
                id = "18637803021",
                code = "084SmokeBlue"
            },
            ["Purple"] = {
                id = "18637813360",
                code = "085SmokePurple"
            },
            ["Red"] = {
                id = "18637796598",
                code = "086SmokeRed"
            },
            ["Black"] = {
                id = "18637798529",
                code = "087SmokeBlack"
            }
        }
        
        -- Armazena globalmente a cor de smoke selecionada
        _G.selectedSmokeColor = Value
        print("" .. Value)
    end
})

-- Botão para equipar a cor de smoke escolhida
Tab5:AddButton({
    Name = "Equip Smoke Color",
    Callback = function()
        -- Tabela com as cores de smoke e seus respectivos IDs e códigos
        local smokeColors = {
            ["White"] = {
                id = "18637791748",
                code = "080SmokeWhite"
            },
            ["Yellow"] = {
                id = "18637800482",
                code = "081SmokeYellow"
            },
            ["Orange"] = {
                id = "18637793920",
                code = "082SmokeOrange"
            },
            ["Green"] = {
                id = "18637789299",
                code = "083SmokeGreen"
            },
            ["Blue"] = {
                id = "18637803021",
                code = "084SmokeBlue"
            },
            ["Purple"] = {
                id = "18637813360",
                code = "085SmokePurple"
            },
            ["Red"] = {
                id = "18637796598",
                code = "086SmokeRed"
            },
            ["Black"] = {
                id = "18637798529",
                code = "087SmokeBlack"
            }
        }
        
        local selectedSmokeColor = _G.selectedSmokeColor or "White"
        
        if selectedSmokeColor and smokeColors[selectedSmokeColor] then
            local colorData = smokeColors[selectedSmokeColor]
            
            local args = {
                [1] = colorData.id,
                [2] = colorData.code
            }
            
            -- Aplica o emmiter com a cor de smoke selecionada
            game:GetService("ReplicatedStorage").Remotes.ApplyEmmiter:InvokeServer(unpack(args))
            
            print("Equipado: " .. selectedSmokeColor .. " Smoke")
        else
            warn("Erro: Cor de smoke não encontrada!")
        end
    end
})

Tab5:AddSection({ " Animações" })

-- ========= LISTA DE ANIMAÇÕES  INATIVIDADE=========
local Animations = {
	["Comunidade adidas"] = 126354114956642,
	["Adidas Esportiva "] = 18538150608,
	["Glamour da Passarela"] = 101279640971758,
	["Animação Negrito"] = 16744209868,
	["Animação Sem Limites"] = 18755930927,
	["Amazon Unboxed"] = 82219139681769,
	["Popular Malvada"] = 101839542383818,
	["Animação Wicked"] = 82682578794949,
	["Aura Adidas"] = 73137983344853,
    ["Mr. Toilet"] =4418326547 ,
	["R15"] = 4211409027,
	["Ud'zal"] = 3307605825,
	["Borock"] = 3710007708,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Idle",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Inatividade",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES CAMINHAR =========
local Animations = {
	["Comunidade adidas"] = 106810508343012,
	["Adidas Esportiva "] = 18538146480,
	["Glamour da Passarela"] = 103190462987721,
	["Animação Negrito"] = 16744219182,
	["Animação Sem Limites"] = 18755942776,
	["Amazon Unboxed"] = 128339543796138,
	["Popular Malvada"] = 133304526526319,
	["Animação Wicked"] = 94133616443608,
	["Aura Adidas"] = 75183215343859,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Walk",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Caminhar",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES CORRIDA =========
local Animations = {
	["Comunidade adidas"] = 124765145869332,
	["Adidas Esportiva "] = 18538133604,
	["Glamour da Passarela"] = 75036746190467,
	["Animação Negrito"] = 16744214662,
	["Animação Sem Limites"] = 18755933883,
	["Amazon Unboxed"] = 114998633936467,
	["Popular Malvada"] = 136276875045281,
	["Animação Wicked"] = 79789194522561,
	["Aura Adidas"] = 123973978164540,
	["Mr. Toilet"] = 4418324223,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Run",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Corrida",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES PULO =========
local Animations = {
	["Comunidade adidas"] = 115715495289805,
	["Adidas Esportiva "] = 18538153691,
	["Glamour da Passarela"] = 138641066989023,
	["Animação Negrito"] = 16744212581,
	["Animação Sem Limites"] = 18755925411,
	["Amazon Unboxed"] = 110418911914024,
	["Popular Malvada"] = 130373407996664,
	["Animação Wicked"] = 111157411630082,
	["Aura Adidas"] = 129527230938281,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Jump",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Pulo",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES QUEDA =========
local Animations = {
	["Comunidade adidas"] = 93993406355955,
	["Adidas Esportiva "] = 18538164337,
	["Glamour da Passarela"] = 72706690305027,
	["Animação Negrito"] = 16744207822,
	["Animação Sem Limites"] = 18755922352,
	["Amazon Unboxed"] = 125108870423182,
	["Popular Malvada"] = 83937116921114,
	["Animação Wicked"] = 124742764102674,
	["Aura Adidas"] = 99457463463495,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Fall",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Queda",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES NADO =========
local Animations = {
	["Comunidade adidas"] = 106537993816942,
	["Adidas Esportiva "] = 18538158932,
	["Glamour da Passarela"] = 112231179705221,
	["Animação Negrito"] = 16744217055,
	["Animação Sem Limites"] = 18755938274,
	["Amazon Unboxed"] = 137392271797713,
	["Popular Malvada"] = 128475661806875,
	["Animação Wicked"] = 135050138303161,
	["Aura Adidas"] = 119007025452432,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Swim",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Nado",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

-- ========= LISTA DE ANIMAÇÕES ESCALAR =========
local Animations = {
	["Comunidade adidas"] = 123695349157584,
	["Adidas Esportiva "] = 18538170170,
	["Glamour da Passarela"] = 104741822987331,
	["Animação Negrito"] = 16744204409,
	["Animação Sem Limites"] = 18755919175,
	["Amazon Unboxed"] = 117011755848398,
	["Popular Malvada"] = 135810009801094,
	["Animação Wicked"] = 123509187015792,
	["Aura Adidas"] = 140398319728398,
}

local selectedAnimation = nil

-- ========= DROPDOWN =========
Tab5:AddDropdown({
	Name = "Selecionar Climb",
	Options = (function()
		local list = {}
		for name,_ in pairs(Animations) do
			table.insert(list, name)
		end
		return list
	end)(),
	Callback = function(option)
		selectedAnimation = Animations[option]
	end
})

-- ========= BOTÃO EQUIPAR =========
Tab5:AddButton({
	Name = "Equipar Animação de Escalar",
	Callback = function()
		if selectedAnimation then
			game:GetService("ReplicatedStorage")
				:WaitForChild("Remotes")
				:WaitForChild("Wear")
				:InvokeServer(selectedAnimation)
		end
	end
})

Tab5:AddSection({ " Nome e Bio" })

local function getRainbowColor(t)
    return Color3.fromHSV((t % 1), 1, 1)
end

local function fireServer(eventName, args)
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local event = ReplicatedStorage:FindFirstChild("RE") and ReplicatedStorage.RE:FindFirstChild(eventName)
    if event then
        pcall(function()
            event:FireServer(unpack(args))
        end)
    end
end

-- Estados dos toggles
local arcuisBothActive = false
local arcuisBioActive = false
local arcuisNameActive = false

-- Toggle 1: Nome + Bio
Tab5:AddToggle({
    Name = "Arcuis  (Nome + Bio)",
    Description = "Nome e Bio com efeito Arco-Iris automatico",
    Default = false,
    Callback = function(state)
        arcuisBothActive = state
        if state then
            task.spawn(function()
                local time = 0
                while arcuisBothActive and LocalPlayer.Character do
                    local color = getRainbowColor(time)
                    fireServer("1RPNam1eColo1r", { [1] = "PickingRPNameColor", [2] = color })
                    fireServer("1RPNam1eColo1r", { [1] = "PickingRPBioColor", [2] = color })
                    task.wait(0.1)
                    time = time + 0.02
                end
            end)
        end
    end
})

-- Toggle 2: Sua Bio
Tab5:AddToggle({
    Name = "Bio Rainbow  [free vip]",
    Description = "Apenas a Bio com efeito Arco-Ãris",
    Default = false,
    Callback = function(state)
        arcuisBioActive = state
        if state then
            task.spawn(function()
                local time = 0
                while arcuisBioActive and LocalPlayer.Character do
                    local color = getRainbowColor(time)
                    fireServer("1RPNam1eColo1r", { [1] = "PickingRPBioColor", [2] = color })
                    task.wait(0.1)
                    time = time + 0.02
                end
            end)
        end
    end
})

-- Toggle 3: Seu Nome
Tab5:AddToggle({
    Name = "Name Rainbow  [free vip]",
    Description = "Apenas o Nome com efeito Arco-Ãris",
    Default = false,
    Callback = function(state)
        arcuisNameActive = state
        if state then
            task.spawn(function()
                local time = 0
                while arcuisNameActive and LocalPlayer.Character do
                    local color = getRainbowColor(time)
                    fireServer("1RPNam1eColo1r", { [1] = "PickingRPNameColor", [2] = color })
                    task.wait(0.1)
                    time = time + 0.02
                end
            end)
        end
    end
})

local vibrantColors = {
    Color3.new(1, 0, 0),
    Color3.new(0, 1, 0),
    Color3.new(0, 0, 1),
    Color3.new(1, 1, 0),
    Color3.new(1, 0, 1),
    Color3.new(0, 1, 1),
    Color3.new(1, 0.5, 0),
    Color3.new(0.5, 0, 1)
}

local function fireServer(eventName, args)
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local event = ReplicatedStorage:FindFirstChild("RE") and ReplicatedStorage.RE:FindFirstChild(eventName)
    if event then
        pcall(function()
            event:FireServer(unpack(args))
        end)
    end
end

local nameAndBioRGBActive = false
Tab5:AddToggle({
    Name = "Nome e Bio RGB Sincronizado",
    Description = "Ativa cores RGB sincronizadas para Nome e Bio",
    Default = false,
    Callback = function(state)
        nameAndBioRGBActive = state
        if state then
            task.spawn(function()
                while nameAndBioRGBActive and LocalPlayer.Character do
                    local color = vibrantColors[math.random(1, #vibrantColors)]
                    local nameArgs = { [1] = "PickingRPNameColor", [2] = color }
                    local bioArgs = { [1] = "PickingRPBioColor", [2] = color }
                    fireServer("1RPNam1eColo1r", nameArgs)
                    fireServer("1RPNam1eColo1r", bioArgs)
                    task.wait(1)
                end
            end)
        end
    end
})

local nameRGBActive = false
Tab5:AddToggle({
    Name = "Nome RGB",
    Description = "Ativa cores RGB para o Nome",
    Default = false,
    Callback = function(state)
        nameRGBActive = state
        if state then
            task.spawn(function()
                while nameRGBActive and LocalPlayer.Character do
                    local color = vibrantColors[math.random(1, #vibrantColors)]
                    local args = { [1] = "PickingRPNameColor", [2] = color }
                    fireServer("1RPNam1eColo1r", args)
                    task.wait(1)
                end
            end)
        end
    end
})

local bioRGBActive = false
Tab5:AddToggle({
    Name = "Bio RGB",
    Description = "Ativa cores RGB na sua bio",
    Default = false,
    Callback = function(state)
        bioRGBActive = state
        if state then
            task.spawn(function()
                while bioRGBActive and LocalPlayer.Character do
                    local color = vibrantColors[math.random(1, #vibrantColors)]
                    local args = { [1] = "PickingRPBioColor", [2] = color }
                    fireServer("1RPNam1eColo1r", args)
                    task.wait(1)
                end
            end)
        end
    end
})

Tab5:AddSection({Name = "Nome e Bio Animado"})

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Remote = ReplicatedStorage:WaitForChild("RE"):WaitForChild("1RPNam1eTex1t")

local selectedBio = ""
local selectedName = ""

-- TEXTBOX BIO
Tab5:AddTextBox({
    Name = "Bio Text",
    Description = "Digite a Bio",
    PlaceholderText = "Escreva sua bio...",
    Callback = function(Value)
        selectedBio = Value
    end
})

-- TEXTBOX NAME
Tab5:AddTextBox({
    Name = "Name Text",
    Description = "Digite o Nome",
    PlaceholderText = "Escreva o nome...",
    Callback = function(Value)
        selectedName = Value
    end
})

-- Controle dos loops
local bioTypingLoop = false
local bioBackLoop = false
local nameTypingLoop = false
local nameBackLoop = false

-- FUNÇÃO ANIMAÇÃO (controlada por toggle)
local function AnimateLoop(remoteName, getText, reverseFlag, stateRef)
    task.spawn(function()
        while stateRef() do
            local text = getText()
            if text ~= "" then
                local buffer = ""
                for i = 1, #text do
                    if not stateRef() then return end
                    buffer = string.sub(text, 1, i)
                    Remote:FireServer(remoteName, buffer)
                    task.wait(0.1)
                end

                if reverseFlag then
                    for i = #text, 1, -1 do
                        if not stateRef() then return end
                        buffer = string.sub(text, 1, i)
                        Remote:FireServer(remoteName, buffer)
                        task.wait(0.1)
                    end
                end
            else
                task.wait(0.2)
            end
        end
    end)
end

-- TOGGLES BIO
Tab5:AddToggle({
    Name = "Bio [Escrevendo Loop]",
    Default = false,
    Callback = function(state)
        bioTypingLoop = state
        if state then
            AnimateLoop("RolePlayBio", function() return selectedBio end, false, function() return bioTypingLoop end)
        end
    end
})

Tab5:AddToggle({
    Name = "Bio [Vai e Volta Loop]",
    Default = false,
    Callback = function(state)
        bioBackLoop = state
        if state then
            AnimateLoop("RolePlayBio", function() return selectedBio end, true, function() return bioBackLoop end)
        end
    end
})

-- TOGGLES NAME
Tab5:AddToggle({
    Name = "Name [Escrevendo Loop]",
    Default = false,
    Callback = function(state)
        nameTypingLoop = state
        if state then
            AnimateLoop("RolePlayName", function() return selectedName end, false, function() return nameTypingLoop end)
        end
    end
})

Tab5:AddToggle({
    Name = "Name [Vai e Volta Loop]",
    Default = false,
    Callback = function(state)
        nameBackLoop = state
        if state then
            AnimateLoop("RolePlayName", function() return selectedName end, true, function() return nameBackLoop end)
        end
    end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Casas---------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab6= Window:MakeTab({ "| Casas", "home" })

local SelectHouse = nil
local NoclipDoor = nil
local HouseDropdown

local Lots = workspace:WaitForChild("001_Lots")

-- Função para pegar casas
local function getHouseList()
    local Tabela = {}
    for _, House in ipairs(Lots:GetChildren()) do
        if House:IsA("Model") and House.Name ~= "For Sale" then
            table.insert(Tabela, House.Name)
        end
    end
    return Tabela
end

-- Criar dropdown uma única vez
HouseDropdown = Tab6:AddDropdown({
    Name = "Selecione a Casa",
    Options = getHouseList(),
    Default = "...",
    Callback = function(Value)
        SelectHouse = Value
        if NoclipDoor then
            NoclipDoor:Set(false)
        end
        print("Casa selecionada:", Value)
    end
})

-- Função de update
local function UpdateHouseDropdown()
    if HouseDropdown and HouseDropdown.Refresh then
        HouseDropdown:Refresh(getHouseList())
    elseif HouseDropdown and HouseDropdown.Set then
        HouseDropdown:Set(getHouseList())
    end
end

-- AUTO UPDATE 🔁
Lots.ChildAdded:Connect(function()
    task.wait(0.3)
    UpdateHouseDropdown()
end)

Lots.ChildRemoved:Connect(function()
    task.wait(0.3)
    UpdateHouseDropdown()
end)

-- Botão manual (opcional)
Tab6:AddButton({
    Name = "Atualizar Lista de Casas",
    Callback = function()
        UpdateHouseDropdown()
    end
})

-- Botão para teleportar para casa
pcall(function()
    Tab6:AddButton({
        Name = "Teleportar para Casa",
        Callback = function()
            local House = workspace["001_Lots"]:FindFirstChild(tostring(SelectHouse))
            if House and game.Players.LocalPlayer.Character then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(House.WorldPivot.Position)
            else
                print("Casa não encontrada: " .. tostring(SelectHouse))
            end
        end
    })
end)

-- Botão para teleportar para cofre
pcall(function()
    Tab6:AddButton({
        Name = "Teleportar para Cofre",
        Callback = function()
            local House = workspace["001_Lots"]:FindFirstChild(tostring(SelectHouse))
            if House and House:FindFirstChild("HousePickedByPlayer") and game.Players.LocalPlayer.Character then
                local safe = House.HousePickedByPlayer.HouseModel:FindFirstChild("001_Safe")
                if safe then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(safe.WorldPivot.Position)
                else
                    print("Cofre não encontrado na casa: " .. tostring(SelectHouse))
                end
            else
                print("Casa não encontrada: " .. tostring(SelectHouse))
            end
        end
    })
end)


-- Toggle para tocar campainha
pcall(function()
    Tab6:AddToggle({
        Name = "Tocar Campainha loop",
        Description = "Em algumas casas nao fuciona",
        Default = false,
        Callback = function(Value)
            getgenv().ChaosHubAutoSpawnDoorbellValue = Value
            spawn(function()
                while getgenv().ChaosHubAutoSpawnDoorbellValue do
                    local House = workspace["001_Lots"]:FindFirstChild(tostring(SelectHouse))
                    if House and House:FindFirstChild("HousePickedByPlayer") then
                        local doorbell = House.HousePickedByPlayer.HouseModel:FindFirstChild("001_DoorBell")
                        if doorbell and doorbell:FindFirstChild("TouchBell") then
                            pcall(function()
                                fireclickdetector(doorbell.TouchBell.ClickDetector)
                            end)
                        end
                    end
                    task.wait(0.5)
                end
            end)
        end
    })
end)

-- Toggle para bater na porta
pcall(function()
    Tab6:AddToggle({
        Name = "Bater na Porta loop",
        Description = "Em algumas casas nao fuciona",
        Default = false,
        Callback = function(Value)
            getgenv().ChaosHubAutoSpawnDoorValue = Value
            spawn(function()
                while getgenv().ChaosHubAutoSpawnDoorValue do
                    local House = workspace["001_Lots"]:FindFirstChild(tostring(SelectHouse))
                    if House and House:FindFirstChild("HousePickedByPlayer") then
                        local doors = House.HousePickedByPlayer.HouseModel:FindFirstChild("001_HouseDoors")
                        if doors and doors:FindFirstChild("HouseDoorFront") and doors.HouseDoorFront:FindFirstChild("Knock") then
                            pcall(function()
                                fireclickdetector(doors.HouseDoorFront.Knock.TouchBell.ClickDetector)
                            end)
                        end
                    end
                    task.wait(0.5)
                end
            end)
        end
    })
end)

local RunService = game:GetService("RunService")

local doorParts = {}
local doorConnection

-- identifica se é porta
local function isDoor(part)
    if not part:IsA("BasePart") then return false end
    local name = part.Name:lower()
    return name:find("door") or name:find("porta")
end

-- aplica noclip nas portas
local function applyDoorNoclip(state)
    for _, part in ipairs(workspace:GetDescendants()) do
        if isDoor(part) then
            doorParts[part] = true
            part.CanCollide = not state
        end
    end
end

Tab6:AddToggle({
    Name = "Noclip portas",
    Description = "Atravessar todas as portas do mapa",
    Default = false,
    Callback = function(Value)

        -- aplica nas portas existentes
        applyDoorNoclip(Value)

        -- auto-update (portas novas)
        if Value then
            doorConnection = workspace.DescendantAdded:Connect(function(obj)
                if isDoor(obj) then
                    doorParts[obj] = true
                    obj.CanCollide = false
                end
            end)
        else
            -- restaura colisão
            for part in pairs(doorParts) do
                if part and part.Parent then
                    part.CanCollide = true
                end
            end
            doorParts = {}

            if doorConnection then
                doorConnection:Disconnect()
                doorConnection = nil
            end
        end
    end
})

Tab6:AddSection({ "Remover ban" })

Tab6:AddButton({
    Name = "Remover Ban",
    Description = "Remove ban de todas as casas",
    Callback = function()

        for _, obj in ipairs(workspace:GetDescendants()) do
            if obj.Name:match("^BannedBlock") then
                pcall(function()
                    obj:Destroy()
                end)
            end
        end

    end
})

Tab6:AddToggle({
    Name = "Auto Remove Ban",
  Description = "Remove ban automaticamente",
    Default = false,
    Callback = function(Value)
        getgenv().AutoRemoveBan = Value

        while getgenv().AutoRemoveBan and task.wait(1) do
            local rs = game:GetService("ReplicatedStorage")
            
            -- Procurar por qualquer pasta com nome "BannedLot" ou similar (ex: BannedLots, BannedLot1, etc)
            for _, obj in pairs(rs:GetChildren()) do
                if obj:IsA("Folder") and string.lower(obj.Name):match("bannedlot") then
                    obj:Destroy()
                    print("[AutoRemoveBan] Removido: " .. obj.Name)
                end
            end
        end
    end    
})

Tab6:AddSection({ "Teleporta para a casa..." })

-- Lista de casas para teletransporte
local casas = {
    ["Casa 1"] = Vector3.new(260.29, 4.37, 209.32),
    ["Casa 2"] = Vector3.new(234.49, 4.37, 228.00),
    ["Casa 3"] = Vector3.new(262.79, 21.37, 210.84),
    ["Casa 4"] = Vector3.new(229.60, 21.37, 225.40),
    ["Casa 5"] = Vector3.new(173.44, 21.37, 228.11),
    ["Casa 6"] = Vector3.new(-43, 21, -137),
    ["Casa 7"] = Vector3.new(-40, 36, -137),
    ["Casa 11"] = Vector3.new(-21, 40, 436),
    ["Casa 12"] = Vector3.new(155, 37, 433),
    ["Casa 13"] = Vector3.new(255, 35, 431),
    ["Casa 14"] = Vector3.new(254, 38, 394),
    ["Casa 15"] = Vector3.new(148, 39, 387),
    ["Casa 16"] = Vector3.new(-17, 42, 395),
    ["Casa 17"] = Vector3.new(-189, 37, -247),
    ["Casa 18"] = Vector3.new(-354, 37, -244),
    ["Casa 19"] = Vector3.new(-456, 36, -245),
    ["Casa 20"] = Vector3.new(-453, 38, -295),
    ["Casa 21"] = Vector3.new(-356, 38, -294),
    ["Casa 22"] = Vector3.new(-187, 37, -295),
    ["Casa 23"] = Vector3.new(-410, 68, -447),
    ["Casa 24"] = Vector3.new(-348, 69, -496),
    ["Casa 28"] = Vector3.new(-103, 12, 1087),
    ["Casa 29"] = Vector3.new(-730, 6, 808),
    ["Casa 30"] = Vector3.new(-245, 7, 822),
    ["Casa 31"] = Vector3.new(639, 76, -361),
    ["Casa 32"] = Vector3.new(-908, 6, -361),
    ["Casa 33"] = Vector3.new(-111, 70, -417),
    ["Casa 34"] = Vector3.new(230, 38, 569),
    ["Casa 35"] = Vector3.new(-30, 13, 2209),
    ["Casa 36"] = Vector3.new(249, 20, -2295),
    ["Casa 37"] = Vector3.new(-1919, 16, 328),
    ["Casa 38"] = Vector3.new(500, 1, 385),
}

-- Criar lista de nomes de casas ordenada
local casasNomes = {}
for nome, _ in pairs(casas) do
    table.insert(casasNomes, nome)
end

table.sort(casasNomes, function(a, b)
    local numA = tonumber(a:match("%d+")) or 0
    local numB = tonumber(b:match("%d+")) or 0
    return numA < numB
end)

-- Dropdown para teletransporte
pcall(function()
    Tab6:AddDropdown({
        Name = "Teleporta para a casa",
        Options = casasNomes,
        Callback = function(casaSelecionada)
            local player = game.Players.LocalPlayer
            if player and player.Character then
                player.Character.HumanoidRootPart.CFrame = CFrame.new(casas[casaSelecionada])
            end
        end
    })
end)

----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba kid-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

-- Aba Child
local Tab7 = Window:MakeTab({"Criança", "baby"})

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local selectedPlayer = nil  -- substitui Target

-- 🔔 SISTEMA DE NOTIFICAÇÃO (HEADER STYLE)
local function CreateNotification(title, message, duration)
    duration = duration or 4

    local playerGui = LocalPlayer:WaitForChild("PlayerGui")

    if playerGui:FindFirstChild("SimpleNotify") then
        playerGui.SimpleNotify:Destroy()
    end

    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "SimpleNotify"
    screenGui.ResetOnSpawn = false
    screenGui.Parent = playerGui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 420, 0, 42)
    frame.Position = UDim2.new(0.5, -210, 0, -50)
    frame.BackgroundColor3 = Color3.fromRGB(27,5, 25, 30)
    frame.BorderSizePixel = 0
    frame.Parent = screenGui

    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 6)

    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -45, 1, 0)
    textLabel.Position = UDim2.new(0, 10, 0, 0)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = string.upper(title)..": "..message
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.SourceSansSemibold
    textLabel.TextSize = 16
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.Parent = frame

    local close = Instance.new("TextButton")
    close.Size = UDim2.new(0, 30, 1, 0)
    close.Position = UDim2.new(1, -30, 0, 0)
    close.BackgroundTransparency = 1
    close.Text = "X"
    close.TextColor3 = Color3.fromRGB(255,255,255)
    close.Font = Enum.Font.SourceSansBold
    close.TextSize = 18
    close.Parent = frame

    TweenService:Create(
        frame,
        TweenInfo.new(0.35, Enum.EasingStyle.Quint, Enum.EasingDirection.Out),
        {Position = UDim2.new(0.5, -210, 0, 5)}
    ):Play()

    local closed = false
    local function Close()
        if closed then return end
        closed = true

        TweenService:Create(
            frame,
            TweenInfo.new(0.25, Enum.EasingStyle.Quint, Enum.EasingDirection.In),
            {Position = UDim2.new(0.5, -210, 0, -50)}
        ):Play()

        task.delay(0.3, function()
            screenGui:Destroy()
        end)
    end

    close.MouseButton1Click:Connect(Close)
    task.delay(duration, Close)
end

-- 📋 LISTA DE PLAYERS
local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

-- 🎯 DROPDOWN DE TARGET
local DropdownJogadores = Tab7:AddDropdown({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = nil,
    Callback = function(Value)
        selectedPlayer = Value  -- aqui é a mudança principal
        print("Alvo selecionado: " .. tostring(selectedPlayer))

        CreateNotification("Notificação", "Player selecionado: "..Value, 3)
    end
})

-- 🔁 ATUALIZAÇÃO AUTOMÁTICA
local function UpdateDropdown()
    task.wait(0.5)
    if DropdownJogadores then
        local selecionadoAntes = selectedPlayer
        local nomesAtualizados = GetPlayerNames()

        if DropdownJogadores.Set then
            DropdownJogadores:Set(nomesAtualizados)
        elseif DropdownJogadores.Refresh then
            DropdownJogadores:Refresh(nomesAtualizados, true)
        end

        if selecionadoAntes then
            local aindaEstaNoJogo = false
            for _, nome in ipairs(nomesAtualizados) do
                if nome == selecionadoAntes then
                    aindaEstaNoJogo = true
                    break
                end
            end

            if aindaEstaNoJogo then
                selectedPlayer = selecionadoAntes
                if DropdownJogadores.Set then
                    DropdownJogadores:Set(selecionadoAntes)
                end
            else
                selectedPlayer = nil
            end
        end
    end
end

-- PLAYER ENTROU
Players.PlayerAdded:Connect(UpdateDropdown)

-- PLAYER SAIU
Players.PlayerRemoving:Connect(function(plr)
    if selectedPlayer and plr.Name == selectedPlayer then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
    end

    UpdateDropdown()
end)



local viewing = false
local cam = workspace.CurrentCamera
local player = game.Players.LocalPlayer

-- Função de notificação com imagem
local function ShowPlayerNotification(plr)
    local username = plr.Name
    local displayname = plr.DisplayName

    local thumbUrl = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. plr.UserId .. "&width=150&height=150&format=png"

    local playerGui = player:WaitForChild("PlayerGui")
    local screenGui = playerGui:FindFirstChild("AnexedNotificationUI")
    if not screenGui then
        screenGui = Instance.new("ScreenGui")
        screenGui.IgnoreGuiInset = true
        screenGui.Name = "AnexedNotificationUI"
        screenGui.ResetOnSpawn = false
        screenGui.Parent = playerGui
    end

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 60)
    frame.Position = UDim2.new(1, 0, 0, -10)
    frame.AnchorPoint = Vector2.new(1, 0)
    frame.BackgroundTransparency = 1
    frame.BorderSizePixel = 0
    frame.ZIndex = 20
    frame.Parent = screenGui

    local image = Instance.new("ImageLabel", frame)
    image.Size = UDim2.new(0, 40, 0, 40)
    image.Position = UDim2.new(0, 10, 0, 10)
    image.BackgroundTransparency = 1
    image.Image = thumbUrl

    local title = Instance.new("TextLabel", frame)
    title.Size = UDim2.new(1, -60, 0, 20)
    title.Position = UDim2.new(0, 60, 0, 8)
    title.BackgroundTransparency = 1
    title.Text = "Visualizando " .. displayname
    title.TextColor3 = Color3.new(1, 1, 1)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 14
    title.TextXAlignment = Enum.TextXAlignment.Left

    local subtitle = Instance.new("TextLabel", frame)
    subtitle.Size = UDim2.new(1, -60, 0, 18)
    subtitle.Position = UDim2.new(0, 60, 0, 30)
    subtitle.BackgroundTransparency = 1
    subtitle.Text = "@" .. username
    subtitle.TextColor3 = Color3.new(1, 1, 1)
    subtitle.Font = Enum.Font.Gotham
    subtitle.TextSize = 12
    subtitle.TextXAlignment = Enum.TextXAlignment.Left

    local TweenService = game:GetService("TweenService")
    local enterTween = TweenService:Create(frame, TweenInfo.new(0.4, Enum.EasingStyle.Quart), {
        Position = UDim2.new(1, -10, 0, 10)
    })
    enterTween:Play()

    task.delay(3, function()
        local exitTween = TweenService:Create(frame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Position = UDim2.new(1, 0, 0, -60)
        })
        exitTween:Play()
        exitTween.Completed:Wait()
        frame:Destroy()
    end)
end

-- Notificação de saida
local function ShowLeaveNotification(playerName)
    local playerGui = player:WaitForChild("PlayerGui")
    local screenGui = playerGui:FindFirstChild("AnexedNotificationUI")
    if not screenGui then
        screenGui = Instance.new("ScreenGui")
        screenGui.IgnoreGuiInset = true
        screenGui.Name = "AnexedNotificationUI"
        screenGui.ResetOnSpawn = false
        screenGui.Parent = playerGui
    end

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 240, 0, 40)
    frame.Position = UDim2.new(1, 0, 0, -10)
    frame.AnchorPoint = Vector2.new(1, 0)
    frame.BackgroundTransparency = 1
    frame.BorderSizePixel = 0
    frame.ZIndex = 20
    frame.Parent = screenGui

    local title = Instance.new("TextLabel", frame)
    title.Size = UDim2.new(1, -20, 1, -10)
    title.Position = UDim2.new(0, 10, 0, 5)
    title.BackgroundTransparency = 1
    title.Text = "@" .. playerName .. " saiu do jogo"
    title.TextColor3 = Color3.fromRGB(255, 120, 120)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 14
    title.TextXAlignment = Enum.TextXAlignment.Left

    local TweenService = game:GetService("TweenService")
    local enterTween = TweenService:Create(frame, TweenInfo.new(0.4, Enum.EasingStyle.Quart), {
        Position = UDim2.new(1, -10, 0, 10)
    })
    enterTween:Play()

    task.delay(3, function()
        local exitTween = TweenService:Create(frame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Position = UDim2.new(1, 0, 0, -60)
        })
        exitTween:Play()
        exitTween.Completed:Wait()
        frame:Destroy()
    end)
end

-- Toggle View com notificação e auto-unview
Tab7:AddToggle({
    Name = "Visualizar  Jogador",
    Callback = function(Value)
        viewing = Value
        if viewing then
            task.spawn(function()
                local shown = false
                while viewing do
                    local target = game.Players:FindFirstChild(selectedPlayer)
                    if target then
                        if not shown then
                            ShowPlayerNotification(target)
                            shown = true
                        end
                        local character = target.Character or target.CharacterAdded:Wait()
                        local humanoid = character:FindFirstChild("Humanoid")
                        if humanoid then
                            cam.CameraSubject = humanoid
                        end
                    else
                        -- Jogador saiu
                        ShowLeaveNotification(selectedPlayer)
                        viewing = false
                        local myChar = player.Character
                        if myChar and myChar:FindFirstChild("Humanoid") then
                            cam.CameraSubject = myChar.Humanoid
                        end
                        break
                    end
                    task.wait(0.1)
                end
            end)
        else
            local myChar = player.Character
            if myChar and myChar:FindFirstChild("Humanoid") then
                cam.CameraSubject = myChar.Humanoid
            end
        end
    end
})

Tab7:AddButton({
    Name = "Enviar criança",
    Callback = function()
        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            return
        end

        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local playerFolder = workspace:FindFirstChild(LocalPlayer.Name)
        local followCharacter = playerFolder and playerFolder:FindFirstChild("FollowCharacter")

        -- 🔹 Se não tiver criança, spawnar
        if not followCharacter then
            local args = {
                [1] = "CharacterFollowSpawnPlayer",
                [2] = "BabyBoy"
            }

            pcall(function()
                ReplicatedStorage.RE:FindFirstChild("1Bab1yFollo1w"):FireServer(unpack(args))
            end)

            -- 🔥 Esperar a criança realmente spawnar
            local timeout = 3
            local startTime = tick()

            repeat
                task.wait(0.1)
                playerFolder = workspace:FindFirstChild(LocalPlayer.Name)
                followCharacter = playerFolder and playerFolder:FindFirstChild("FollowCharacter")
            until followCharacter or tick() - startTime > timeout

            if not followCharacter then
                warn("Criança não spawnou a tempo.")
                return
            end
        end

        -- 🔹 Ativar colisão
        if playerFolder then
            for _, v in pairs(playerFolder:GetChildren()) do
                if v:IsA("BasePart") then
                    v.CanCollide = true
                end
            end
        end

        local target = selectedPlayer
        local targetFolder = workspace:FindFirstChild(target)

        if targetFolder and followCharacter then
            followCharacter.Parent = targetFolder

            -- Evitar múltiplas conexões
            if rawget(getgenv(), "RunService") then
                getgenv().RunService:Disconnect()
                getgenv().RunService = nil
            end

            getgenv().RunService = game:GetService("RunService").Heartbeat:Connect(function()
                local followCharacterNow = targetFolder:FindFirstChild("FollowCharacter")
                if followCharacterNow 
                    and followCharacterNow:FindFirstChild("Torso")
                    and followCharacterNow.Torso:FindFirstChild("BodyPosition") then

                    local humanoidRootPart = targetFolder:FindFirstChild("HumanoidRootPart")

                    if humanoidRootPart then
                        followCharacterNow.Torso.BodyPosition.Position =
                            humanoidRootPart.Position - (humanoidRootPart.CFrame.LookVector * 3)

                        if followCharacterNow.Torso:FindFirstChild("BodyGyro") then
                            followCharacterNow.Torso.BodyGyro.CFrame = humanoidRootPart.CFrame
                        end
                    end
                end
            end)
        end
    end
})


Tab7:AddButton({
    Name = "Retornar criança",
    Callback = function()
        if rawget(getgenv(), "RunService") then
            getgenv().RunService:Disconnect()
            getgenv().RunService = nil
        end

        local args = { [1] = "DeleteFollowCharacter" }
        local success, err = pcall(function()
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Bab1yFollo1w"):FireServer(unpack(args))
        end)
        if not success then
            warn("Erro ao retornar criança: " .. err)
        end

        local args1 = { [1] = "CharacterFollowSpawnPlayer", [2] = "BabyBoy" }
        success, err = pcall(function()
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Bab1yFollo1w"):FireServer(unpack(args1))
        end)
        if not success then
            warn("Erro ao spawnar criança: " .. err)
        end
    end
})



---------------------------------------------------------------------------------------------------------------------------------
                                          -- === Tab 8: Troll Musica === --
---------------------------------------------------------------------------------------------------------------------------------
local Tab8 = Window:MakeTab({"Musicas", "music"})

local function tocarMusica(id)
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    
    -- Radio (ToolMusicText)
    local argsRadio = {
        [1] = "ToolMusicText",
        [2] = id
    }
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("PlayerToolEvent"):FireServer(unpack(argsRadio))
    
    -- Casa (PickHouseMusicText)
    local argsCasa = {
        [1] = "PickHouseMusicText",
        [2] = id
    }
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Player1sHous1e"):FireServer(unpack(argsCasa))

    -- Carro (PickingCarMusicText)
    local argsCarro = {
        [1] = "PickingCarMusicText",
        [2] = id
    }
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Player1sCa1r"):FireServer(unpack(argsCarro))

    -- Scooter (PickingScooterMusicText)
    local argsScooter = {
        [1] = "PickingScooterMusicText",
        [2] = id
    }
    ReplicatedStorage:WaitForChild("RE"):WaitForChild("1NoMoto1rVehicle1s"):FireServer(unpack(argsScooter))
end

local function isValidMusicId(value)
    return value and value ~= "" and value ~= "Option 1" and not value:match("novas musica adds") and not value:match("musica brasil") and not value:match("musica do meu interece") and not value:match("musica dls por elas") and not value:match("meme abaixo") and not value:match("estourada")
end

Tab8:AddTextBox({
    Name = "ID da musica",
    PlaceholderText = "Digite o ID",
    Callback = function(value)
        if value and value ~= "" then
            tocarMusica(tostring(value))
        end
    end
})

-- Dropdowns para Tab8
local function createMusicDropdown(title, musicOptions, defaultOption)
    local musicNames = {}
    local categoryMap = {}
    for category, sounds in pairs(musicOptions) do
        for _, music in ipairs(sounds) do
            if music.name ~= "" then
                table.insert(musicNames, music.name)
                categoryMap[music.name] = {id = music.id, category = category}
            end
        end
    end

    local function playMusic(soundId)
        tocarMusica(tostring(soundId)) -- Usa a funÃ§Ã£o tocarMusica para tocar em todos os contextos
    end

    Tab8:AddDropdown({
        Name = title,
        Description = "all",
        Default = defaultOption,
        Multi = false,
        Options = musicNames,
        Callback = function(selectedSound)
            if selectedSound and categoryMap[selectedSound] then
                local soundId = categoryMap[selectedSound].id
                if soundId and soundId ~= "" and soundId ~= "4354908569" then
                    playMusic(soundId)
                end
            end
        end
    })
end

-- Dropdown "Forro"
createMusicDropdown("Forro", {
    ["forro"] = {
	    { name = "Forro Ja Cansou", id = 74812784884330},
    	{ name = "Lembro Ate Hoje", id = 71531533552899 },
        {name = "AMIGO", id = "91119180724905"},
        {name = "Amor Verdadeiro", id = "123455164277076"},
        {name = "Deixa Eu Ficar", id = "82929658013383"},
        {name = "MTG ZUM ZUM ", id = "92446612272052"},
        {name = "PASSINHO DO BARÃO", id = "127786586963377"},
        {name = "BOYS DO FORRO", id = "139462268046679"},
		
        {name = "Quem é o louco", id = "106958630419629"},
        {name = "Última chance", id = "84053362849165"},
        {name = "The king", id = "120324849313242"},
        {name = "100% forro vaquejada", id = "92295159623916"},
        {name = "forro ja cansou", id = "74812784884330"},
        {name = "lenbro ate hoje", id = "71531533552899"},
        {name = "forro da rezenha", id = "120973520531216"},
        {name = "forro dudu", id = "74404168179733"},
        {name = "forro sao joao", id = "106364874935196"},
        {name = "forro engrassado paia", id = "76524290482399"},
        
        {name = "Uno zero", id = "112959083808887"},
        {name = "Iate do neymar", id = "135738534706063"},
        {name = "Batidao na aldeia", id = "79953696595578"},
        {name = "", id = ""},
        {name = "", id = ""}
    }
}, "Option 1")

-- Dropdown "Músicas e Memes Aleatórios"
createMusicDropdown("Músicas e Memes Aleatorios", {
    ["Músicas e Memes Aleatorios"] = {
    	{ name = "Want To Love", id = 104846670980072 },
        { name = "Backrooms", id = 120817494107898 },
        {name = "Stray War", id = "120102995443063"},
        {name = "Bring Me To Iife", id = "111417042398302"},
        {name = "n sei...", id = "119589720384457"},
        
        {name = "ANXIETY (Amapiano Re-fix)", id = "101483901475189"}, 
        {name = "Megalovania but its only the melodies", id = "104500091160463"},
        {name = "androphono strikes back", id = "78312089943968"},
        {name = "longe de mais", id = "124478512057763"},
        {name = "CELL!", id = "117634275895085"},
        {name = "SLIP AWAY", id = "126152928520174"},
        {name = "Alone in Motion", id = "122379348696948"},
        {name = "Fade Away", id = "81002139735874"},
        {name = "Wounds & Wishes", id = "109347979566607"},
        {name = "AscensÃ£o do Monarca", id = "101864243033211"},
        {name = "carro do ovo", id = "3148329638"},
        {name = "MIKU MIKU HATSUNE", id = "112783541496955"},
        
        {name = "AirPlane", id = "73197748961359"},
        {name = "Dark Nigth (melodia)", id = "103504594968244"},
        {name = "Countin Stars", id = "118957335322667"},
        {name = "Five Nights", id = "89258052168328"},
        {name = "Forgot", id = "76908132937245"},
        {name = "Let The World Burn", id = "111351357978027"},
        {name = "Mimosa 2000", id = "137329447492960"},
        {name = "SunMoon", id = "91995598699901"},
        {name = "AllNigt", id = "98310334398449"},
        {name = "No More", id = "1846458016"},
    	{ name = "Samba", id = 1836175030 },
    	{ name = "Samba2", id = 1838888602 },
        { name = "Stephen Walking - JC-08", id = 7028970358 },
        { name = "Grant - Color", id = 7023828725 },
        { name = "Conro - All I Want", id = 7023680426 },
        { name = "Grant - Are We Still Young", id = 5410086445 },
        { name = "Stonebank - Fire", id = 7028985831 },
        { name = "Rootkit - Taking Me Higher", id = 5410081542 },
        { name = "Duumu - Forward", id = 5410081471 },
        { name = "Tony Romera - I Can't", id = 5410082805 },
        { name = "Musicas de Piano Acustico", id = 1838457617 },
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""}
    }
}, "Option 1")

-- Dropdown "Funk"
createMusicDropdown("Funk", {
    ["Funk"] = {
	{ name = "Sou Teu Fã", id = 85342086082111 },
    {name = "Mensagem", id = "130637458480604"},
    {name = "Sente o Som DO Tapa", id = "97708834121472"},
    {name = "Toma Jatada", id = "91493452201730"},
    {name = "Onda Que é Bom", id = "134130716324734"},
    {name = "Meia Noite", id = "82117652303865"},
    {name = "Dança do Canguru", id = "86876136192157"},
        {name = "fuga na viatura", id = "131891110268352"},
        {name = "CVRL", id = "124244582950595"},
        {name = "MONTAGEM ARABIANA (Pke Gaz1nh)", id = "78076624091098"},
        {name = "batida Brega Violino (Beat Brega Funk)", id = "99399643204701"},
        {name = "Manda o papo (NGI)", id = "132642647937688"},
        {name = "Viver bem", id = "82805460494325"},
        {name = "Faixa estronda", id = "121187736532042"},
        {name = "Ritmo Pixelado", id = "93928823862203"},
        {name = "Melodia Virtual", id = "139147474886402"},
        {name = "SENTA", id = "124085422276732"},
        {name = "V7", id = "80348640826643"},
        {name = "UIUAH", id = "82894376737849"},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""}
    }
}, "Option 1")

-- Dropdown "Phonk"
createMusicDropdown("Phonk", {
    ["phonk"] = {
        {name = "Amor Sem Final", id = "127038714548359"},
        {name = "Renicht Espectral", id = "119202700760169"},
        {name = "Cutemak Phonk", id = "120871403922972"},
        {name = "Sento e me Acabo", id = "124140125253346"},
		
        {name = "wyles", id = "85385155970460"},
        {name = "phonk kawai", id = "91502410121438"},
        {name = "vem no pocpoc", id = "102333419023382"},
        {name = "tatiu wim", id = "122871512353520"},
        {name = "phonk2", id = "126887144190812"},
        {name = "phonk4", id = "115016589376700"},
        {name = "phonk5", id = "118740708757685"},
        {name = "phonk rajada", id = "105126065014034"},
        {name = "vapo do vapo", id = "106317184644394"},
        {name = "tutatatutata", id = "112068892721408"},
        {name = "phonk slower", id = "122852029094656"},
        {name = "phonk12", id = "84733736048142"},
        {name = "estouradassa1", id = "92175624643620"},
        {name = "eoropa", id = "111346133543699"},
        {name = "atimosphekika", id = "77857496821844"},
        {name = "Catuquanvan", id = "88038595663211"},
        {name = "ILOVE phonksla", id = "82148953715595"},

        {name = " FUTABA", id = "91834632690710"},
        {name = "GOTH FUNK", id = "97662362226511"},
        {name = "SUBURBANA", id = "139825057894568"},
    	{ name = "Slowed Vapo No Vapo", id = 106317184644394 },
    	{ name = "Ultra Slowed", id = 84733736048142 },
    	{ name = "tuber 93", id = 1839246711 },
    	{ name = "Blassed Mane", id = 16831108393 },
    	{ name = "Mtg Balada", id = 83797836818857 },	
        { name = "PASSO BEM SOLTO", id = 119936139925486 },
        { name = "Kerosene Cyristal Castels", id = 17647322226 },
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""},
        {name = "", id = ""}
    }
}, "Option 1")

Tab8:AddButton({
    Name = "Stop",
    Description = "ALL music",
    Callback = function()
        tocarMusica("")
    end
})

---------------------------------------------------------------------------------------------------------------------------------
                                          -- === Tab9 Carros=== --
---------------------------------------------------------------------------------------------------------------------------------

local Tab9= Window:MakeTab({ "| Carros", "car" })

local carSpeed = 25
local turboValue = "25"

Tab9:AddTextBox({
    Name = "Velocidade do carro",
    Description = "Digite a Velocidade",
    PlaceholderText = "Digite o valor da Velocidade...",
    Callback = function(Value)
		carSpeed = tonumber(Value) or carSpeed
    end
})

Tab9:AddTextBox({
    Name = "Definir Turbo",
    Description = "Defina o Turbo",
    PlaceholderText = "Digite o valor do Turbo...",
    Callback = function(Value)
        turboValue = tostring(Value)
    end
})

Tab9:AddButton({
	Name = "Mudar Velocidade e Turbo",
	Callback = function()
			local vehicles = workspace:FindFirstChild("Vehicles")
		local car = vehicles and vehicles:FindFirstChild(LocalPlayer.Name .. "Car")
		local seatsFolder = car and car:FindFirstChild("Seats")
		local seatInSeats = seatsFolder and seatsFolder:FindFirstChild("VehicleSeat")
		if seatInSeats then
			local maxSpeed = seatInSeats:FindFirstChild("MaxSpeed")
			if maxSpeed and maxSpeed:IsA("NumberValue") then
				maxSpeed.Value = carSpeed
			end

			local turbo = seatInSeats:FindFirstChild("Turbo")
			if turbo and turbo:IsA("StringValue") then
				turbo.Value = turboValue
			end
		end

		local bodyFolder = car and car:FindFirstChild("Body")
		local seatInBody = bodyFolder and bodyFolder:FindFirstChild("VehicleSeat")
		if seatInBody then
			local topSpeed = seatInBody:FindFirstChild("TopSpeed")
			if topSpeed and topSpeed:IsA("NumberValue") then
				topSpeed.Value = carSpeed
			end

			local turbo = seatInBody:FindFirstChild("Turbo")
			if turbo and turbo:IsA("StringValue") then
				turbo.Value = turboValue
			end
		end
        
	end
})

Tab9:AddSection({ "Seleciona o Carrosl" })

local function updateVehicleList()
    local novaTabela = {}
    for _, v in pairs(game.Workspace.Vehicles:GetChildren()) do
        table.insert(novaTabela, v.Name)
    end
    return novaTabela
end

local selectedVehicle = nil

local CarrosTT = Tab9:AddDropdown({
    Name = "Selecionar Carro",
    Options = updateVehicleList(),
    Default = nil,
    Callback = function(Value)
        selectedVehicle = Value
    end
})

Tab9:AddButton({
    Name = "Atualiza Lista",
    Callback = function()
        CarrosTT:Set(updateVehicleList())
    end
})

Tab9:AddToggle({
    Name = "Ver Camera do Carro Selecionado",
    Description = "Foca a camera no carro selecionado",
    Default = false,
    Callback = function(state)
        local camera = workspace.CurrentCamera

        if state then
            if not selectedVehicle or selectedVehicle == "" then
                warn("Nenhum carro selecionado!")
                return
            end

            local vehiclesFolder = workspace:FindFirstChild("Vehicles")
            if not vehiclesFolder then
                warn("Pasta Vehicles não encontrada!")
                return
            end

            local vehicle = vehiclesFolder:FindFirstChild(selectedVehicle)
            if not vehicle then
                warn("Carro não encontrado!")
                return
            end

            local vehicleSeat = vehicle:FindFirstChildWhichIsA("VehicleSeat", true)
            if not vehicleSeat then
                warn("VehicleSeat não encontrado!")
                return
            end

            -- Salva estado original
            _G.OriginalCameraSubject = camera.CameraSubject
            _G.OriginalCameraType = camera.CameraType

            -- Ajusta câmera
            camera.CameraSubject = vehicleSeat
            camera.CameraType = Enum.CameraType.Follow

        else
            -- Restaura câmera
            if _G.OriginalCameraSubject then
                camera.CameraSubject = _G.OriginalCameraSubject
                camera.CameraType = _G.OriginalCameraType or Enum.CameraType.Custom

                _G.OriginalCameraSubject = nil
                _G.OriginalCameraType = nil
            end
        end
    end
})

Tab9:AddButton({
    Name = "Teleporta ao asento",
    Callback = function()
        local pl = game.Players.LocalPlayer
        local character = pl.Character or pl.CharacterAdded:Wait()
        local root = character:WaitForChild("HumanoidRootPart")

        if selectedVehicle then
            local vehicle = workspace.Vehicles:FindFirstChild(selectedVehicle)
            if vehicle and vehicle:FindFirstChild("Body") then
                local body = vehicle.Body
                local destino = nil
                if body:FindFirstChild("VehicleSeat") then
                    destino = body.VehicleSeat
                elseif body:FindFirstChild("CarSeatPosition") then
                    destino = body.CarSeatPosition
                elseif body:FindFirstChild("Passenger") then
                    destino = body.Passenger
                end
                if destino and destino:IsA("BasePart") then
                    root.CFrame = destino.CFrame + Vector3.new(0, 3, 0)
                end
            end
        end
    end
})

Tab9:AddToggle({
    Name = "Puxar Carro",
    Default = false,
    Callback = function(Value)
      	if not Value then return end

		local player = game.Players.LocalPlayer
		local char = player.Character or player.CharacterAdded:Wait()
		local hrp = char:FindFirstChild("HumanoidRootPart")
		if not hrp then return end

		if selectedVehicle then
			local vehicle = workspace.Vehicles:FindFirstChild(selectedVehicle)
			if vehicle and vehicle:FindFirstChild("Body") then
				local body = vehicle.Body
				local seat = body:FindFirstChild("CarSeatPosition") or body:FindFirstChild("VehicleSeat") or body:FindFirstChild("Passenger")

				if seat and seat:IsA("BasePart") then
					local originalPosition = hrp.CFrame
					hrp.CFrame = seat.CFrame
					wait(0.8)

					if vehicle.PrimaryPart then
						vehicle:SetPrimaryPartCFrame(originalPosition)
					elseif seat then
						vehicle:MoveTo(originalPosition.Position)
					end

					hrp.CFrame = originalPosition
				end
			end
		end
    end
})

local function teleportAllCars()
    for _, vehicle in ipairs(game.Workspace.Vehicles:GetChildren()) do
        for _, part in ipairs(vehicle:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
                part.Massless = true
            end
        end
    end
    
    wait(0.3)

    for _, vehicle in ipairs(game.Workspace.Vehicles:GetChildren()) do
        local playerPosition = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
        vehicle:SetPrimaryPartCFrame(playerPosition)
        for _, part in ipairs(vehicle:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
                part.Massless = false
            end
        end
    end
end

Tab9:AddSection({ "Todos os Carros" })

Tab9:AddButton({
    Name = "Puxar Carros",
    Callback = function()
        teleportAllCars()
    end
})

Tab9:AddButton({
    Name = "Remover Carros",
    Callback = function()
        local ofnawufn = false

if ofnawufn == true then
    return
end
ofnawufn = true

local cawwfer = "MilitaryBoatFree" 
local oldcfffff = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1754, -2, 58) 
wait(0.3)

local args = {
    [1] = "PickingBoat",
    [2] = cawwfer
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
wait(1)

local wrinfjn
for _, errb in pairs(game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"]:GetDescendants()) do
    if errb:IsA("VehicleSeat") then
        wrinfjn = errb
    end
end

repeat
    if game.Players.LocalPlayer.Character.Humanoid.Health == 0 then return end
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then
        if not game.Players.LocalPlayer.Character.Humanoid.SeatPart == wrinfjn then
            game.Players.LocalPlayer.Character.Humanoid.Sit = false
        end
    end
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = wrinfjn.CFrame
    task.wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = wrinfjn.CFrame + Vector3.new(0,1,0)
    task.wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = wrinfjn.CFrame + Vector3.new(0,-1,0)
    task.wait()
until game.Players.LocalPlayer.Character.Humanoid.SeatPart == wrinfjn

for _, wifn in pairs(game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"]:GetDescendants()) do
    if wifn.Name == "PhysicalWheel" then
        wifn:Destroy()
    end
end

local FLINGED = Instance.new("BodyThrust", game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass) 
FLINGED.Force = Vector3.new(50000, 0, 50000) 
FLINGED.Name = "SUNTERIUM HUB FLING"
FLINGED.Location = game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.Position

for _, wvwvwasc in pairs(game.workspace.Vehicles:GetChildren()) do
    for _, ascegr in pairs(wvwvwasc:GetDescendants()) do
        if ascegr.Name == "VehicleSeat" then
            local targetcar = ascegr
            local tet = Instance.new("BodyVelocity", game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass)
            tet.MaxForce = Vector3.new(math.huge,math.huge,math.huge)
            tet.P = 1250
            tet.Velocity = Vector3.new(0,0,0)
            tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"
            for m=1,25 do
                local pos = {x=0, y=0, z=0}
                pos.x = targetcar.Position.X
                pos.y = targetcar.Position.Y
                pos.z = targetcar.Position.Z
                pos.x = pos.x + targetcar.Velocity.X / 2
                pos.y = pos.y + targetcar.Velocity.Y / 2
                pos.z = pos.z + targetcar.Velocity.Z / 2
                if pos.y <= -200 then
                    game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.CFrame = CFrame.new(0,1000,0)
                else
                    game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.CFrame = CFrame.new(Vector3.new(pos.x,pos.y,pos.z))
                    task.wait()
                    game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.CFrame = CFrame.new(Vector3.new(pos.x,pos.y,pos.z)) + Vector3.new(0,-2,0)
                    task.wait()
                    game.workspace.Vehicles[game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.CFrame = CFrame.new(Vector3.new(pos.x,pos.y,pos.z)) * CFrame.new(0,0,2)
                    task.wait()
                    game.workspace.Vehicles[
game.Players.LocalPlayer.Name.."Car"].Chassis.Mass.CFrame = CFrame.new(Vector3.new(pos.x,pos.y,pos.z)) * CFrame.new(2,0,0)
                    task.wait()
                end
                task.wait()
            end
        end
    end
end

task.wait()
local args = {
    [1] = "DeleteAllVehicles"
}

game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer(unpack(args))
game.Players.LocalPlayer.Character.Humanoid.Sit = false
wait()
local tet = Instance.new("BodyVelocity", game.Players.LocalPlayer.Character.HumanoidRootPart)
tet.MaxForce = Vector3.new(math.huge,math.huge,math.huge)
tet.P = 1250
tet.Velocity = Vector3.new(0,0,0)
tet.Name = "#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"
wait(0.1)
for m=1,2 do 
    task.wait()
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcfffff
end
wait(1)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcfffff
wait()
game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("#mOVOOEPF$#@F$#GERE..>V<<<<EW<V<<W"):Destroy()
wait(0.2)
ofnawufn = false
    end
})

Tab9:AddSection({ "ESP Carros" })

local ESPEnabled = false
local espConnections = {}

local function createESP(vehicle)
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "ESP"
    billboard.Adornee = vehicle
    billboard.Size = UDim2.new(0, 150, 0, 30)
    billboard.StudsOffset = Vector3.new(0, 3, 0)
    billboard.AlwaysOnTop = true

    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.BackgroundTransparency = 1
    textLabel.TextColor3 = Color3.new(0, 1, 0)
    textLabel.TextScaled = true
    textLabel.Font = Enum.Font.SourceSansBold
    textLabel.Parent = billboard

    billboard.Parent = vehicle
    return textLabel
end

local function toggleESP(state)
    ESPEnabled = state
    if ESPEnabled then
        for _, vehicle in pairs(workspace.Vehicles:GetChildren()) do
            if not vehicle:FindFirstChild("ESP") and vehicle:IsA("Model") and vehicle.PrimaryPart then
                local textLabel = createESP(vehicle)
                local connection = game:GetService("RunService").RenderStepped:Connect(function()
                    if ESPEnabled and vehicle and vehicle.PrimaryPart then
                        local player = game.Players.LocalPlayer
                        local distance = (player.Character.PrimaryPart.Position - vehicle.PrimaryPart.Position).Magnitude
                        textLabel.Text = vehicle.Name .. " | Distância: " .. math.floor(distance) .. " studs"
                    end
                end)
                table.insert(espConnections, connection)
            end
        end
    else
        for _, connection in pairs(espConnections) do
            connection:Disconnect()
        end
        espConnections = {}
        for _, vehicle in pairs(workspace.Vehicles:GetChildren()) do
            if vehicle:FindFirstChild("ESP") then
                vehicle.ESP:Destroy()
            end
        end
    end
end

local Toggle = Tab9:AddToggle({
    Name = "ESP Carros",
    Default = false,
    Callback = function(Value)
        toggleESP(Value)
    end
})

