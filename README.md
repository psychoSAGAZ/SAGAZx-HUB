-------------------------------------------
-- Intro
-------------------------------------------

task.spawn(function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/Ngdykhvhhfchh/refs/heads/main/README.md"))()
end)

-------------------------------------------
-- Redz Lib
-------------------------------------------


local Window = redzlib:MakeWindow({
    Title = "SAGAZx HUB | Brookhaven",
    SubTitle = "| by SAGAZx",
    SaveFolder = "SAGAZxConfig"
})

Window:AddMinimizeButton({
    Button = {
        Image = "rbxassetid://86050226751861",
        BackgroundTransparency = 0
    },
    Corner = {
        CornerRadius = UDim.new(0, 8)
    },
})
----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Home-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab1 = Window:MakeTab({ "| Ini­cio", "menu" })

Tab1:AddDiscordInvite({
    Name = "SAGAZx",
    Description = "Me Siga No Discord e TikTok",
    Logo = "rbxassetid://86050226751861",
    Invite = "Discord: ''https://discord.gg/xWcFhEgg''         TikTok: ''tiktok.com/@sagazx_xd''   ",
})

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
Tab1:AddParagraph({"Versão", "2.0.1"})

Tab1:AddSection({Name = "Outros"}) 
Tab1:AddButton({
    Name = "Deletar Brookhaven News",
    Description = "Faz Muira Zuada",
    Callback = function()
        local obj = workspace:FindFirstChild("BrookavenNewsSign")

        if obj then
            obj:Destroy()
            print("BrookavenNewsSign deletado!")
        else
            warn("Objeto não encontrado.")
        end
    end
})

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

Tab2:AddSection({ Name = "Outros" })

local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

local LocalPlayer = Players.LocalPlayer

local SpinConnection
local SpinSpeed = 0.5

Tab2:AddTextBox({
    Name = "Velocidade do Spin",
    PlaceholderText = "Digite a velocidade",
    ClearText = false,
    Callback = function(Value)
        local Number = tonumber(Value)
        if Number then
            SpinSpeed = Number
        end
    end
})

Tab2:AddToggle({
    Name = "Spin",
    Description = "Gira o Personagem Infinitamente",
    Default = false,
    Callback = function(Value)
        if Value then
            if SpinConnection then
                SpinConnection:Disconnect()
            end

            SpinConnection = RunService.RenderStepped:Connect(function(dt)
                local Character = LocalPlayer.Character
                local Root = Character and Character:FindFirstChild("HumanoidRootPart")

                if Root then
                    Root.CFrame = Root.CFrame * CFrame.Angles(0, math.rad(360 * SpinSpeed * dt), 0)
                end
            end)
        else
            if SpinConnection then
                SpinConnection:Disconnect()
                SpinConnection = nil
            end
        end
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

Tab2:AddToggle({
    Name = "FullBright",
    Description = "Deixa o Mapa iluminado",
    Default = false,
    Callback = function(Value)
        if Value then
            -- Ativa o brilho máximo
            game:GetService("Lighting").Ambient = Color3.fromRGB(255, 255, 255)
            game:GetService("Lighting").OutdoorAmbient = Color3.fromRGB(255, 255, 255)
            game:GetService("Lighting").Brightness = 2
        else
            -- Volta ao normal (ajuste conforme o jogo se precisar)
            game:GetService("Lighting").Ambient = Color3.fromRGB(127, 127, 127)
            game:GetService("Lighting").OutdoorAmbient = Color3.fromRGB(127, 127, 127)
            game:GetService("Lighting").Brightness = 1
        end
    end
})

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local LocalPlayer = Players.LocalPlayer

local Swimming = false
local OldGravity = workspace.Gravity
local SwimBeat
local GravReset

Tab2:AddToggle({
    Name = "Swim",
    Description = "Nadar Sem Água",
    Default = false,
    Callback = function(Value)
        local Character = LocalPlayer.Character
        if not Character then return end

        local Humanoid = Character:FindFirstChildWhichIsA("Humanoid")
        local Root = Character:FindFirstChild("HumanoidRootPart")
        if not Humanoid or not Root then return end

        if Value then
            OldGravity = workspace.Gravity
            workspace.Gravity = 0

            GravReset = Humanoid.Died:Connect(function()
                workspace.Gravity = OldGravity
                Swimming = false
            end)

            for _, State in ipairs(Enum.HumanoidStateType:GetEnumItems()) do
                if State ~= Enum.HumanoidStateType.None then
                    Humanoid:SetStateEnabled(State, false)
                end
            end

            Humanoid:ChangeState(Enum.HumanoidStateType.Swimming)

            SwimBeat = RunService.Heartbeat:Connect(function()
                if Humanoid.MoveDirection.Magnitude > 0 then
                    Root.Velocity = Humanoid.MoveDirection * 20
                elseif UserInputService:IsKeyDown(Enum.KeyCode.Space) then
                    Root.Velocity = Vector3.new(0, 20, 0)
                else
                    Root.Velocity = Vector3.zero
                end

                Humanoid:ChangeState(Enum.HumanoidStateType.Swimming)
            end)

            Swimming = true
        else
            workspace.Gravity = OldGravity
            Swimming = false

            if GravReset then
                GravReset:Disconnect()
                GravReset = nil
            end

            if SwimBeat then
                SwimBeat:Disconnect()
                SwimBeat = nil
            end

            for _, State in ipairs(Enum.HumanoidStateType:GetEnumItems()) do
                if State ~= Enum.HumanoidStateType.None then
                    Humanoid:SetStateEnabled(State, true)
                end
            end
        end
    end
})

local RunService = game:GetService("RunService")
local LayConnection

Tab2:AddToggle({
    Name = "Deitar",
    Description = "Deita no Chão",
    Default = false,
    Callback = function(Value)
        local Character = game.Players.LocalPlayer.Character
        if not Character then return end

        local Humanoid = Character:FindFirstChildWhichIsA("Humanoid")
        local Root = Character:FindFirstChild("HumanoidRootPart")
        if not Humanoid or not Root then return end

        if Value then
            LayConnection = RunService.Heartbeat:Connect(function()
                Humanoid.PlatformStand = true
                Root.CFrame = CFrame.new(Root.Position) * CFrame.Angles(math.rad(90), Root.Orientation.Y * math.pi / 180, 0)
            end)
        else
            if LayConnection then
                LayConnection:Disconnect()
                LayConnection = nil
            end

            Humanoid.PlatformStand = false
            Humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
    end
})

Tab2:AddButton({
    Name = "Jerk",
    Description = "",
    Callback = function()
        loadstring(game:HttpGet("https://pastefy.app/YZoglOyJ/raw"))()
    end
})


Tab2:AddButton({
    Name = "Sit",
    Description = "Faz o Personagem Sentar",
    Callback = function()
        local Character = game.Players.LocalPlayer.Character
        if Character then
            local Humanoid = Character:FindFirstChildWhichIsA("Humanoid")
            if Humanoid then
                Humanoid.Sit = true
            end
        end
    end
})

Tab2:AddButton({
    Name = "Tp Tool",
    Description = "Teleporta Você Para Onde Você Clicar",
    Callback = function()
        local Player = game.Players.LocalPlayer

        -- Evita criar duas ferramentas
        if Player.Backpack:FindFirstChild("Tp Tool") then
            return
        end

        local Mouse = Player:GetMouse()

        local Tool = Instance.new("Tool")
        Tool.Name = "Tp Tool"
        Tool.RequiresHandle = false

        -- Coloque o ID da imagem aqui
        Tool.TextureId = "rbxassetid://1234567890"

        Tool.Activated:Connect(function()
            local Character = Player.Character
            local Root = Character and Character:FindFirstChild("HumanoidRootPart")

            if Root then
                Root.CFrame = CFrame.new(Mouse.Hit.Position + Vector3.new(0, 2.5, 0))
            end
        end)

        Tool.Parent = Player.Backpack
    end
})



Tab2:AddSection({ Name = "Espião" })

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local cam = workspace.CurrentCamera

local viewing = false
local playerList = {}
local currentIndex = 1
local screenGui
local lastPlayerName = nil --  salva último player

--  Atualiza lista de players
local function UpdatePlayerList()
    playerList = {}
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer then
            table.insert(playerList, plr)
        end
    end

    table.sort(playerList, function(a,b)
        return a.Name < b.Name
    end)
end

--  Player atual
local function GetCurrentPlayer()
    return playerList[currentIndex]
end

--  Spectar
local function Spectate(plr)
    if not plr then return end

    local char = plr.Character or plr.CharacterAdded:Wait()
    local hum = char:FindFirstChild("Humanoid")

    if hum then
        cam.CameraSubject = hum
    end
end

--  Reset camera
local function ResetCamera()
    local char = LocalPlayer.Character
    if char and char:FindFirstChild("Humanoid") then
        cam.CameraSubject = char.Humanoid
    end
end

--  CRIAR SUA GUI
local function CreateUI()
    if screenGui then screenGui:Destroy() end

    screenGui = Instance.new("ScreenGui")
    screenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

    -- BOTÃO <
    local back = Instance.new("TextButton", screenGui)
    back.Size = UDim2.new(0, 60, 0, 60)
    back.Position = UDim2.new(0, 412, 0, 425)
    back.Text = "<"
    back.TextSize = 50
    back.BackgroundColor3 = Color3.fromRGB(108,108,108)
    Instance.new("UICorner", back)

    -- FRAME CENTRAL
    local frame = Instance.new("Frame", screenGui)
    frame.Size = UDim2.new(0, 200, 0, 60)
    frame.Position = UDim2.new(1, -688, 0, 425)
    frame.BackgroundColor3 = Color3.fromRGB(108,108,108)
    Instance.new("UICorner", frame)

    -- IMAGEM
    local img = Instance.new("ImageLabel", frame)
    img.Size = UDim2.new(0,40,0,40)
    img.Position = UDim2.new(0,10,0,10)
    img.BackgroundTransparency = 1

    -- TEXTO
    local titulo = Instance.new("TextLabel", frame)
    titulo.Size = UDim2.new(1,-60,0,20)
    titulo.Position = UDim2.new(0,60,0,8)
    titulo.Text = "Espionando:"
    titulo.TextColor3 = Color3.new(1,1,1)
    titulo.BackgroundTransparency = 1
    titulo.Font = Enum.Font.GothamBold
    titulo.TextSize = 15
    titulo.TextXAlignment = Enum.TextXAlignment.Left

    -- USERNAME
    local username = Instance.new("TextLabel", frame)
    username.Size = UDim2.new(1,-60,0,18)
    username.Position = UDim2.new(0,60,0,30)
    username.BackgroundTransparency = 1
    username.TextColor3 = Color3.new(1,1,1)
    username.Font = Enum.Font.Gotham
    username.TextSize = 12
    username.TextXAlignment = Enum.TextXAlignment.Left

    -- BOTÃO >
    local next = Instance.new("TextButton", screenGui)
    next.Size = UDim2.new(0, 60, 0, 60)
    next.Position = UDim2.new(0, 685, 0, 425)
    next.Text = ">"
    next.TextSize = 50
    next.BackgroundColor3 = Color3.fromRGB(108,108,108)
    Instance.new("UICorner", next)

    --  Atualiza UI
    local function UpdateUI()
        local plr = GetCurrentPlayer()
        if not plr then return end

        lastPlayerName = plr.Name --  salva automaticamente

        username.Text = "@" .. plr.Name

        img.Image = "https://www.roblox.com/headshot-thumbnail/image?userId="
            .. plr.UserId .. "&width=150&height=150&format=png"

        Spectate(plr)
    end

    -- 
    back.MouseButton1Click:Connect(function()
        if #playerList == 0 then return end
        currentIndex -= 1
        if currentIndex < 1 then
            currentIndex = #playerList
        end
        UpdateUI()
    end)

    -- 
    next.MouseButton1Click:Connect(function()
        if #playerList == 0 then return end
        currentIndex += 1
        if currentIndex > #playerList then
            currentIndex = 1
        end
        UpdateUI()
    end)

    UpdateUI()
end

--  TOGGLE REDZ
Tab2:AddToggle({
    Name = "Espiona Todos Os Players",
    Default = false,
    Callback = function(Value)
        viewing = Value

        if viewing then
            UpdatePlayerList()

            if #playerList == 0 then
                warn("Sem players")
                return
            end

            --  tenta voltar pro último player
            currentIndex = 1
            if lastPlayerName then
                for i, plr in ipairs(playerList) do
                    if plr.Name == lastPlayerName then
                        currentIndex = i
                        break
                    end
                end
            end

            CreateUI()
            Spectate(GetCurrentPlayer())

        else
            if screenGui then
                screenGui:Destroy()
                screenGui = nil
            end
            ResetCamera()
        end
    end
})

--  Atualização automática
Players.PlayerAdded:Connect(UpdatePlayerList)
Players.PlayerRemoving:Connect(UpdatePlayerList)

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




Tab2:AddSection({ Name = "CAMERA LOCK", Icon = "rbxassetid://" })

local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local CamDistance = 10
local CamHeight = 5
local CamTilt = 0
local CamLower = 0
local CamLocked = false
local SmoothSpeed = 0.15

local CamPosition = nil
local CamLookAt = nil

local function updateCamera()
	if CamLocked and CamPosition and CamLookAt then
		local offset = Vector3.new(0, CamHeight - CamLower, CamDistance)
		local targetCFrame = CFrame.new(CamPosition + offset, CamLookAt) * CFrame.Angles(math.rad(CamTilt), 0, 0)
		Camera.CameraType = Enum.CameraType.Scriptable
		Camera.CFrame = Camera.CFrame:Lerp(targetCFrame, SmoothSpeed)
	end
end

Tab2:AddSlider({
	Name = "CAMERA DISTANCE",
	Min = 1,
	Max = 50,
	Default = CamDistance,
	Callback = function(value)
		CamDistance = value
	end
})

Tab2:AddSlider({
	Name = "CAMERA HEIGHT",
	Min = -50,
	Max = 50,
	Default = CamHeight,
	Callback = function(value)
		CamHeight = value
	end
})

Tab2:AddSlider({
	Name = "CAMERA TILT",
	Min = -90,
	Max = 90,
	Default = CamTilt,
	Callback = function(value)
		CamTilt = value
	end
})

Tab2:AddSlider({
	Name = "CAMERA LOWER",
	Min = -50,
	Max = 50,
	Default = CamLower,
	Callback = function(value)
		CamLower = value
	end
})

Tab2:AddToggle({
	Name = "LOCK CAMERA",
	Default = false,
	Callback = function(state)
		if state then
			local char = LocalPlayer.Character
			if char and char:FindFirstChild("HumanoidRootPart") then
				local hrp = char.HumanoidRootPart
				local forward = hrp.CFrame.LookVector
				CamPosition = hrp.Position - forward * CamDistance + Vector3.new(0, CamHeight - CamLower, 0)
				CamLookAt = hrp.Position
			end
			CamLocked = true
		else
			CamLocked = false
			Camera.CameraType = Enum.CameraType.Custom
			CamPosition = nil
			CamLookAt = nil
		end
	end
})
RunService.RenderStepped:Connect(updateCamera)

Tab2:AddSection({ Name = "Spawn Bombas", Icon = "rbxassetid://" })

local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local WorkspaceService = game:GetService("Workspace")


local BombAmount = 5 
local ColetandoBombas = false -- Controla se o loop de coleta deve rodar ou parar


local BlowBombsServer = nil
pcall(function()
    local SettingsModule = require(Player:WaitForChild("PlayerGui"):WaitForChild("Player8Handler"):WaitForChild("Game8Settings"))
    BlowBombsServer = SettingsModule.BlowBombsServer
end)

local BombFolder = nil
pcall(function()
    BombFolder = WorkspaceService.WorkspaceCom["001_CriminalWeapons"].GiveTools
end)


Tab2:AddTextBox({
    Name = "Quantidade De Bombas",
    Default = "5",
    PlaceholderText = "Digite um numero...",
    ClearTextOnFocus = false,
    Callback = function(value)
        local num = tonumber(value)
        if num and num > 0 then
            BombAmount = num
        else
            BombAmount = 5 -- Valor padrao caso o texto digitado seja invÃ¡lido
        end
    end
})


local function getBombCount()
    local cnt = 0
    if Player:FindFirstChild("Backpack") then
        for _, t in ipairs(Player.Backpack:GetChildren()) do
            if t:IsA("Tool") and t.Name:lower():find("bomb") then
                cnt = cnt + 1
            end
        end
    end
    if Player.Character then
        for _, t in ipairs(Player.Character:GetChildren()) do
            if t:IsA("Tool") and t.Name:lower():find("bomb") then
                cnt = cnt + 1
            end
        end
    end
    return cnt
end


Tab2:AddButton({
    Name = "Pega Bombas",
    Callback = function()
        if ColetandoBombas then 
            print("Já existe uma coleta em andamento!")
            return 
        end
        
        ColetandoBombas = true
        
        task.spawn(function()
            local Character = Player.Character
            if not Character then
                print("Character não encontrado!")
                ColetandoBombas = false
                return
            end
            
            local RootPart = Character:WaitForChild("HumanoidRootPart", 5)
            if not RootPart then
                print("HumanoidRootPart não encontrado!")
                ColetandoBombas = false
                return
            end
            
            local origin = RootPart.CFrame
            local attempts = 0
            local collected = getBombCount()

            if CreateNotification and CreateNotification.Notification then
                CreateNotification:Notification("Coleta", "Iniciando coleta automatizada...", 2)
            else
                print("Iniciando coleta automatizada...")
            end

            -- Loop de repetição principal
            while ColetandoBombas and collected < BombAmount and attempts < 150 do
                attempts = attempts + 1
                
                -- Busca a bomba dinamicamente a cada loop para evitar referências nulas (nil)
                local AlvoBomba = nil
                
                -- 1ª Tentativa: Procura na pasta oficial que você informou
                if BombFolder then
                    AlvoBomba = BombFolder:FindFirstChild("Bomb") or BombFolder:FindFirstChildWhichIsA("BasePart")
                end
                
                -- 2ª Tentativa: Se não achou na pasta, escaneia o workspace por ClickDetectors de bomba
                if not AlvoBomba then
                    for _, v in ipairs(workspace:GetDescendants()) do
                        if v:IsA("ClickDetector") and v.Parent and v.Parent.Name:lower():find("bomb") then
                            AlvoBomba = v.Parent
                            break
                        end
                    end
                end

                -- Se encontrou a bomba e o ClickDetector, executa a aproximação e clique
                if AlvoBomba and AlvoBomba:FindFirstChild("ClickDetector") and RootPart then
                    pcall(function()
                        -- Teleporta ligeiramente acima do item
                        RootPart.CFrame = AlvoBomba.CFrame * CFrame.new(0, 1.8, 0)
                        task.wait(0.02)
                        fireclickdetector(AlvoBomba.ClickDetector, 2)
                    end)
                else
                    -- Se não encontrou nenhuma bomba no mapa inteiro, avisa no console
                    print("Procurando bomba no mapa... Nenhuma encontrada nesta tentativa (" .. tostring(attempts) .. ")")
                end

                task.wait(0.05) -- Delay seguro para o Roblox registrar o clique
                collected = getBombCount()
            end
            
            -- Retorna à posição original de forma segura
            pcall(function() 
                RootPart.CFrame = origin 
            end)
            
            -- Verificação final de estoque
            if ColetandoBombas then
                if collected >= BombAmount then
                    if CreateNotification and CreateNotification.Notification then
                        CreateNotification:Notification("Sucesso", "Total de " .. tostring(collected) .. " bombas coletadas!", 3)
                    end
                else
                    if CreateNotification and CreateNotification.Notification then
                        CreateNotification:Notification("Aviso", "A coleta encerrou. Total obtido: " .. tostring(collected) .. "/" .. tostring(BombAmount), 4)
                    end
                end
            end
            
            ColetandoBombas = false
        end)
    end
})




Tab2:AddButton({
    Name = "Parar de Pega Bombas",
    Callback = function()
        if ColetandoBombas then
            ColetandoBombas = false -- Altera a flag para fechar o loop do botÃ£o acima imediatamente
            CreateNotification:Notification("Interrompido", "Cancelando coleta e retornando Ã  posiÃ§Ã£o...", 3)
        else
            CreateNotification:Notification("Info", "VocÃª nÃ£o estÃ¡ coletando bombas no momento.", 2)
        end
    end
})


Tab2:AddButton({
    Name = "Spawn Bombas",
    Callback = function()
        task.spawn(function()
            local Character = Player.Character or Player.CharacterAdded:Wait()
            local RootPart = Character:WaitForChild("HumanoidRootPart")
            
            local ferramentas = {}
            
            if Player:FindFirstChild("Backpack") then
                for _, t in ipairs(Player.Backpack:GetChildren()) do
                    if t:IsA("Tool") and t.Name:lower():find("bomb") then
                        table.insert(ferramentas, t)
                    end
                end
            end

            for _, t in ipairs(Character:GetChildren()) do
                if t:IsA("Tool") and t.Name:lower():find("bomb") then
                    table.insert(ferramentas, t)
                end
            end

            if #ferramentas == 0 then
                CreateNotification:Notification("Erro", "Nenhuma bomba encontrada no seu inventÃ¡rio!", 3)
                return
            end

            for _, bomb in ipairs(ferramentas) do
                task.spawn(function()
                    pcall(function()
                        local mouseLoc = bomb:FindFirstChild("MouseLoc")
                        local mouseLocCone = bomb:FindFirstChild("MouseLocCone")

                        if mouseLoc then
                            mouseLoc.OnClientInvoke = function()
                                return RootPart.Position + Vector3.new(0, 4, 0)
                            end
                        end

                        if mouseLocCone then
                            mouseLocCone.OnClientInvoke = function()
                                return RootPart
                            end
                        end

                        if bomb.Parent ~= Character then
                            bomb.Parent = Character
                        end
                        bomb:Activate()
                    end)
                end)
            end
        end)
    end
})


Tab2:AddButton({
    Name = "Ativa Bombas",
    Callback = function()
        if BlowBombsServer and BlowBombsServer:IsA("RemoteEvent") then
            pcall(function()
                BlowBombsServer:FireServer("Bomb" .. Player.Name)
                CreateNotification:Notification("DetonaÃ§Ã£o", "Sinal enviado para explodir as bombas!", 3)
            end)
        else
            pcall(function()
                ReplicatedStorage.RE["1Blo1wBomb1sServe1r"]:FireServer("Bomb" .. Player.Name)
                CreateNotification:Notification("DetonaÃ§Ã£o", "Sinal alternativo enviado!", 3)
            end)
        end
    end
})


local LoopSpamBomba = false

Tab2:AddToggle({
    Name = "Auto Spawn e Ativar Bombas",
    Default = false,
    Callback = function(state)
        LoopSpamBomba = state
        
        if LoopSpamBomba then
            task.spawn(function()
                if CreateNotification and CreateNotification.Notification then
                    CreateNotification:Notification("Auto Spam", "Loop de bombas ativado!", 2)
                end
                
                -- Loop principal enquanto o Toggle estiver ligado
                while LoopSpamBomba do
                    local Character = Player.Character
                    local RootPart = Character and Character:FindFirstChild("HumanoidRootPart")
                    
                    if Character and RootPart then
                        local ferramentas = {}
                        
                        -- 1. Coleta todas as bombas do inventário
                        if Player:FindFirstChild("Backpack") then
                            for _, t in ipairs(Player.Backpack:GetChildren()) do
                                if t:IsA("Tool") and t.Name:lower():find("bomb") then
                                    table.insert(ferramentas, t)
                                end
                            end
                        end
                        for _, t in ipairs(Character:GetChildren()) do
                            if t:IsA("Tool") and t.Name:lower():find("bomb") then
                                table.insert(ferramentas, t)
                            end
                        end

                        -- 2. Se houver bombas, inicia o processo de descarregar
                        if #ferramentas > 0 then
                            -- Move todas as bombas para o personagem imediatamente
                            for _, bomb in ipairs(ferramentas) do
                                pcall(function()
                                    local mouseLoc = bomb:FindFirstChild("MouseLoc")
                                    local mouseLocCone = bomb:FindFirstChild("MouseLocCone")

                                    if mouseLoc then
                                        mouseLoc.OnClientInvoke = function()
                                            return RootPart.Position + Vector3.new(0, 4, 0)
                                        end
                                    end
                                    if mouseLocCone then
                                        mouseLocCone.OnClientInvoke = function()
                                            return RootPart
                                        end
                                    end

                                    if bomb.Parent ~= Character then
                                        bomb.Parent = Character
                                    end
                                end)
                            end
                            
                            --  PAUSA CRÍTICA: Dá tempo (0.03s) para o Roblox reconhecer as bombas nas suas mãos
                            task.wait(0.03)

                            -- Ativa todas que foram equipadas
                            for _, bomb in ipairs(ferramentas) do
                                pcall(function()
                                    bomb:Activate()
                                end)
                            end

                            --  SEGUNDA PAUSA CRÍTICA: Dá tempo para as bombas irem para a cabeça antes do "Boom"
                            task.wait(0.05)
                            
                            -- 3. Detonação remota
                            if BlowBombsServer and BlowBombsServer:IsA("RemoteEvent") then
                                pcall(function()
                                    BlowBombsServer:FireServer("Bomb" .. Player.Name)
                                end)
                            else
                                pcall(function()
                                    ReplicatedStorage.RE["1Blo1wBomb1sServe1r"]:FireServer("Bomb" .. Player.Name)
                                end)
                            end
                        end
                    end
                    
                    -- Pequena espera de 0.1 segundos antes de repetir todo o ciclo novamente
                    task.wait(0.1) 
                end
                
                if CreateNotification and CreateNotification.Notification then
                    CreateNotification:Notification("Auto Spam", "Loop de bombas desativado.", 2)
                end
            end)
        end
    end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Jogadores-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

local Tab3= Window:MakeTab({ "| Jogadores", "users" })


local DropdownJogadores
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local selectedPlayer = nil  -- Armazena o jogador selecionado

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
    frame.BackgroundColor3 = Color3.fromRGB(27, 5, 25)
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
    close.TextColor3 = Color3.fromRGB(255, 255, 255)
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

-- 👥 LISTA DE PLAYERS
local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

Tab3:AddButton({
    Name = "Click Player",
    Callback = function()

        local backpack = LocalPlayer:WaitForChild("Backpack")

        -- Remove a antiga caso exista
        if backpack:FindFirstChild("SelecionarPlayer") then
            backpack.SelecionarPlayer:Destroy()
        end

        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("SelecionarPlayer") then
            LocalPlayer.Character.SelecionarPlayer:Destroy()
        end

        local Tool = Instance.new("Tool")
        Tool.Name = "SelecionarPlayer"
        Tool.RequiresHandle = false
        Tool.CanBeDropped = false
        Tool.TextureId = "rbxassetid://10747373426"
        Tool.Parent = backpack

        local Mouse = LocalPlayer:GetMouse()

        Tool.Activated:Connect(function()
            local Target = Mouse.Target
            if not Target then
                return
            end

            local Character = Target:FindFirstAncestorOfClass("Model")
            if not Character then
                return
            end

            local Player = Players:GetPlayerFromCharacter(Character)
            if not Player or Player == LocalPlayer then
                return
            end

            selectedPlayer = Player.Name

            if DropdownJogadores then
                DropdownJogadores:Set(Player.Name)
            end

            CreateNotification(
                "Notificação",
                "Player selecionado: "..Player.Name,
                3
            )
        end)
    end
})

-- 🎯 DROPDOWN DE TARGET (Alterado para usar a nova DropdownPlayer)
DropdownJogadores = Tab3:AddDropdownPlayer({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = "...",
    Callback = function(Value)
        selectedPlayer = Value
        print("Alvo selecionado: " .. tostring(selectedPlayer))

        -- Evita mandar notificação se o valor for o reset padrão da biblioteca
        if Value and Value ~= "..." and Value ~= "Selecionar Jogador" then
            CreateNotification("Notificação", "Player selecionado: "..Value, 3)
        end
    end
})

-- 🔁 ATUALIZAÇÃO AUTOMÁTICA SUPER SIMPLIFICADA
local function UpdateDropdown()
    task.wait(0.3) -- Aguarda o Roblox terminar de processar o player
    if DropdownJogadores then
        local nomesAtualizados = GetPlayerNames()
        
        -- Atualiza a lista nativamente pela nova função sem perder o nome visível!
        DropdownJogadores:Set(nomesAtualizados)
    end
end

-- CONEXÕES DOS EVENTOS
Players.PlayerAdded:Connect(UpdateDropdown)

Players.PlayerRemoving:Connect(function(plr)
    -- Se o jogador que saiu era o nosso alvo, avisa na tela
    if selectedPlayer and plr.Name == selectedPlayer then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
        selectedPlayer = nil
    end

    UpdateDropdown()
end)




local selectedKillMethod = nil -- Variável global que vai guardar o método ativo

Tab3:AddDropdown({
    Name = "Método Kill/Bring",
    Options = { "ônibus", "sofa", "prop" }, -- As opções que aparecem na interface
    Default = nil,
    Callback = function(Value)
        selectedKillMethod = Value
        print("Método selecionado: " .. tostring(selectedKillMethod))
        CreateNotification("Método", "Selecionado: " .. Value, 2)
    end
})
 

local selectedFlingMethod = nil -- Variável global que vai guardar o método de fling ativo

Tab3:AddDropdown({
    Name = "Método Fling",
    Options = { "ônibus", "sofa", "prop", "bola" }, -- Todas as opções solicitadas
    Default = nil,
    Callback = function(Value)
        selectedFlingMethod = Value
        print("Método Fling selecionado: " .. tostring(selectedFlingMethod))
        CreateNotification("Método Fling", "Selecionado: " .. Value, 2)
    end
})


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

Tab3:AddButton({
    Name = "Bring",
    Callback = function()
        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            return
        end

        if selectedKillMethod == "ônibus" then
            task.spawn(function()
                local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
                if not targetPlayer or not targetPlayer.Character then return end

                local character = game:GetService("Players").LocalPlayer.Character or game:GetService("Players").LocalPlayer.CharacterAdded:Wait()
                local rootPart = character:WaitForChild("HumanoidRootPart")
                local humanoid = character:WaitForChild("Humanoid")
                
                local realOriginalPos = rootPart.CFrame 
                local busSpawnPlace = CFrame.new(82.657265, 6.133477, -1368.286011)

                rootPart.CFrame = busSpawnPlace
                task.wait(2)

                game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1Ca1r"):FireServer("PickingCar", "Bus", "Work")
                task.wait(3)

                local bus = workspace.Vehicles:FindFirstChild(game:GetService("Players").LocalPlayer.Name .. "Car")
                if bus then
                    local seat = bus:FindFirstChild("Seats") and bus.Seats:FindFirstChild("VehicleSeat")
                    if seat then
                        seat:Sit(humanoid)
                        repeat task.wait() until humanoid.Sit
                    end

                    local tChar = targetPlayer.Character
                    local tRoot = tChar:FindFirstChild("HumanoidRootPart")
                    local tHum = tChar:FindFirstChildOfClass("Humanoid")

                    if tRoot and tHum then
                        local pullTimer = tick()
                        while tHum.Health > 0 and not tHum.Sit and (tick() - pullTimer) < 15 do
                            task.wait()
                            local time = tick() * 35
                            local lateralOffset = math.sin(time) * 4
                            local frontBackOffset = math.cos(time) * 20
                            bus:PivotTo(tRoot.CFrame * CFrame.new(lateralOffset, 0, frontBackOffset))
                        end

                        if tHum.Sit then
                            task.wait(0.5)
                            bus:PivotTo(realOriginalPos)
                            task.wait(1.5)
                        end
                    end

                    humanoid.Sit = false
                    task.wait(0.2)
                    rootPart.CFrame = realOriginalPos + Vector3.new(0, 3, 0)
                    task.wait(0.3)
                    
                    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Ca1r"):FireServer("DeleteAllVehicles")
                end
            end)

        elseif selectedKillMethod == "sofa" then
            task.spawn(function()
                local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
                local char = game:GetService("Players").LocalPlayer.Character
                if not targetPlayer or not char then return end

                local hum = char:FindFirstChildOfClass("Humanoid")
                local root = char:FindFirstChild("HumanoidRootPart")
                local targetRoot = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                local targetHum = targetPlayer.Character and targetPlayer.Character:FindFirstChildOfClass("Humanoid")

                if not hum or not root or not targetRoot or not targetHum then return end

                local originalCFrame = root.CFrame
                local Remotes = game:GetService("ReplicatedStorage"):WaitForChild("RE")
                
                Remotes:WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                task.wait(0.2)
                Remotes:WaitForChild("1Too1l"):InvokeServer("PickingTools", "Couch")
                
                local couch = game:GetService("Players").LocalPlayer.Backpack:WaitForChild("Couch", 5)
                if not couch then return end
                couch.Parent = char
                
                task.wait(0.2)
                game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.F, false, game)
                hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false)

                local bp = Instance.new("BodyPosition")
                bp.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                bp.D = 100
                bp.P = 10000
                bp.Parent = targetRoot

                local startTime = tick()
                while tick() - startTime < 7 do
                    if targetHum.Sit then break end
                    
                    local rot = CFrame.Angles(math.rad(math.random(-90, 90)), math.rad(math.random(-90, 90)), math.rad(math.random(-90, 90)))
                    local offset = Vector3.new(math.random(-4, 4), 2, math.random(-4, 4))
                    
                    root.CFrame = CFrame.new(targetRoot.Position + offset) * rot
                    bp.Position = root.Position
                    task.wait(0.05)
                end

                bp:Destroy()
                
                root.Velocity = Vector3.zero
                root.RotVelocity = Vector3.zero
                root.CFrame = originalCFrame
                
                task.wait(1)
                
                Remotes:WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                local checkTool = char:FindFirstChild("Couch") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Couch")
                if checkTool then checkTool:Destroy() end

                hum:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
                
                hum.WalkSpeed = 0
                hum.JumpPower = 0
                
                local stopTime = tick()
                while tick() - stopTime < 3 do
                    root.Velocity = Vector3.zero
                    root.RotVelocity = Vector3.zero
                    root.CFrame = originalCFrame
                    task.wait()
                end
                
                hum.WalkSpeed = 16
                hum.JumpPower = 50
            end)

        elseif selectedKillMethod == "prop" then
            -- === SCRIPT DE BRING USANDO PROP ===
            task.spawn(function()
                local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
                if not targetPlayer or targetPlayer == game:GetService("Players").LocalPlayer then return end
                
                -- Limpa e spawna o prop
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllProps")
                task.wait(0.2)
                
                local char = game:GetService("Players").LocalPlayer.Character
                if not char then return end
                local hrp = char:WaitForChild("HumanoidRootPart")
                local humanoid = char:WaitForChild("Humanoid")
                
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "PropMaker")
                local tool = game:GetService("Players").LocalPlayer.Backpack:WaitForChild("PropMaker", 5)
                if tool then
                    humanoid:EquipTool(tool)
                    task.wait(0.3)
                    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("RequestingPropName", "FurnitureBleachers", "Furniture")
                    task.wait(0.5)
                    local toolRemote = tool:FindFirstChild("Tool_PropMake")
                    if toolRemote then
                        toolRemote:FireServer(workspace.Model.Street.Street, hrp.Position + Vector3.new(0, -15, 0))
                    end
                    game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Up(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
                end

                local dest = hrp.CFrame * CFrame.new(0, 0, -5)
                local wasSitting = false
                local liftOffset = -10
                
                local connection
                connection = game:GetService("RunService").Heartbeat:Connect(function()
                    local c = targetPlayer.Character
                    local r = c and c:FindFirstChild("HumanoidRootPart")
                    local h = c and c:FindFirstChild("Humanoid")
                    if not r or not h or not connection then return end
                    
                    -- Função interna para achar os props
                    local props = {}
                    local workspaceCom = workspace:FindFirstChild("WorkspaceCom")
                    if workspaceCom then
                        for _,folder in ipairs(workspaceCom:GetChildren()) do
                            for _,p in ipairs(folder:GetChildren()) do
                                if p.Name:find("Prop"..game:GetService("Players").LocalPlayer.Name) and p:FindFirstChild("SetCurrentCFrame") then
                                    table.insert(props, p)
                                end
                            end
                        end
                    end

                    if h.Sit then
                        if not wasSitting then
                            wasSitting = true
                            for _,prop in ipairs(props) do
                                pcall(function() prop.SetCurrentCFrame:InvokeServer(dest) end)
                            end
                            task.wait(0.4)
                            if connection then connection:Disconnect() connection = nil end
                            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllProps")
                        end
                    else
                        wasSitting = false
                        liftOffset = liftOffset + 0.5
                        if liftOffset > 2 then liftOffset = -10 end
                        for _,prop in ipairs(props) do
                            pcall(function() prop.SetCurrentCFrame:InvokeServer(r.CFrame * CFrame.new(0, liftOffset, 0)) end)
                        end
                    end
                end)
                
                task.wait(10) -- Limite de tempo de segurança para desligar se falhar
                if connection then connection:Disconnect() connection = nil end
            end)
        else
            warn("Nenhum método foi selecionado no Dropdown!")
        end
    end
})

Tab3:AddButton({
    Name = "Kill",
    Callback = function()
        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            return
        end

        -- Verifica qual método está selecionado e executa o código original correspondente
        if selectedKillMethod == "ônibus" then
            
            -- === MÉTODO ÔNIBUS ORIGINAL (KILL COM TELEPORTE PRO VOID) ===
            task.spawn(function()
                local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
                if not targetPlayer or not targetPlayer.Character then return end
                
                local ReplicatedStorage = game:GetService("ReplicatedStorage")
                local LocalPlayer = game:GetService("Players").LocalPlayer
                local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
                local rootPart = character:WaitForChild("HumanoidRootPart")
                local humanoid = character:WaitForChild("Humanoid")
                local oldPos = rootPart.CFrame

                rootPart.CFrame = CFrame.new(82.657265, 6.133477, -1368.286011)
                task.wait(2)

                local spawnArgs = {"PickingCar", "Bus", "Work"}
                ReplicatedStorage:WaitForChild("RE"):WaitForChild("1Ca1r"):FireServer(unpack(spawnArgs))
                task.wait(3)

                local bus = workspace:WaitForChild("Vehicles"):FindFirstChild(LocalPlayer.Name .. "Car")
                if bus then
                    local seat = bus:FindFirstChild("Seats") and bus.Seats:FindFirstChild("VehicleSeat")
                    if seat then
                        seat:Sit(humanoid)
                        repeat task.wait() until humanoid.Sit
                    end

                    local tChar = targetPlayer.Character
                    local tRoot = tChar:FindFirstChild("HumanoidRootPart")
                    local tHum = tChar:FindFirstChildOfClass("Humanoid")

                    if tRoot and tHum then
                        local killTimer = tick()
                        while tHum.Health > 0 and not tHum.Sit and (tick() - killTimer) < 15 do
                            task.wait()
                            local randomX, randomY, randomZ = math.random(-360, 360), math.random(-360, 360), math.random(-360, 360)
                            local offset = tHum.MoveDirection * (tRoot.Velocity.Magnitude / 1.05)
                            local ang = CFrame.Angles(math.rad(randomX), math.rad(randomY), math.rad(randomZ))
                            
                            local function kill(pos)
                                if bus and (bus.PrimaryPart or bus:FindFirstChild("Seats")) then
                                    bus:PivotTo(CFrame.new(tRoot.Position) * pos * ang)
                                end
                            end

                            kill(CFrame.new(0, 1, 0) + offset)
                            kill(CFrame.new(0, -2.25, 5) + offset)
                            kill(CFrame.new(0, 2.25, 0.25) + offset)
                            kill(CFrame.new(-2.25, -1.5, 2.25) + offset)
                            kill(CFrame.new(0, 1.5, 0) + offset)
                            kill(CFrame.new(0, -1.5, 0) + offset)
                        end
                    end

                    -- LEVA PARA O VOID (Mecânica que faltava)
                    bus:PivotTo(CFrame.new(0, -470, 0))
                    task.wait(0.2)
                    humanoid.Sit = false
                    task.wait(0.1)
                    rootPart.CFrame = oldPos
                    ReplicatedStorage.RE:FindFirstChild("1Ca1r"):FireServer("DeleteAllVehicles")
                end
            end)

        elseif selectedKillMethod == "sofa" then
            
            -- === MÉTODO SOFÁ ORIGINAL (COUCH KILL) ===
            task.spawn(function()
                local Players = game:GetService("Players")
                local ReplicatedStorage = game:GetService("ReplicatedStorage")
                local VirtualInputManager = game:GetService("VirtualInputManager")
                local LocalPlayer = Players.LocalPlayer
                local Remotes = ReplicatedStorage:WaitForChild("RE")

                local targetPlayer = Players:FindFirstChild(selectedPlayer)
                local char = LocalPlayer.Character
                if not targetPlayer or not char then return end

                local hum = char:FindFirstChildOfClass("Humanoid")
                local root = char:FindFirstChild("HumanoidRootPart")
                local targetRoot = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                local targetHum = targetPlayer.Character and targetPlayer.Character:FindFirstChildOfClass("Humanoid")

                if not hum or not root or not targetRoot or not targetHum then return end

                local originalCFrame = root.CFrame
                
                Remotes:WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                task.wait(0.3)
                Remotes:WaitForChild("1Too1l"):InvokeServer("PickingTools", "Couch")
                
                local couch = LocalPlayer.Backpack:WaitForChild("Couch", 5)
                if not couch then return end
                couch.Parent = char
                
                task.wait(0.2)
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.F, false, game)
                hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false)

                local bp = Instance.new("BodyPosition")
                bp.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                bp.D = 100
                bp.P = 10000
                bp.Parent = targetRoot

                local startTime = tick()
                while tick() - startTime < 7 do
                    if targetHum.Sit then break end
                    
                    local rot = CFrame.Angles(math.rad(math.random(-90, 90)), math.rad(math.random(-90, 90)), math.rad(math.random(-90, 90)))
                    local offset = Vector3.new(math.random(-4, 4), 2, math.random(-4, 4))
                    
                    root.CFrame = CFrame.new(targetRoot.Position + offset) * rot
                    bp.Position = root.Position
                    task.wait(0.05)
                end

                bp:Destroy()
                root.Velocity = Vector3.zero
                root.RotVelocity = Vector3.zero

                -- Puxa o jogador para baixo caso ele sente (Mecânica original de Kill do sofá)
                if targetHum.Sit then
                    task.wait(0.1)
                    root.CFrame = CFrame.new(root.Position.X, -100, root.Position.Z)
                    task.wait(0.3)
                    
                    Remotes:WaitForChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                    local checkTool = char:FindFirstChild("Couch") or LocalPlayer.Backpack:FindFirstChild("Couch")
                    if checkTool then checkTool:Destroy() end
                    task.wait(0.5)
                end

                hum:SetStateEnabled(Enum.HumanoidStateType.Seated, true)
                
                root.Velocity = Vector3.zero
                root.RotVelocity = Vector3.zero
                root.CFrame = originalCFrame
                
                hum.WalkSpeed = 0
                hum.JumpPower = 0
                
                local stopTime = tick()
                while tick() - stopTime < 3 do
                    root.Velocity = Vector3.zero
                    root.RotVelocity = Vector3.zero
                    root.CFrame = originalCFrame
                    task.wait()
                end
                hum.WalkSpeed = 16
                hum.JumpPower = 50
            end)

        elseif selectedKillMethod == "prop" then
            
            -- === MÉTODO PROP ORIGINAL (KILL PROP COM BLEACHERS) ===
            task.spawn(function()
                local Players = game:GetService("Players")
                local RunService = game:GetService("RunService")
                local ReplicatedStorage = game:GetService("ReplicatedStorage")
                local VirtualUser = game:GetService("VirtualUser")
                local LocalPlayer = Players.LocalPlayer

                local targetPlayer = Players:FindFirstChild(selectedPlayer)
                if not targetPlayer then return end

                local function ClearTools()
                    pcall(function()
                        ReplicatedStorage.RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                        ReplicatedStorage.RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllProps")
                    end)
                end

                local function GetMyProps()
                    local props = {}
                    local workspaceCom = workspace:FindFirstChild("WorkspaceCom")
                    if not workspaceCom then return props end
                    for _,folder in ipairs(workspaceCom:GetChildren()) do
                        for _,prop in ipairs(folder:GetChildren()) do
                            if prop.Name:find("Prop"..LocalPlayer.Name) and prop:FindFirstChild("SetCurrentCFrame") then
                                table.insert(props, prop)
                            end
                        end
                    end
                    return props
                end

                local function TeleportProps(cf)
                    for _,prop in ipairs(GetMyProps()) do
                        task.spawn(function()
                            pcall(function()
                                prop.SetCurrentCFrame:InvokeServer(cf)
                            end)
                        end)
                    end
                end

                ClearTools()
                task.wait(0.2)
                local char = LocalPlayer.Character
                if not char then return end
                local hrp = char:WaitForChild("HumanoidRootPart")
                local humanoid = char:WaitForChild("Humanoid")
                
                ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "PropMaker")
                local tool = LocalPlayer.Backpack:WaitForChild("PropMaker", 5)
                if tool then
                    humanoid:EquipTool(tool)
                    task.wait(0.3)
                    local reqArgs = {"RequestingPropName", "FurnitureBleachers", "Furniture"}
                    ReplicatedStorage.RE:FindFirstChild("1Clea1rTool1s"):FireServer(unpack(reqArgs))
                    task.wait(0.5)
                    local toolRemote = tool:FindFirstChild("Tool_PropMake")
                    if toolRemote then
                        toolRemote:FireServer(workspace.Model.Street.Street, hrp.Position + Vector3.new(0, -15, 0))
                    end
                    VirtualUser:Button1Down(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
                    task.wait(0.1)
                    VirtualUser:Button1Up(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
                end

                local wasSitting = false
                local liftOffset = -10
                local destinationCF = CFrame.new(216, -1338, -477) -- CFrame original de Kill do Prop
                
                local connection
                local startTime = tick()
                
                connection = RunService.Heartbeat:Connect(function()
                    local c = targetPlayer.Character
                    local r = c and c:FindFirstChild("HumanoidRootPart")
                    local h = c and c:FindFirstChild("Humanoid")
                    
                    if not r or not h or (tick() - startTime > 12) then 
                        if connection then connection:Disconnect() end
                        ClearTools()
                        return 
                    end
                    
                    if h.Sit then
                        if not wasSitting then
                            wasSitting = true
                            TeleportProps(destinationCF)
                            task.wait(0.4)
                            if connection then connection:Disconnect() end
                            ClearTools()
                        end
                    else
                        wasSitting = false
                        liftOffset = liftOffset + 0.5
                        if liftOffset > 2 then liftOffset = -10 end
                        TeleportProps(r.CFrame * CFrame.new(0, liftOffset, 0))
                    end
                end)
            end)

        else
            warn("Nenhum método foi selecionado no Dropdown!")
        end
    end
})




-- 🚀 BOTÃO FLING COMPLETO E EXTRAÍDO
Tab3:AddButton({
    Name = "Fling",
    Description = "",
    Callback = function()
        if not selectedFlingMethod then
            warn("Nenhum fling selecionado!")
            CreateNotification("Notificação", "Escolha um método de Fling antes!", 3)
            return
        end

        if not selectedPlayer then
            warn("Nenhum jogador selecionado!")
            CreateNotification("Notificação", "Escolha um jogador antes!", 3)
            return
        end

        ----------------------------------------------------------------------------------------------------
        -- 🚌 MÉTODO: ÔNIBUS (Retirado do Script 1)
        ----------------------------------------------------------------------------------------------------
        if selectedFlingMethod == "ônibus" then
            local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
            if not targetPlayer or not targetPlayer.Character then return end

            local character = game:GetService("Players").LocalPlayer.Character or game:GetService("Players").LocalPlayer.CharacterAdded:Wait()
            local rootPart = character:WaitForChild("HumanoidRootPart")
            local humanoid = character:WaitForChild("Humanoid")
            local spawnPlace = CFrame.new(82.657265, 6.133477, -1368.286011)

            rootPart.CFrame = spawnPlace
            task.wait(2)

            game:GetService("ReplicatedStorage"):WaitForChild("RE"):WaitForChild("1Ca1r"):FireServer("PickingCar", "Bus", "Work")
            task.wait(3)

            local bus = workspace.Vehicles:FindFirstChild(game:GetService("Players").LocalPlayer.Name .. "Car")
            if bus then
                local seat = bus:FindFirstChild("Seats") and bus.Seats:FindFirstChild("VehicleSeat")
                if seat then
                    seat:Sit(humanoid)
                    repeat task.wait() until humanoid.Sit
                end

                local tChar = targetPlayer.Character
                local tRoot = tChar:FindFirstChild("HumanoidRootPart")
                local tHum = tChar:FindFirstChildOfClass("Humanoid")

                if tRoot and tHum then
                    local searchTimer = tick()
                    while tHum.Health > 0 and not tHum.Sit and (tick() - searchTimer) < 15 do
                        task.wait()
                        local time = tick() * 60
                        bus:PivotTo(tRoot.CFrame * CFrame.new(math.sin(time)*5, 0, math.cos(time)*5) * CFrame.Angles(0, time, 0))
                    end

                    if tHum.Sit then
                        local extremeSkyPos = CFrame.new(tRoot.Position.X, 999999, tRoot.Position.Z)
                        bus:PivotTo(extremeSkyPos)
                        task.wait(0.5)

                        local flingTimer = tick()
                        while (tick() - flingTimer) < 10 do
                            game:GetService("RunService").Heartbeat:Wait()
                            local randRotation = CFrame.Angles(math.rad(math.random(-10000, 10000)), math.rad(math.random(-10000, 10000)), math.rad(math.random(-10000, 10000)))
                            bus:PivotTo(extremeSkyPos * randRotation)
                        end
                    end
                end

                task.wait(0.1)
                humanoid.Health = 0
            end

        ----------------------------------------------------------------------------------------------------
        -- 🛋️ MÉTODO: SOFÁ (Retirado do Script 3 - Fling Couch)
        ----------------------------------------------------------------------------------------------------
        elseif selectedFlingMethod == "sofa" then
            local Players = game:GetService("Players")
            local LocalPlayer = Players.LocalPlayer
            local cam = workspace.CurrentCamera

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

        ----------------------------------------------------------------------------------------------------
        -- 📦 MÉTODO: PROP (Retirado do Script 2 - Fling Prop)
        ----------------------------------------------------------------------------------------------------
        elseif selectedFlingMethod == "prop" then
            local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
            if not targetPlayer then return end

            pcall(function()
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllProps")
            end)
            task.wait(0.2)

            local char = game:GetService("Players").LocalPlayer.Character
            if not char then return end
            local hrp = char:WaitForChild("HumanoidRootPart")
            local humanoid = char:WaitForChild("Humanoid")
            
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "PropMaker")
            local tool = game:GetService("Players").LocalPlayer.Backpack:WaitForChild("PropMaker", 5)
            if tool then
                humanoid:EquipTool(tool)
                task.wait(0.3)
                local reqArgs = {"RequestingPropName", "FurnitureBleachers", "Furniture"}
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer(unpack(reqArgs))
                task.wait(0.5)
                local toolRemote = tool:FindFirstChild("Tool_PropMake")
                if toolRemote then
                    toolRemote:FireServer(workspace.Model.Street.Street, hrp.Position + Vector3.new(0, -15, 0))
                end
                game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
                task.wait(0.1)
                game:GetService("VirtualUser"):Button1Up(Vector2.new(0, 500), workspace.CurrentCamera.CFrame)
            end

            local wasSitting = false
            local liftOffset = -10
            local destinationCF = CFrame.new(1082537, 81322368, -4719626)

            local startTime = tick()
            while tick() - startTime < 10 and targetPlayer.Character do
                game:GetService("RunService").Heartbeat:Wait()
                local c = targetPlayer.Character
                local r = c and c:FindFirstChild("HumanoidRootPart")
                local h = c and c:FindFirstChild("Humanoid")
                if not r or not h then break end
                
                if h.Sit then
                    if not wasSitting then
                        wasSitting = true
                        local props = {}
                        local wCom = workspace:FindFirstChild("WorkspaceCom")
                        if wCom then
                            for _,f in ipairs(wCom:GetChildren()) do
                                for _,prop in ipairs(f:GetChildren()) do
                                    if prop.Name:find("Prop"..game:GetService("Players").LocalPlayer.Name) and prop:FindFirstChild("SetCurrentCFrame") then
                                        pcall(function() prop.SetCurrentCFrame:InvokeServer(destinationCF) end)
                                    end
                                end
                            end
                        end
                        task.wait(0.4)
                        pcall(function()
                            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllTools")
                            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer("ClearAllProps")
                        end)
                        break
                    end
                else
                    wasSitting = false
                    liftOffset = liftOffset + 0.5
                    if liftOffset > 2 then liftOffset = -10 end
                    local props = {}
                    local wCom = workspace:FindFirstChild("WorkspaceCom")
                    if wCom then
                        for _,f in ipairs(wCom:GetChildren()) do
                            for _,prop in ipairs(f:GetChildren()) do
                                if prop.Name:find("Prop"..game:GetService("Players").LocalPlayer.Name) and prop:FindFirstChild("SetCurrentCFrame") then
                                    pcall(function() prop.SetCurrentCFrame:InvokeServer(r.CFrame * CFrame.new(0, liftOffset, 0)) end)
                                end
                            end
                        end
                    end
                end
            end

        ----------------------------------------------------------------------------------------------------
        -- ⚽ MÉTODO: BOLA (Retirado do Script 3 - Fling Ball)
        ----------------------------------------------------------------------------------------------------
        elseif selectedFlingMethod == "bola" then
            local Players = game:GetService("Players")
            local ReplicatedStorage = game:GetService("ReplicatedStorage")
            local Workspace = game:GetService("Workspace")

            local player = Players.LocalPlayer
            local targetPlayer = Players:FindFirstChild(selectedPlayer)

            if not targetPlayer or not targetPlayer.Character then return end

            local character = player.Character or player.CharacterAdded:Wait()
            local backpack = player:WaitForChild("Backpack")
            local ServerBalls = Workspace:WaitForChild("WorkspaceCom"):WaitForChild("001_SoccerBalls")

            if not backpack:FindFirstChild("SoccerBall") and not character:FindFirstChild("SoccerBall") then
                ReplicatedStorage.RE:FindFirstChild("1Too1l"):InvokeServer("PickingTools", "SoccerBall")
            end

            repeat task.wait() until backpack:FindFirstChild("SoccerBall") or character:FindFirstChild("SoccerBall")

            local ballTool = backpack:FindFirstChild("SoccerBall")
            if ballTool then ballTool.Parent = character end

            repeat task.wait() until ServerBalls:FindFirstChild("Soccer" .. player.Name)
            local Ball = ServerBalls:FindFirstChild("Soccer" .. player.Name)

            Ball.CanCollide = false
            Ball.Massless = true
            Ball.CustomPhysicalProperties = PhysicalProperties.new(0.0001, 0, 0)

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


            force:Destroy()
            angular:Destroy()
        else
            warn("Fling não encontrado!")
        end
    end
})


Tab3:AddSection({Name = "Outros"})

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

        if bool then
            if not selectedPlayer then
                warn("Nenhum jogador selecionado!")
                return false
            end

            humanoid.Sit = true

            -- Anti fling
            humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
            humanoidRootPart.AssemblyAngularVelocity = Vector3.zero

            if headSitConnection then
                headSitConnection:Disconnect()
            end

            headSitConnection = RunService.Heartbeat:Connect(function()
                -- Atualiza o alvo em tempo real
                local targetPlayer = Players:FindFirstChild(selectedPlayer)

                if targetPlayer
                    and targetPlayer.Character
                    and targetPlayer.Character:FindFirstChild("Head") then

                    -- Continua sentado mesmo se apertar espaço
                    if not humanoid.Sit then
                        humanoid.Sit = true
                    end

                    local head = targetPlayer.Character.Head

                    humanoidRootPart.CFrame =
                        head.CFrame * CFrame.new(0, 1.6, 0.4)

                    -- Anti fling
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
            if headSitConnection then
                headSitConnection:Disconnect()
                headSitConnection = nil
            end

            humanoid.Sit = false
            humanoidRootPart.AssemblyLinearVelocity = Vector3.zero
            humanoidRootPart.AssemblyAngularVelocity = Vector3.zero
        end
    end
})


Tab3:AddButton({
    Name = "Colocar Banana no Player",
    Callback = function()
        if selectedPlayer and selectedPlayer ~= "..." and selectedPlayer ~= "Selecionar Jogador" then
            
            local targetPlayer = game:GetService("Players"):FindFirstChild(selectedPlayer)
            
            if targetPlayer and targetPlayer.Character then
                local TargetRoot = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
                local LocalPlayer = game:GetService("Players").LocalPlayer
                local MyCharacter = LocalPlayer.Character
                local MyRoot = MyCharacter and MyCharacter:FindFirstChild("HumanoidRootPart")
                local Humanoid = MyCharacter and MyCharacter:FindFirstChildOfClass("Humanoid")
                
                if TargetRoot and MyRoot and Humanoid then
                    
                    -- 🎥 LÓGICA DO VIEW TEMPORÁRIO (Se o Toggle de View contínua não estiver ativo)
                    if not viewing then
                        local targetHumanoid = targetPlayer.Character:FindFirstChildOfClass("Humanoid")
                        if targetHumanoid then
                            task.spawn(function()
                                local cam = workspace.CurrentCamera
                                cam.CameraSubject = targetHumanoid
                                ShowPlayerNotification(targetPlayer) -- Dispara a sua notificação visual personalizada
                                
                                task.wait(3) -- Mantém visualizando por 3 segundos
                                
                                -- Restaura a câmera para o seu personagem apenas se o toggle contínuo não tiver sido ligado nesse meio tempo
                                if not viewing and MyCharacter and MyCharacter:FindFirstChildOfClass("Humanoid") then
                                    cam.CameraSubject = MyCharacter:FindFirstChildOfClass("Humanoid")
                                end
                            end)
                        end
                    end
                    
                    -- 1. FUNÇÃO INTERNA PARA BUSCAR A TOOL NO INVENTÁRIO OU NA MÃO
                    local function obterPeelTool()
                        local tool = nil
                        if LocalPlayer:FindFirstChild("Backpack") then
                            tool = LocalPlayer.Backpack:FindFirstChild("Minions2026_BananaPeel")
                        end
                        if not tool and MyCharacter then
                            tool = MyCharacter:FindFirstChild("Minions2026_BananaPeel")
                        end
                        return tool
                    end

                    local PeelTool = obterPeelTool()

                    -- 2. SE NÃO TIVER A TOOL, SOLICITA AO SERVIDOR E AGUARDA APARECER
                    if not PeelTool then
                        local args = {
                            [1] = "AcceptedToolToServer",
                            [2] = "Minions2026_BananaPeel",
                            [3] = LocalPlayer
                        }
                        
                        local triggerEvent = game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t")
                        if triggerEvent then
                            triggerEvent:FireServer(unpack(args))
                            
                            -- Aguarda a ferramenta chegar na mochila por até 2 segundos
                            local timeout = 0
                            while not PeelTool and timeout < 40 do
                                timeout = timeout + 1
                                task.wait(0.05)
                                PeelTool = obterPeelTool()
                            end
                        end
                    end

                    -- 3. EXECUTA A LÓGICA SE A FERRAMENTA ESTIVER DISPONÍVEL
                    if PeelTool then
                        local RemotesLib = nil
                        pcall(function()
                            RemotesLib = require(game:GetService("ReplicatedStorage").Packages.Remotes)
                        end)

                        if RemotesLib and RemotesLib.fireServerComponent then
                            pcall(function()
                                -- Garante que a ferramenta está equipada na mão
                                if PeelTool.Parent ~= MyCharacter then
                                    Humanoid:EquipTool(PeelTool)
                                    task.wait(0.05)
                                end

                                local TargetPosition = TargetRoot.Position - Vector3.new(0, 3, 0)
                                local distancia = (MyRoot.Position - TargetRoot.Position).Magnitude
                                
                                -- Se estiver longe (mais de 30 studs), teleporta com segurança por baixo
                                if distancia > 30 then
                                    local originalCFrame = MyRoot.CFrame
                                    
                                    local bV = Instance.new("BodyVelocity")
                                    bV.Velocity = Vector3.new(0, 0, 0)
                                    bV.MaxForce = Vector3.new(0, math.huge, 0)
                                    bV.Parent = MyRoot
                                    
                                    MyRoot.CFrame = TargetRoot.CFrame * CFrame.new(0, -14, 0)
                                    task.wait(0.35)
                                    
                                    RemotesLib.fireServerComponent(PeelTool, "PlaceBananaPeel", TargetPosition)
                                    task.wait(0.10)
                                    
                                    MyRoot.CFrame = originalCFrame
                                    bV:Destroy()
                                else
                                    RemotesLib.fireServerComponent(PeelTool, "PlaceBananaPeel", TargetPosition)
                                end
                            end)
                        else
                            warn("Biblioteca de Remotes nativa não encontrada.")
                        end
                    else
                        warn("Não foi possível puxar ou encontrar a casca de banana.")
                    end
                    
                end
            end
        else
            warn("Nenhum jogador válido selecionado no dropdown.")
        end
    end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Antis-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

local Tab4= Window:MakeTab({ "| Antis", "shield" })

local antiSitEnabled = false
local antiSitLoop

Tab4:AddToggle({
    Name = "Anti-Sit",
    Description = "Impede o jogador de sentar",
    Default = false,
    Callback = function(state)
        antiSitEnabled = state

        if state then
            antiSitLoop = task.spawn(function()
                while antiSitEnabled do
                    local character = game.Players.LocalPlayer.Character

                    if character then
                        local humanoid = character:FindFirstChildOfClass("Humanoid")

                        if humanoid then
                            humanoid:SetStateEnabled(Enum.HumanoidStateType.Seated, false)

                            if humanoid.Sit then
                                humanoid.Sit = false
                                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
                            end
                        end
                    end

                    task.wait()
                end
            end)
        else
            local character = game.Players.LocalPlayer.Character

            if character then
                local humanoid = character:FindFirstChildOfClass("Humanoid")

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


local doorParts = {}
local doorConnection

local function isDoor(obj)
    local name = obj.Name:lower()
    return name:find("door") or name:find("porta")
end

local function setDoorNoclip(obj, state)
    if obj:IsA("BasePart") then
        doorParts[obj] = true
        obj.CanCollide = not state
    end

    for _, v in ipairs(obj:GetDescendants()) do
        if v:IsA("BasePart") then
            doorParts[v] = true
            v.CanCollide = not state
        end
    end
end

local function applyDoorNoclip(state)
    for _, obj in ipairs(workspace:GetDescendants()) do
        if isDoor(obj) then
            setDoorNoclip(obj, state)
        end
    end
end

Tab4:AddToggle({
    Name = "Noclip Portas / Anti Fling Portas",
    Description = "As portas não vão mais te empurrar!",
    Default = false,
    Callback = function(Value)

        applyDoorNoclip(Value)

        if Value then
            doorConnection = workspace.DescendantAdded:Connect(function(obj)
                if isDoor(obj) then
                    task.wait()
                    setDoorNoclip(obj, true)
                end
            end)
        else
            for part in pairs(doorParts) do
                if part and part.Parent then
                    part.CanCollide = true
                end
            end

            table.clear(doorParts)

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

local BananaConnection

Tab4:AddToggle({
    Name = "Anti Bananas",
    Default = false,
    Callback = function(Value)
        if Value then
            -- Remove as bananas que já existem
            for _, v in ipairs(workspace:GetChildren()) do
                if v.Name:match("^BananaPeel_") then
                    local touch = v:FindFirstChild("Touch")
                    if touch then
                        touch:Destroy()
                    end
                end
            end

            -- Detecta novas bananas
            BananaConnection = workspace.ChildAdded:Connect(function(v)
                if v.Name:match("^BananaPeel_") then
                    local touch = v:WaitForChild("Touch", 3)
                    if touch then
                        touch:Destroy()
                    end
                end
            end)

        else
            -- Para de detectar quando desligar
            if BananaConnection then
                BananaConnection:Disconnect()
                BananaConnection = nil
            end
        end
    end
})


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Avatar---------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab5= Window:MakeTab({ "| Avatar", "shirt" })

local DropdownJogadoresAvatar
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local SelectedPlayerAvatar = nil -- Armazena o jogador selecionado para o avatar

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
    frame.BackgroundColor3 = Color3.fromRGB(27, 5, 25)
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
    close.TextColor3 = Color3.fromRGB(255, 255, 255)
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

-- 👥 LISTA DE PLAYERS
local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

Tab5:AddButton({
    Name = "Click Player Avatar",
    Callback = function()

        local backpack = LocalPlayer:WaitForChild("Backpack")

        -- remove tool antiga
        if backpack:FindFirstChild("SelecionarPlayerAvatar") then
            backpack.SelecionarPlayerAvatar:Destroy()
        end

        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("SelecionarPlayer") then
            LocalPlayer.Character.SelecionarPlayer:Destroy()
        end

        local Tool = Instance.new("Tool")
        Tool.Name = "SelecionarPlayerAvatar"
        Tool.RequiresHandle = false
        Tool.CanBeDropped = false
        Tool.TextureId = "rbxassetid://10734952036"
        Tool.Parent = backpack

        local Mouse = LocalPlayer:GetMouse()

        Tool.Activated:Connect(function()
            local Target = Mouse.Target
            if not Target then return end

            local Character = Target:FindFirstAncestorOfClass("Model")
            if not Character then return end

            local Player = Players:GetPlayerFromCharacter(Character)
            if not Player or Player == LocalPlayer then return end

            -- 🔥 variável correta
            SelectedPlayerAvatar = Player.Name

            -- 🔥 atualiza dropdown corretamente
            if DropdownJogadoresAvatar then
                DropdownJogadoresAvatar:Set(Player.Name)
            end

            CreateNotification(
                "Notificação",
                "Player selecionado: " .. Player.Name,
                3
            )
        end)
    end
})



-- 🎯 DROPDOWN DE TARGET (Alterado para AddDropdownPlayer e Tab5)
DropdownJogadoresAvatar = Tab5:AddDropdownPlayer({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = "...",
    Callback = function(Value)
        SelectedPlayerAvatar = Value -- define a sua variável
        print("Alvo selecionado: " .. tostring(SelectedPlayerAvatar))

        -- Evita notificações duplicadas/vazias ao resetar
        if Value and Value ~= "..." and Value ~= "Selecionar Jogador" then
            CreateNotification("Notificação", "Player selecionado: "..Value, 3)
        end
    end
})

-- 🔁 ATUALIZAÇÃO AUTOMÁTICA SUPER CLEAN
local function UpdateDropdown()
    task.wait(0.3) -- Pequena folga para o motor do Roblox processar
    if DropdownJogadoresAvatar then
        local nomesAtualizados = GetPlayerNames()
        
        -- Atualiza a lista nativamente pela nova função sem bugar o texto visível!
        DropdownJogadoresAvatar:Set(nomesAtualizados)
    end
end

-- CONEXÕES DOS EVENTOS
Players.PlayerAdded:Connect(UpdateDropdown)

Players.PlayerRemoving:Connect(function(plr)
    -- Se o jogador que saiu era quem você estava de olho
    if SelectedPlayerAvatar and plr.Name == SelectedPlayerAvatar then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
        SelectedPlayerAvatar = nil
    end

    UpdateDropdown()
end)


-- Dropdown para escolher o tipo de corpo para o reset
Tab5:AddDropdown({
    Name = "Tipo de Corpo",
    Description = "Selecione o corpo base para carregar a skin",
    Options = {"Corpo Normal", "Corpo Normal Esticado", "Corpo Alto Fino"},
    Default = "Corpo Normal",
    Flag = "body_type_dropdown",
    Callback = function(Value)
        -- Armazena globalmente a opção selecionada
        _G.SelectedBodyType = Value
        print("Corpo selecionado: " .. Value)
    end
})


Tab5:AddButton({
    Name = "Copiar Avatar",
    Callback = function()

        if not SelectedPlayerAvatar then
            CreateNotification("Aviso", "Nenhum jogador selecionado", 4)
            return
        end

        local Players = game:GetService("Players")
        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local Remotes = ReplicatedStorage:WaitForChild("Remotes")

        local LP = Players.LocalPlayer
        local LChar = LP.Character or LP.CharacterAdded:Wait()

        local TPlayer = Players:FindFirstChild(SelectedPlayerAvatar)
        if not TPlayer then
            CreateNotification("Erro", "Jogador não encontrado", 4)
            return
        end

        local TChar = TPlayer.Character or TPlayer.CharacterAdded:Wait()
        if not TChar then
            CreateNotification("Erro", "Character do alvo não carregado", 4)
            return
        end

        local LHumanoid = LChar:FindFirstChildOfClass("Humanoid")
        local THumanoid = TChar:FindFirstChildOfClass("Humanoid")

        if not LHumanoid or not THumanoid then
            CreateNotification("Erro", "Humanoid não encontrado", 4)
            return
        end

        -- Função auxiliar para vestir itens com delay
        local function SafeWear(assetId)
            if not assetId or assetId == 0 or assetId == "0" then return end
            pcall(function()
                Remotes.Wear:InvokeServer(tonumber(assetId))
            end)
            task.wait(0.35) -- Delay de segurança anti rate limit do Brookhaven
        end

        -- ==========================================
        -- 1. CAPTURAR OS DADOS DO ALVO NO INÍCIO
        -- ==========================================
        local PDesc = THumanoid:GetAppliedDescription()
        
        -- Guardar os IDs planejados originais em uma tabela
        local targetIDs = {}
        local function addTargetId(id)
            if id and tonumber(id) and tonumber(id) ~= 0 then
                targetIDs[tonumber(id)] = true
            end
        end

        -- Coletar IDs originais (Roupas, Rosto e Acessórios)
        addTargetId(PDesc.Shirt)
        addTargetId(PDesc.Pants)
        addTargetId(PDesc.Face)
        
        local targetAccessories = PDesc:GetAccessories(true)
        for _, acc in ipairs(targetAccessories) do
            addTargetId(acc.AssetId)
        end

        -- ==========================================
        -- 2. RESETAR O LOCALPLAYER COM O CORPO SELECIONADO
        -- ==========================================
        
        -- Tabela de corpos e seus respectivos códigos correspondentes
        local bodyCodes = {
            ["Corpo Normal"]          = "BH-AE-0f8f8960d421497695b6c7f81888d9a6",
            ["Corpo Normal Esticado"] = "BH-AE-6d902b983af44f819336326f3c5f0a2c",
            ["Corpo Alto Fino"]       = "BH-AE-7dd15b77d3834f81ac83bc309f919d1a"
        }

        -- Recupera a escolha do dropdown. Se estiver vazia, usa "Corpo Normal" por padrão.
        local chosenBody = _G.SelectedBodyType or "Corpo Normal"
        local code = bodyCodes[chosenBody] or "BH-AE-98069945232645a5a4c827bb7eb2f2bb"

        task.spawn(function()
            pcall(function()
                Remotes.AvatarEditorOutfitCodes:InvokeServer("Load", code)
            end)
        end)

        task.wait(4) -- Tempo para a limpeza do reset terminar

        -- ==========================================
        -- 3. PRIMEIRA TENTATIVA DE EQUIPAR (ROUPAS & ACESSÓRIOS)
        -- ==========================================
        
        -- Corpo/Package
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
        pcall(function()
            Remotes.ChangeCharacterBody:InvokeServer(unpack(argsBody))
        end)
        task.wait(0.5)

        -- Roupas e Rosto clássicos
        if targetIDs[tonumber(PDesc.Shirt)] then SafeWear(PDesc.Shirt) end
        if targetIDs[tonumber(PDesc.Pants)] then SafeWear(PDesc.Pants) end
        if targetIDs[tonumber(PDesc.Face)] then SafeWear(PDesc.Face) end

        -- Acessórios
        for _, acc in ipairs(targetAccessories) do
            if acc.AssetId then
                SafeWear(acc.AssetId)
            end
        end

        -- Cor da Pele
        local SkinColor = TChar:FindFirstChild("Body Colors")
        if SkinColor then
            pcall(function()
                Remotes.ChangeBodyColor:FireServer(tostring(SkinColor.HeadColor))
            end)
            task.wait(0.3)
        end

        -- ==========================================
        -- FUNÇÃO DE REVISÃO REUTILIZÁVEL (DOUBLE-CHECK)
        -- ==========================================
        local function RunRevision(revisionNumber)
            local checkTChar = TPlayer.Character
            local checkTHumanoid = checkTChar and checkTChar:FindFirstChildOfClass("Humanoid")
            
            if not checkTHumanoid then return false end
            
            local NewPDesc = checkTHumanoid:GetAppliedDescription()
            
            -- Gerar lista atual de IDs do Alvo para conferência
            local currentTargetIDs = {}
            local function addCurrentId(id)
                if id and tonumber(id) and tonumber(id) ~= 0 then
                    currentTargetIDs[tonumber(id)] = true
                end
            end

            addCurrentId(NewPDesc.Shirt)
            addCurrentId(NewPDesc.Pants)
            addCurrentId(NewPDesc.Face)
            for _, acc in ipairs(NewPDesc:GetAccessories(true)) do
                addCurrentId(acc.AssetId)
            end

            -- Analisar diferença entre a lista inicial e a lista de agora
            local totalOriginalItems = 0
            local matchingItems = 0

            for id, _ in pairs(targetIDs) do
                totalOriginalItems = totalOriginalItems + 1
                if currentTargetIDs[id] then
                    matchingItems = matchingItems + 1
                end
            end

            local matchRatio = totalOriginalItems > 0 and (matchingItems / totalOriginalItems) or 1

            -- Se o alvo mudou mais de 40% da skin, cancelamos a revisão
            if matchRatio < 0.6 then
                warn("Revisão " .. revisionNumber .. " abortada: O jogador mudou de skin.")
                return false
            end

            -- Se a skin for compatível, reequipamos apenas o que faltou em você
            local LDesc = LHumanoid:GetAppliedDescription()
            local myEquipped = {}
            local function addMyId(id)
                if id and tonumber(id) and tonumber(id) ~= 0 then
                    myEquipped[tonumber(id)] = true
                end
            end

            addMyId(LDesc.Shirt)
            addMyId(LDesc.Pants)
            addMyId(LDesc.Face)
            for _, acc in ipairs(LDesc:GetAccessories(true)) do
                addMyId(acc.AssetId)
            end

            local missingItemsFound = false
            for id, _ in pairs(targetIDs) do
                if not myEquipped[id] then
                    missingItemsFound = true
                    print("Revisão " .. revisionNumber .. ": Tentando reequipar item faltando (ID: " .. tostring(id) .. ")...")
                    SafeWear(id)
                end
            end

            return true
        end

        -- ==========================================
        -- EXECUÇÃO DAS REVISÕES 2 E 3
        -- ==========================================
        task.wait(1.5) -- Pausa antes da Segunda Revisão
        RunRevision(2)

        task.wait(1.5) -- Pausa antes da Terceira Revisão
        RunRevision(3)

        -- ==========================================
        -- 4. COPIAR E APLICAR AS ANIMAÇÕES (NO FINAL)
        -- ==========================================
        local Animations = {
            PDesc.IdleAnimation, PDesc.WalkAnimation, PDesc.RunAnimation,
            PDesc.JumpAnimation, PDesc.FallAnimation, PDesc.ClimbAnimation, PDesc.SwimAnimation
        }
        for _, anim in ipairs(Animations) do
            if tonumber(anim) and anim ~= 0 then
                SafeWear(anim)
            end
        end

        -- ==========================================
        -- 5. NOTIFICAÇÃO DE FINALIZAÇÃO
        -- ==========================================
        CreateNotification(
            "Sucesso",
            "Avatar de " .. SelectedPlayerAvatar .. " Copiado Com Sucesso!",
            4
        )

    end
})

Tab5:AddButton({
    Name = "Copiar Avatar Roblox",
    Callback = function()

        if not SelectedPlayerAvatar then
            CreateNotification("Aviso", "Nenhum jogador selecionado", 4)
            return
        end

        local Players = game:GetService("Players")
        local ReplicatedStorage = game:GetService("ReplicatedStorage")
        local Remotes = ReplicatedStorage:WaitForChild("Remotes")

        local LP = Players.LocalPlayer
        local LChar = LP.Character or LP.CharacterAdded:Wait()

        local TPlayer = Players:FindFirstChild(SelectedPlayerAvatar)
        if not TPlayer then
            CreateNotification("Erro", "Jogador não encontrado", 4)
            return
        end

        local LHumanoid = LChar:FindFirstChildOfClass("Humanoid")
        if not LHumanoid then
            CreateNotification("Erro", "Seu Humanoid não foi encontrado", 4)
            return
        end

        -- Função auxiliar para vestir itens com delay seguro
        local function SafeWear(assetId)
            if not assetId or assetId == 0 or assetId == "0" then return end
            pcall(function()
                Remotes.Wear:InvokeServer(tonumber(assetId))
            end)
            task.wait(0.35)
        end

        -- ==========================================
        -- 1. PUXAR O AVATAR DO PERFIL DA ROBLOX
        -- ==========================================
        local success, PDesc = pcall(function()
            return Players:GetHumanoidDescriptionFromUserId(TPlayer.UserId)
        end)

        if not success or not PDesc then
            CreateNotification("Erro", "Não foi possível carregar o avatar original do Roblox", 4)
            return
        end

        -- Guardar os IDs originais em uma tabela
        local targetIDs = {}
        local function addTargetId(id)
            if id and tonumber(id) and tonumber(id) ~= 0 then
                targetIDs[tonumber(id)] = true
            end
        end

        addTargetId(PDesc.Shirt)
        addTargetId(PDesc.Pants)
        addTargetId(PDesc.Face)
        
        local targetAccessories = PDesc:GetAccessories(true)
        for _, acc in ipairs(targetAccessories) do
            addTargetId(acc.AssetId)
        end

        -- ==========================================
        -- 2. RESETAR O LOCALPLAYER COM O CORPO DO DROPDOWN
        -- ==========================================
        local bodyCodes = {
            ["Corpo Normal"]          = "BH-AE-0f8f8960d421497695b6c7f81888d9a6",
            ["Corpo Normal Esticado"] = "BH-AE-6d902b983af44f819336326f3c5f0a2c",
            ["Corpo Alto Fino"]       = "BH-AE-7dd15b77d3834f81ac83bc309f919d1a"
        }

        local chosenBody = _G.SelectedBodyType or "Corpo Normal"
        local code = bodyCodes[chosenBody] or "BH-AE-98069945232645a5a4c827bb7eb2f2bb"

        task.spawn(function()
            pcall(function()
                Remotes.AvatarEditorOutfitCodes:InvokeServer("Load", code)
            end)
        end)

        task.wait(4) -- Tempo para a limpeza do reset terminar

        -- ==========================================
        -- 3. PRIMEIRA TENTATIVA DE EQUIPAR (ROBLOX ORIGINAL)
        -- ==========================================
        
        -- Corpo/Package
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
        pcall(function()
            Remotes.ChangeCharacterBody:InvokeServer(unpack(argsBody))
        end)
        task.wait(0.5)

        -- Roupas e Rosto clássicos do Roblox
        if targetIDs[tonumber(PDesc.Shirt)] then SafeWear(PDesc.Shirt) end
        if targetIDs[tonumber(PDesc.Pants)] then SafeWear(PDesc.Pants) end
        if targetIDs[tonumber(PDesc.Face)] then SafeWear(PDesc.Face) end

        -- Acessórios do Roblox
        for _, acc in ipairs(targetAccessories) do
            if acc.AssetId then
                SafeWear(acc.AssetId)
            end
        end

        -- Cor da Pele Original do Perfil
        pcall(function()
            -- No Brookhaven, a cor da pele é enviada como string de uma cor BrickColor ou similar.
            -- Convertemos o HeadColor (Color3) original do Roblox para o remote mudar
            local skinBrickColor = BrickColor.new(PDesc.HeadColor)
            Remotes.ChangeBodyColor:FireServer(tostring(skinBrickColor))
        end)
        task.wait(0.3)

        -- ==========================================
        -- FUNÇÃO DE REVISÃO REUTILIZÁVEL (DOUBLE-CHECK)
        -- ==========================================
        local function RunRevision(revisionNumber)
            -- Como o avatar vem direto da API da Roblox, não precisamos verificar se o alvo "mudou de skin no Brookhaven".
            -- A lista de destino `targetIDs` é sempre a original e imutável do perfil dele.
            
            local LDesc = LHumanoid:GetAppliedDescription()
            local myEquipped = {}
            local function addMyId(id)
                if id and tonumber(id) and tonumber(id) ~= 0 then
                    myEquipped[tonumber(id)] = true
                end
            end

            addMyId(LDesc.Shirt)
            addMyId(LDesc.Pants)
            addMyId(LDesc.Face)
            for _, acc in ipairs(LDesc:GetAccessories(true)) do
                addMyId(acc.AssetId)
            end

            local missingItemsFound = false
            for id, _ in pairs(targetIDs) do
                if not myEquipped[id] then
                    missingItemsFound = true
                    print("Revisão original " .. revisionNumber .. ": Tentando reequipar item faltando (ID: " .. tostring(id) .. ")...")
                    SafeWear(id)
                end
            end

            return true
        end

        -- ==========================================
        -- EXECUÇÃO DAS REVISÕES 2 E 3
        -- ==========================================
        task.wait(1.5) -- Pausa antes da Segunda Revisão
        RunRevision(2)

        task.wait(1.5) -- Pausa antes da Terceira Revisão
        RunRevision(3)

        -- ==========================================
        -- 4. COPIAR E APLICAR AS ANIMAÇÕES (NO FINAL)
        -- ==========================================
        local Animations = {
            PDesc.IdleAnimation, PDesc.WalkAnimation, PDesc.RunAnimation,
            PDesc.JumpAnimation, PDesc.FallAnimation, PDesc.ClimbAnimation, PDesc.SwimAnimation
        }
        for _, anim in ipairs(Animations) do
            if tonumber(anim) and anim ~= 0 then
                SafeWear(anim)
            end
        end

        -- ==========================================
        -- 5. NOTIFICAÇÃO DE FINALIZAÇÃO
        -- ==========================================
        CreateNotification(
            "Sucesso",
            "Avatar  Roblox de " .. SelectedPlayerAvatar .. " copiado!",
            4
        )

    end
})




Tab5:AddSection({ "Salva skins" })


-- ============================================================================
-- SKIN MANAGER COMPLETO COM SISTEMA DE REVISÃO E GERADOR DE CÓDIGOS (TAB5)
-- ============================================================================

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local HttpService = game:GetService("HttpService")
local Remotes = ReplicatedStorage:WaitForChild("Remotes")

local FILE_NAME = "SAGAZxAvataLoad.json"
local CODES_FILE = "SAGAZxOutfitCodes.json"

local Skins = {}
local Outfits = {} -- Estrutura: { [NomeSkin] = { Code = "BH-AE-...", CreatedAt = timestamp } }

-- ==========================================
-- SISTEMA DE LEITURA E SALVAMENTO DE ARQUIVOS
-- ==========================================
local function LoadFiles()
    -- Carregar Skins Normais
    if isfile(FILE_NAME) then
        local success, result = pcall(function()
            return HttpService:JSONDecode(readfile(FILE_NAME))
        end)
        if success and type(result) == "table" then
            Skins = result
        else
            Skins = {}
        end
    else
        writefile(FILE_NAME, "{}")
    end

    -- Carregar Códigos Exportados
    if isfile(CODES_FILE) then
        local success, result = pcall(function()
            return HttpService:JSONDecode(readfile(CODES_FILE))
        end)
        if success and type(result) == "table" then
            Outfits = result
        else
            Outfits = {}
        end
    else
        writefile(CODES_FILE, "{}")
    end
end

local function SaveSkinsFile()
    writefile(FILE_NAME, HttpService:JSONEncode(Skins))
end

local function SaveCodesFile()
    writefile(CODES_FILE, HttpService:JSONEncode(Outfits))
end

LoadFiles()

-- ==========================================
-- CAPTURAR AVATAR LOCAL OU DO ALVO
-- ==========================================
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
        Animations = {
            Idle = Desc.IdleAnimation,
            Walk = Desc.WalkAnimation,
            Run = Desc.RunAnimation,
            Jump = Desc.JumpAnimation,
            Fall = Desc.FallAnimation,
            Climb = Desc.ClimbAnimation,
            Swim = Desc.SwimAnimation
        }
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
        Animations = {
            Idle = Desc.IdleAnimation,
            Walk = Desc.WalkAnimation,
            Run = Desc.RunAnimation,
            Jump = Desc.JumpAnimation,
            Fall = Desc.FallAnimation,
            Climb = Desc.ClimbAnimation,
            Swim = Desc.SwimAnimation
        }
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

-- ==========================================
-- APLICAR SKIN COM 3 REVISÕES (INCLUINDO ANIMAÇÕES)
-- ==========================================
local function AplicarSkin(data)
    if not data then return end

    local LP = Players.LocalPlayer
    local LChar = LP.Character or LP.CharacterAdded:Wait()
    local LHumanoid = LChar:FindFirstChildOfClass("Humanoid")
    if not LHumanoid then return end

    local targetIDs = {}
    local function addTargetId(id)
        if id and tonumber(id) and tonumber(id) ~= 0 then
            targetIDs[tonumber(id)] = true
        end
    end

    if data.Clothing then
        addTargetId(data.Clothing.Shirt)
        addTargetId(data.Clothing.Pants)
        addTargetId(data.Clothing.Face)
    end
    if data.Accessories then
        for _, id in ipairs(data.Accessories) do
            addTargetId(id)
        end
    end

    local function SafeWear(assetId)
        if not assetId or assetId == 0 or assetId == "0" then return end
        pcall(function()
            Remotes.Wear:InvokeServer(tonumber(assetId))
        end)
        task.wait(0.35)
    end

    -- Usa o tipo de corpo selecionado no Dropdown da UI
    local bodyCodes = {
        ["Corpo Normal"]          = "BH-AE-0f8f8960d421497695b6c7f81888d9a6",
        ["Corpo Normal Esticado"] = "BH-AE-6d902b983af44f819336326f3c5f0a2c",
        ["Corpo Alto Fino"]       = "BH-AE-7dd15b77d3834f81ac83bc309f919d1a"
    }
    local chosenBody = _G.SelectedBodyTypeSkinManager or "Corpo Normal"
    local code = bodyCodes[chosenBody] or "BH-AE-0f8f8960d421497695b6c7f81888d9a6"

    task.spawn(function()
        pcall(function()
            Remotes.AvatarEditorOutfitCodes:InvokeServer("Load", code)
        end)
    end)
    task.wait(4)

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
        pcall(function()
            Remotes.ChangeCharacterBody:InvokeServer(unpack(argsBody))
        end)
        task.wait(0.5)
    end

    if data.Clothing then
        if targetIDs[tonumber(data.Clothing.Shirt)] then SafeWear(data.Clothing.Shirt) end
        if targetIDs[tonumber(data.Clothing.Pants)] then SafeWear(data.Clothing.Pants) end
        if targetIDs[tonumber(data.Clothing.Face)] then SafeWear(data.Clothing.Face) end
    end

    if data.Accessories then
        for _, id in ipairs(data.Accessories) do
            SafeWear(id)
        end
    end

    if data.BodyColor then
        pcall(function()
            Remotes.ChangeBodyColor:FireServer(tostring(data.BodyColor))
        end)
        task.wait(0.3)
    end

    local function RunSkinManagerRevision(revisionNumber)
        local LDesc = LHumanoid:GetAppliedDescription()
        local myEquipped = {}
        local function addMyId(id)
            if id and tonumber(id) and tonumber(id) ~= 0 then
                myEquipped[tonumber(id)] = true
            end
        end

        addMyId(LDesc.Shirt)
        addMyId(LDesc.Pants)
        addMyId(LDesc.Face)
        for _, acc in ipairs(LDesc:GetAccessories(true)) do
            addMyId(acc.AssetId)
        end

        for id, _ in pairs(targetIDs) do
            if not myEquipped[id] then
                print("Correção Skin Manager (Etapa " .. revisionNumber .. "): Reequipando Item ID: " .. id)
                SafeWear(id)
            end
        end
    end

    task.wait(1.5)
    RunSkinManagerRevision(2)
    task.wait(1.5)
    RunSkinManagerRevision(3)

    if data.Animations then
        local animKeys = {"Idle", "Walk", "Run", "Jump", "Fall", "Climb", "Swim"}

        local function RunAnimationRevision(revisionStep)
            local LDesc = LHumanoid:GetAppliedDescription()
            local currentAnims = {
                Idle = LDesc.IdleAnimation,
                Walk = LDesc.WalkAnimation,
                Run = LDesc.RunAnimation,
                Jump = LDesc.JumpAnimation,
                Fall = LDesc.FallAnimation,
                Climb = LDesc.ClimbAnimation,
                Swim = LDesc.SwimAnimation
            }

            for _, key in ipairs(animKeys) do
                local savedAnim = tonumber(data.Animations[key])
                local currentAnim = tonumber(currentAnims[key])

                if savedAnim and savedAnim ~= 0 then
                    if savedAnim ~= currentAnim then
                        print("Correção Animação (Revisão " .. revisionStep .. "): Reequipando " .. key .. " (ID: " .. savedAnim .. ")")
                        SafeWear(savedAnim)
                    end
                end
            end
        end

        for _, key in ipairs(animKeys) do
            local animId = data.Animations[key]
            if tonumber(animId) and tonumber(animId) ~= 0 then
                SafeWear(animId)
            end
        end

        task.wait(1.5)
        RunAnimationRevision(2)
        task.wait(1.5)
        RunAnimationRevision(3)
    end

    CreateNotification("Sucesso", "Skin Aplicada Com Sucesso!", 4)
end

-- ==========================================
-- AUXILIARES DA INTERFACE
-- ==========================================
local function GetSkinList()
    local list = {}
    for name, _ in pairs(Skins) do
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

-- Retorna a lista de códigos com dias restantes de forma limpa (Sem expor o código)
local SelectedOutfitKey = nil
local DropdownCodes

local function GetFormattedCodesList()
    LoadFiles()
    local list = {}
    local now = os.time()
    for name, info in pairs(Outfits) do
        local elapsed = now - (info.CreatedAt or now)
        local secondsLeft = 2592000 - elapsed
        local daysLeft = math.floor(secondsLeft / 86400)
        
        if daysLeft < 0 then daysLeft = 0 end
        
        local label = string.format("%s (%d dias restantes)", name, daysLeft)
        table.insert(list, label)
    end
    table.sort(list)
    return list
end

local function RefreshCodesDropdown()
    if not DropdownCodes then return end
    local newList = GetFormattedCodesList()
    if DropdownCodes.Set then
        DropdownCodes:Set(newList)
    elseif DropdownCodes.Refresh then
        DropdownCodes:Refresh(newList, true)
    end
    SelectedOutfitKey = nil
end

-- ==========================================
-- DESIGN DA INTERFACE (TAB5)
-- ==========================================

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



-- Dropdown Principal de Tipo de Corpo
Tab5:AddDropdown({
    Name = "Tipo de Corpo (Skin Manager)",
    Description = "Selecione o corpo base para carregar a skin",
    Options = {"Corpo Normal", "Corpo Normal Esticado", "Corpo Alto Fino"},
    Default = "Corpo Normal",
    Flag = "body_type_dropdown_sm",
    Callback = function(Value)
        _G.SelectedBodyTypeSkinManager = Value
        print("Skin Manager Corpo base alterado para: " .. Value)
    end
})

-- ==========================================
-- BOTÕES DE PERSISTÊNCIA & OPERAÇÃO
-- ==========================================





-- Salvar Skin do Player Selecionado
Tab5:AddButton({
    Name = "Salvar Skin do Player Selecionado",
    Callback = function()
        if not SelectedPlayerAvatar then
            CreateNotification("Aviso", "Nenhum player selecionado.", 4)
            return
        end

        local targetPlayer = Players:FindFirstChild(SelectedPlayerAvatar)
        if not targetPlayer then
            CreateNotification("Erro", "Player não encontrado.", 4)
            return
        end

        local PlayerData = GetAvatarDataFromPlayer(targetPlayer)
        if not PlayerData then
            CreateNotification("Erro", "Erro ao extrair skin.", 4)
            return
        end

        local nomeLimpo = tostring(SkinName):gsub("^%s*(.-)%s*$", "%1")
        if nomeLimpo == "" then
            nomeLimpo = SelectedPlayerAvatar
        end

        Skins[nomeLimpo] = PlayerData
        SaveSkinsFile()
        RefreshDropdown()
        CreateNotification("Sucesso", "Skin salva como: " .. nomeLimpo, 4)
    end
})

-- Salvar Nova Skin
Tab5:AddButton({
    Name = "Salvar Skin",
    Callback = function()
        local nomeLimpo = tostring(SkinName):gsub("^%s*(.-)%s*$", "%1")
        if nomeLimpo == "" then
            CreateNotification("Aviso", "Digite um nome na TextBox.", 4)
            return
        end

        local CurrentData = GetCurrentAvatarData()
        if not CurrentData then return end

        Skins[nomeLimpo] = CurrentData
        SaveSkinsFile()
        RefreshDropdown()
        CreateNotification("Sucesso", "Skin salva: " .. nomeLimpo, 4)
    end
})

-- Carregar Skin
Tab5:AddButton({
    Name = "Carregar Skin Selecionada",
    Callback = function()
        if SelectedSkin and Skins[SelectedSkin] then
            AplicarSkin(Skins[SelectedSkin])
        else
            CreateNotification("Aviso", "Selecione uma skin na lista.", 4)
        end
    end
})

-- Salvar Skin Atual na Opção Selecionada no Dropdown
Tab5:AddButton({
    Name = "Salvar Skin Atual na Opção Selecionada",
    Callback = function()
        if not SelectedSkin then
            CreateNotification("Aviso", "Selecione uma skin na Dropdown primeiro!", 4)
            return
        end

        local CurrentData = GetCurrentAvatarData()
        if not CurrentData then return end

        Skins[SelectedSkin] = CurrentData
        SaveSkinsFile()
        CreateNotification("Sucesso", "Skin " .. SelectedSkin .. " Atualizada!", 4)
    end
})

-- Deletar Skin
Tab5:AddButton({
    Name = "Deletar Skin Selecionada",
    Callback = function()
        if SelectedSkin and Skins[SelectedSkin] then
            Skins[SelectedSkin] = nil
            SaveSkinsFile()
            SelectedSkin = nil
            RefreshDropdown()
            CreateNotification("Sucesso", "Skin deletada.", 4)
        else
            CreateNotification("Aviso", "Selecione uma skin para deletar.", 4)
        end
    end
})

-- Gerar Código da Skin Selecionada
Tab5:AddButton({
    Name = "Gerar Código da Skin Selecionada",
    Description = "Gere o Código Para o Carregamento Instantâneo",
    Callback = function()
        if not SelectedSkin or not Skins[SelectedSkin] then
            CreateNotification("Aviso", "Selecione uma skin na dropdown de skins!", 4)
            return
        end

        local skinName = SelectedSkin
        local skinData = Skins[skinName]

        CreateNotification("Processando", "Aplicando skin '" .. skinName .. "' para gerar o código...", 5)

        -- Aplica a skin selecionada usando o corpo e revisões
        AplicarSkin(skinData)

        -- Solicita a exportação do código do servidor
        local success, result1, result2 = pcall(function()
            return Remotes.AvatarEditorOutfitCodes:InvokeServer("Export")
        end)

        local generatedCode = nil
        if success then
            if tostring(result1):find("BH%-AE") then
                generatedCode = result1
            elseif tostring(result2):find("BH%-AE") then
                generatedCode = result2
            end
        end

        if generatedCode then
            Outfits[skinName] = {
                Code = generatedCode,
                CreatedAt = os.time()
            }
            SaveCodesFile()
            RefreshCodesDropdown()
            CreateNotification("Sucesso", "Código gerado para " .. skinName, 4)
        else
            CreateNotification("Erro", "Erro ao gerar código do servidor.", 4)
        end
    end
})

Tab5:AddSection({ "Carrega Skins Salvas Instantaneamente" })

DropdownCodes = Tab5:AddDropdown({
    Name = "Codigos de Skins",
    Options = GetFormattedCodesList(),
    Callback = function(option)
        if option then
            local name = option:match("^(.-)%s*%(")
            if name then
                SelectedOutfitKey = name:gsub("%s+$", "")
            else
                SelectedOutfitKey = option
            end
        end
    end
})

-- Carregar Código Selecionado
Tab5:AddButton({
    Name = "Carregar Skin Selecionado",
    Callback = function()
        if not SelectedOutfitKey or not Outfits[SelectedOutfitKey] then
            CreateNotification("Aviso", "Selecione Uma Skin  na Dropdown Primeiro!", 4)
            return
        end
        
        local info = Outfits[SelectedOutfitKey]
        task.spawn(function()
            pcall(function()
                Remotes.AvatarEditorOutfitCodes:InvokeServer("Load", info.Code)
            end)
        end)
        CreateNotification("Sucesso", "Skin Carregada Com Sucesso!", 4)
    end
})

-- Excluir Código Selecionado
Tab5:AddButton({
    Name = "Excluir Skin Selecionada",
    Callback = function()
        if not SelectedOutfitKey or not Outfits[SelectedOutfitKey] then
            CreateNotification("Aviso", "Selecione um código para excluir!", 4)
            return
        end
        
        Outfits[SelectedOutfitKey] = nil
        SaveCodesFile()
        RefreshCodesDropdown()
        CreateNotification("Sucesso", "Código de Skin Excluído Com Sucesso!", 4)
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

loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/Anima%C3%A7%C3%B5es%20Brookhaven%20"))()

Tab5:AddButton({
    Name = "Animações",
    Description = "",
    Callback = function()
        if _G.ToggleAnimGui then
            _G.ToggleAnimGui(true) -- Abre a interface de forma certeira!
        else
            warn("O script de animacoes ainda nao terminou de carregar.")
        end
    end
})

Tab5:AddButton({
    Name = "Mr. Toilet Idle ",
    Description = "",
    Callback = function()
        -- INSIRA O ID DA ANIMAÇÃO NO LUGAR DO NUMERO ABAIXO:
        local animId = 4418326547
        
        -- Executa o envio seguro para o servidor do jogo (Brookhaven)
        pcall(function()
            local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
            if remotes and remotes:FindFirstChild("Wear") then 
                remotes.Wear:InvokeServer(tonumber(animId)) 
                print("Animacao enviada com sucesso! ID:", animId)
            else
                warn("Remotes de customizacao nao encontrados no jogo.")
            end
        end)
    end
})

Tab5:AddButton({
    Name = "Mr. Toilet Run ",
    Description = "",
    Callback = function()
        -- INSIRA O ID DA ANIMAÇÃO NO LUGAR DO NUMERO ABAIXO:
        local animId = 4418324223
        
        -- Executa o envio seguro para o servidor do jogo (Brookhaven)
        pcall(function()
            local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
            if remotes and remotes:FindFirstChild("Wear") then 
                remotes.Wear:InvokeServer(tonumber(animId)) 
                print("Animacao enviada com sucesso! ID:", animId)
            else
                warn("Remotes de customizacao nao encontrados no jogo.")
            end
        end)
    end
})

Tab5:AddButton({
    Name = "Borock idle ",
    Description = "",
    Callback = function()
        -- INSIRA O ID DA ANIMAÇÃO NO LUGAR DO NUMERO ABAIXO:
        local animId = 3710007708
        
        -- Executa o envio seguro para o servidor do jogo (Brookhaven)
        pcall(function()
            local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
            if remotes and remotes:FindFirstChild("Wear") then 
                remotes.Wear:InvokeServer(tonumber(animId)) 
                print("Animacao enviada com sucesso! ID:", animId)
            else
                warn("Remotes de customizacao nao encontrados no jogo.")
            end
        end)
    end
})

Tab5:AddButton({
    Name = "R15 idle ",
    Description = "",
    Callback = function()
        -- INSIRA O ID DA ANIMAÇÃO NO LUGAR DO NUMERO ABAIXO:
        local animId = 4211409027
        
        -- Executa o envio seguro para o servidor do jogo (Brookhaven)
        pcall(function()
            local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
            if remotes and remotes:FindFirstChild("Wear") then 
                remotes.Wear:InvokeServer(tonumber(animId)) 
                print("Animacao enviada com sucesso! ID:", animId)
            else
                warn("Remotes de customizacao nao encontrados no jogo.")
            end
        end)
    end
})

Tab5:AddButton({
    Name = "Ud'zal idle ",
    Description = "",
    Callback = function()
        -- INSIRA O ID DA ANIMAÇÃO NO LUGAR DO NUMERO ABAIXO:
        local animId = 3307605825
        
        -- Executa o envio seguro para o servidor do jogo (Brookhaven)
        pcall(function()
            local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
            if remotes and remotes:FindFirstChild("Wear") then 
                remotes.Wear:InvokeServer(tonumber(animId)) 
                print("Animacao enviada com sucesso! ID:", animId)
            else
                warn("Remotes de customizacao nao encontrados no jogo.")
            end
        end)
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


----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba Casas---------------------------------------------------------
----------------------------------------------------------------------------------------------------------------
local Tab6= Window:MakeTab({ "| Casas", "home" })

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local LocalPlayer = Players.LocalPlayer
local Lots = workspace:WaitForChild("001_Lots")

local Remote = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("Lot:RevokeLandmark")

-- 🔎 DETECTOR
local function PlayerHasHouse()
    for _, House in ipairs(Lots:GetChildren()) do
        if House:IsA("Model") then
            local Owner = House:FindFirstChild("Owner")
            local OwnerObj = House:FindFirstChild("OwnerObj")

            if Owner and (Owner.Value == LocalPlayer.Name or Owner.Value == LocalPlayer.UserId) then
                return true
            end

            if OwnerObj and OwnerObj:IsA("ObjectValue") and OwnerObj.Value == LocalPlayer then
                return true
            end
        end
    end

    return false
end

-- 🔔 SUA NOTIFICAÇÃO (mesma posição + tween)
local TweenService = game:GetService("TweenService")

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
    frame.BackgroundColor3 = Color3.fromRGB(27, 5, 25)
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
    close.TextColor3 = Color3.fromRGB(255, 255, 255)
    close.Font = Enum.Font.SourceSansBold
    close.TextSize = 18
    close.Parent = frame

    -- 🔥 ANIMAÇÃO IGUAL AO SEU SISTEMA
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

-- 🔘 BOTÃO FINAL
Tab6:AddButton({
    Name = "Duplica Casa",
    Callback = function()
        local hasHouse = PlayerHasHouse()

        if hasHouse then
            Remote:FireServer()
        else
            CreateNotification("Erro", "Você não tem uma casa", 4)
        end
    end
})

Tab6:AddSection({ "Banir Jogadores da Sua Casa" })

do -- 📦 ESCOPO ISOLADO (Evita conflitos com outros scripts da sua UI)
    local Players = game:GetService("Players")
    local LocalPlayer = Players.LocalPlayer

    -- Variáveis de controle totalmente privadas deste bloco
    local listaDisponiveis = {}
    local listaSalvos = {}

    local selecionadoDropdown1 = nil
    local selecionadoDropdown2 = nil
    local banirListaAtivo = false
    local banirTodosAtivo = false

    -- Coleta os players iniciais
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(listaDisponiveis, player.Name)
        end
    end

    -- Declaração local dos elementos para não vazar para o script principal
    local Dropdown1 = nil
    local Dropdown2 = nil

    local function atualizarInterfaces()
        if Dropdown1 then Dropdown1:Set(listaDisponiveis) end
        if Dropdown2 then Dropdown2:Set(listaSalvos) end
    end

    local function reiniciarListas()
        listaDisponiveis = {}
        listaSalvos = {}
        selecionadoDropdown1 = nil
        selecionadoDropdown2 = nil
        
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then
                table.insert(listaDisponiveis, player.Name)
            end
        end
        atualizarInterfaces()
    end

    -- 🎯 DROPDOWN 1: SELECIONAR JOGADORES
    Dropdown1 = Tab6:AddDropdownPlayer({
        Name = "Selecionar Jogador",
        Options = listaDisponiveis,
        Default = "...",
        Callback = function(Value)
            -- Verifica se o nome passado bate com o formato esperado e evita travas do placeholder
            if Value and Value ~= "..." and Value ~= "Selecionar Jogador" then
                selecionadoDropdown1 = Value
                
                for i, nome in ipairs(listaDisponiveis) do
                    if nome == selecionadoDropdown1 then
                        table.remove(listaDisponiveis, i)
                        break
                    end
                end
                
                table.insert(listaSalvos, selecionadoDropdown1)
                selecionadoDropdown1 = nil
                atualizarInterfaces()
            end
        end
    })

    -- 🎯 DROPDOWN 2: LISTA DE JOGADORES SALVOS
    Dropdown2 = Tab6:AddDropdownPlayer({
        Name = "Jogadores na Lista",
        Options = listaSalvos,
        Default = "...",
        Callback = function(Value)
            if Value and Value ~= "..." and Value ~= "Jogadores na Lista" then
                selecionadoDropdown2 = Value
            end
        end
    })

    -- 🛑 BOTÃO: REMOVER PLAYER SELECIONADO DA LISTA
    Tab6:AddButton({
        Name = "Remover player selecionado da lista",
        Callback = function()
            if selecionadoDropdown2 and selecionadoDropdown2 ~= "..." then
                for i, nome in ipairs(listaSalvos) do
                    if nome == selecionadoDropdown2 then
                        table.remove(listaSalvos, i)
                        break
                    end
                end
                
                table.insert(listaDisponiveis, selecionadoDropdown2)
                selecionadoDropdown2 = nil
                atualizarInterfaces()
            end
        end
    })

    -- 🧹 BOTÃO: REMOVER TODOS OS PLAYERS DA LISTA
    Tab6:AddButton({
        Name = "Remover todos os players da lista",
        Callback = function()
            reiniciarListas()
        end
    })

    -- ⚡ TOGGLE: BANIR JOGADORES DA LISTA
    Tab6:AddToggle({
        Name = "Banir jogadores da lista",
        Description = "Bane da Casa Apenas Quem Estiver Adicionado na Lista",
        Default = false,
        Callback = function(state)
            banirListaAtivo = state

            spawn(function()
                while banirListaAtivo do
                    for _, player in ipairs(Players:GetPlayers()) do
                        if player ~= LocalPlayer then
                            local naLista = false
                            for _, nomeSalvo in ipairs(listaSalvos) do
                                if player.Name == nomeSalvo then
                                    naLista = true
                                    break
                                end
                            end
                            
                            if naLista then
                                local lots = workspace:FindFirstChild("001_Lots")
                                if lots then
                                    for _, casa in pairs(lots:GetChildren()) do
                                        local permissao = casa:FindFirstChild("HousePickedByPlayer")
                                            and casa.HousePickedByPlayer:FindFirstChild("HouseModel")
                                            and casa.HousePickedByPlayer.HouseModel:FindFirstChild("Permissions:Disallow")

                                        if permissao then
                                            permissao:FireServer(player)
                                        end
                                    end
                                end
                            end
                        end
                    end
                    task.wait(1)
                end
            end)
        end
    })

    -- ⚡ TOGGLE: BANIR TODOS OS JOGADORES DA CASA (Menos os da lista)
    Tab6:AddToggle({
        Name = "Banir Todos os Jogadores da Casa",
        Description = "Bane todos do servidor exceto quem estiver na lista",
        Default = false,
        Callback = function(state)
            banirTodosAtivo = state

            spawn(function()
                while banirTodosAtivo do
                    for _, player in ipairs(Players:GetPlayers()) do
                        if player ~= LocalPlayer then
                            local estaProtegido = false
                            for _, nomeSalvo in ipairs(listaSalvos) do
                                if player.Name == nomeSalvo then
                                    estaProtegido = true
                                    break
                                end
                            end
                            
                            if not estaProtegido then
                                local lots = workspace:FindFirstChild("001_Lots")
                                if lots then
                                    for _, casa in pairs(lots:GetChildren()) do
                                        local permissao = casa:FindFirstChild("HousePickedByPlayer")
                                            and casa.HousePickedByPlayer:FindFirstChild("HouseModel")
                                            and casa.HousePickedByPlayer.HouseModel:FindFirstChild("Permissions:Disallow")

                                        if permissao then
                                            permissao:FireServer(player)
                                        end
                                    end
                                end
                            end
                        end
                    end
                    task.wait(1)
                end
            end)
        end
    })

    -- 🛠️ EVENTOS DE CONEXÃO E LIMPEZA
    Players.PlayerAdded:Connect(function(player)
        task.wait(0.5)
        local jaExiste = false
        for _, nome in ipairs(listaSalvos) do
            if nome == player.Name then jaExiste = true break end
        end
        for _, nome in ipairs(listaDisponiveis) do
            if nome == player.Name then jaExiste = true break end
        end
        
        if not jaExiste and player ~= LocalPlayer then
            table.insert(listaDisponiveis, player.Name)
            atualizarInterfaces()
        end
    end)

    Players.PlayerRemoving:Connect(function(player)
        for i, nome in ipairs(listaDisponiveis) do
            if nome == player.Name then table.remove(listaDisponiveis, i) break end
        end
        for i, nome in ipairs(listaSalvos) do
            if nome == player.Name then table.remove(listaSalvos, i) break end
        end
        
        if selecionadoDropdown2 == player.Name then
            selecionadoDropdown2 = nil
        end
        atualizarInterfaces()
    end)
end


Tab6:AddSection({ "Casas" })

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
---------------------------------------------------------------------------------------------------------------------------------
                                          -- === Tab7 Carros=== --
---------------------------------------------------------------------------------------------------------------------------------

local Tab7= Window:MakeTab({ "| Carros", "car" })

local carSpeed = 25
local turboValue = "25"

Tab7:AddTextBox({
    Name = "Velocidade do carro",
    Description = "Digite a Velocidade",
    PlaceholderText = "Digite o valor da Velocidade...",
    Callback = function(Value)
		carSpeed = tonumber(Value) or carSpeed
    end
})

Tab7:AddTextBox({
    Name = "Definir Turbo",
    Description = "Defina o Turbo",
    PlaceholderText = "Digite o valor do Turbo...",
    Callback = function(Value)
        turboValue = tostring(Value)
    end
})

Tab7:AddButton({
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

Tab7:AddSection({ "Seleciona o Carrosl" })

local function updateVehicleList()
    local novaTabela = {}
    for _, v in pairs(game.Workspace.Vehicles:GetChildren()) do
        table.insert(novaTabela, v.Name)
    end
    return novaTabela
end

local selectedVehicle = nil

local CarrosTT = Tab7:AddDropdown({
    Name = "Selecionar Carro",
    Options = updateVehicleList(),
    Default = nil,
    Callback = function(Value)
        selectedVehicle = Value
    end
})

Tab7:AddButton({
    Name = "Atualiza Lista",
    Callback = function()
        CarrosTT:Set(updateVehicleList())
    end
})

Tab7:AddToggle({
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

Tab7:AddButton({
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

Tab7:AddToggle({
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

Tab7:AddSection({ "Todos os Carros" })

Tab7:AddButton({
    Name = "Puxar Carros",
    Callback = function()
        teleportAllCars()
    end
})

Tab7:AddButton({
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

Tab7:AddSection({ "ESP Carros" })

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

local Toggle = Tab7:AddToggle({
    Name = "ESP Carros",
    Default = false,
    Callback = function(Value)
        toggleESP(Value)
    end
})
----------------------------------------------------------------------------------------------------------------
-----------------------------------------Aba kid-----------------------------------------------------
----------------------------------------------------------------------------------------------------------------

-- Aba Child
local Tab8= Window:MakeTab({"Criança", "baby"})

local DropdownJogadoresKid
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

local selectedPlayerKid = nil  -- Armazena o jogador selecionado

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
    frame.BackgroundColor3 = Color3.fromRGB(27, 5, 25)
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
    close.TextColor3 = Color3.fromRGB(255, 255, 255)
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

-- 👥 LISTA DE PLAYERS
local function GetPlayerNames()
    local PlayerNames = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(PlayerNames, player.Name)
        end
    end
    return PlayerNames
end

Tab8:AddButton({
    Name = "Click Player Avatar",
    Callback = function()

        local backpack = LocalPlayer:WaitForChild("Backpack")

        -- remove tool antiga
        if backpack:FindFirstChild("SelecionarPlayerKid") then
            backpack.SelecionarPlayerKid:Destroy()
        end

        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("SelecionarPlayer") then
            LocalPlayer.Character.SelecionarPlayer:Destroy()
        end

        local Tool = Instance.new("Tool")
        Tool.Name = "SelecionarPlayerAvatar"
        Tool.RequiresHandle = false
        Tool.CanBeDropped = false
        Tool.TextureId = "rbxassetid://10709769732"
        Tool.Parent = backpack

        local Mouse = LocalPlayer:GetMouse()

        Tool.Activated:Connect(function()
            local Target = Mouse.Target
            if not Target then return end

            local Character = Target:FindFirstAncestorOfClass("Model")
            if not Character then return end

            local Player = Players:GetPlayerFromCharacter(Character)
            if not Player or Player == LocalPlayer then return end

            -- 🔥 variável correta
            selectedPlayerKid = Player.Name

            -- 🔥 atualiza dropdown corretamente
            if DropdownJogadoresKid then
                DropdownJogadoresKid:Set(Player.Name)
            end

            CreateNotification(
                "Notificação",
                "Player selecionado: " .. Player.Name,
                3
            )
        end)
    end
})

-- 🎯 DROPDOWN DE TARGET (Alterado para usar a nova DropdownPlayer)
DropdownJogadoresKid = Tab8:AddDropdownPlayer({
    Name = "Selecionar Jogador",
    Options = GetPlayerNames(),
    Default = "...",
    Callback = function(Value)
        selectedPlayerKid = Value
        print("Alvo selecionado: " .. tostring(selectedPlayerKid))

        -- Evita mandar notificação se o valor for o reset padrão da biblioteca
        if Value and Value ~= "..." and Value ~= "Selecionar Jogador" then
            CreateNotification("Notificação", "Player selecionado: "..Value, 3)
        end
    end
})

-- 🔁 ATUALIZAÇÃO AUTOMÁTICA SUPER SIMPLIFICADA
local function UpdateDropdown()
    task.wait(0.3) -- Aguarda o Roblox terminar de processar o player
    if DropdownJogadoresKid then
        local nomesAtualizados = GetPlayerNames()
        
        -- Atualiza a lista nativamente pela nova função sem perder o nome visível!
        DropdownJogadoresKid:Set(nomesAtualizados)
    end
end

-- CONEXÕES DOS EVENTOS
Players.PlayerAdded:Connect(UpdateDropdown)

Players.PlayerRemoving:Connect(function(plr)
    -- Se o jogador que saiu era o nosso alvo, avisa na tela
    if selectedPlayerKid and plr.Name == selectedPlayerKid then
        CreateNotification("Notificação", "O player "..plr.Name.." saiu do servidor", 4)
        selectedPlayerKid = nil
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
Tab8:AddToggle({
    Name = "Visualizar  Jogador",
    Callback = function(Value)
        viewing = Value
        if viewing then
            task.spawn(function()
                local shown = false
                while viewing do
                    local target = game.Players:FindFirstChild(selectedPlayerKid)
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
                        ShowLeaveNotification(selectedPlayerKid)
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

Tab8:AddButton({
    Name = "Enviar criança",
    Callback = function()
        if not selectedPlayerKid then
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

        local target = selectedPlayerKid 
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


Tab8:AddButton({
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

Tab8:AddSection({ Name = "BANG", Icon = "rbxassetid://" })

-- Função auxiliar para garantir que a criança exista
local function GetOrSpawnChild()
    local LocalPlayer = game.Players.LocalPlayer
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local playerFolder = workspace:FindFirstChild(LocalPlayer.Name)
    local followCharacter = playerFolder and playerFolder:FindFirstChild("FollowCharacter")

    if not followCharacter then
        local args = {
            [1] = "CharacterFollowSpawnPlayer",
            [2] = "BabyBoy"
        }

        pcall(function()
            ReplicatedStorage.RE:FindFirstChild("1Bab1yFollo1w"):FireServer(unpack(args))
        end)

        -- Esperar a criança spawnar
        local timeout = 3
        local startTime = tick()
        repeat
            task.wait(0.1)
            playerFolder = workspace:FindFirstChild(LocalPlayer.Name)
            followCharacter = playerFolder and playerFolder:FindFirstChild("FollowCharacter")
        until followCharacter or tick() - startTime > timeout

        if not followCharacter then
            warn("Criança não spawnou a tempo.")
            return nil
        end
    end

    -- Ativar colisão
    if playerFolder then
        for _, v in pairs(playerFolder:GetChildren()) do
            if v:IsA("BasePart") then
                v.CanCollide = true
            end
        end
    end

    return followCharacter
end

Tab8:AddButton({
    Title = "BANG FACE",
    Description = "",
    Callback = function()
        if not selectedPlayerKid then
            warn("LOC4T HUB: Nenhum player selecionado!")
            return
        end

        local followCharacter = GetOrSpawnChild()
        if not followCharacter then return end

        local target = selectedPlayerKid
        local pl = game.Players.LocalPlayer
        local targetChar = workspace:FindFirstChild(target)
        local hrp = targetChar and targetChar:FindFirstChild("HumanoidRootPart")
        if not targetChar or not hrp then warn("LOC4T HUB: Target não encontrada!") return end

        followCharacter.Parent = workspace
        local torso = followCharacter:FindFirstChild("Torso")
        if not torso then warn("LOC4T HUB: Torso não encontrado!") return end

        if getgenv().ChildFollowLoop then
            getgenv().ChildFollowLoop:Disconnect()
        end

        getgenv().ChildFollowLoop = game:GetService("RunService").Heartbeat:Connect(function()
            if not (targetChar and targetChar:FindFirstChild("HumanoidRootPart") and torso) then
                getgenv().ChildFollowLoop:Disconnect()
                return
            end

            local head = targetChar:FindFirstChild("Head")
            local facePos
            if head then
                facePos = head.Position + head.CFrame.LookVector * 0.1
            else
                facePos = hrp.Position + hrp.CFrame.LookVector * 0.1
            end

            local pos1 = facePos + hrp.CFrame.LookVector * -0.2
            local pos2 = facePos + hrp.CFrame.LookVector * 2.9

            local t = tick() % 1
            local progress = math.abs(math.sin(t * math.pi))
            local newPos = pos1:Lerp(pos2, progress)

            torso.BodyPosition.Position = newPos
            torso.BodyGyro.CFrame = CFrame.lookAt(torso.Position, facePos)
        end)
    end
})

Tab8:AddButton({
    Title = "BANG ATRÁS DO ALVO",
    Description = "",
    Callback = function()
        if not selectedPlayerKid then
            warn("LOC4T HUB: Nenhum player selecionado!")
            return
        end

        local followCharacter = GetOrSpawnChild()
        if not followCharacter then return end

        local target = selectedPlayerKid
        local pl = game.Players.LocalPlayer
        local targetChar = workspace:FindFirstChild(target)
        local hrp = targetChar and targetChar:FindFirstChild("HumanoidRootPart")
        if not targetChar or not hrp then warn("LOC4T HUB: Target não encontrada!") return end

        followCharacter.Parent = workspace
        local torso = followCharacter:FindFirstChild("Torso")
        if not torso then warn("LOC4T HUB: Torso não encontrado!") return end

        if getgenv().ChildFollowLoop then
            getgenv().ChildFollowLoop:Disconnect()
        end

        getgenv().ChildFollowLoop = game:GetService("RunService").Heartbeat:Connect(function()
            if not (targetChar and targetChar:FindFirstChild("HumanoidRootPart") and torso) then
                getgenv().ChildFollowLoop:Disconnect()
                return
            end

            local backPos = hrp.Position - hrp.CFrame.LookVector * 0.1
            local pos1 = backPos - hrp.CFrame.LookVector * 2.8
            local pos2 = backPos - hrp.CFrame.LookVector * -0.2

            local t = tick() % 1
            local progress = math.abs(math.sin(t * math.pi))
            local newPos = pos1:Lerp(pos2, progress)

            torso.BodyPosition.Position = newPos
            torso.BodyGyro.CFrame = CFrame.lookAt(torso.Position, hrp.Position)
        end)
    end
})


---------------------------------------------------------------------------------------------------------------------------------
                                          -- === Tab 9 Troll Musica === --
---------------------------------------------------------------------------------------------------------------------------------
local Tab9 = Window:MakeTab({"Musicas", "music"})


loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/MUSIC/refs/heads/main/README.md"))()

Tab9:AddTextBox({
    Name = "ID da musica",
    PlaceholderText = "Digite o ID",
    Callback = function(value)
        if value and value ~= "" then
            tocarMusica(tostring(value))
        end
    end
})

-- Dropdowns para Tab9 com Pesquisa Integrada
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
        tocarMusica(tostring(soundId)) -- Usa a função tocarMusica para tocar em todos os contextos
    end

    -- 🔍 Mudamos de AddDropdown para AddDropdownSearch
    Tab9:AddDropdownSearch({
        Name = title,
        Description = "all",
        Default = defaultOption,
        MultiSelect = false, -- Certifique-se de que o nome do parâmetro é MultiSelect conforme a nova função
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
        {name = "ja que me ensinou (Estourado)", id = "102593134121793"},
        {name = "online metendo", id = "97825347303470"},
        {name = "Titanic", id = "75498888713958"},
        {name = "Botadinha (Estourado)", id = "84624301411909"},
        {name = "NOTIFICAÇÃO PREFERIDA", id = "90137280531474"},
        {name = "nunca será eu", id = "122871200237533"},
        {name = "cadeira", id = "96888228525073"},
        {name = "IMPERFEITO (BREGA)", id = "97664717493077"},
        {name = "Vai Tomar Flechada", id = "138345050819224"},
        {name = "Boate Azul", id = "106412079335663"},
        {name = "Esquema confirmado", id = "134035788881796"},
        {name = "A CULPA É NOSSA", id = "72213295707216"},
        {name = "Desça Dai Seu Corno", id = "119738878921996"},
        {name = "Amor Ou Litrão", id = "111551362636063"},
        {name = "Forro Já Cansou", id = "74812784884330"},
        {name = "Lembro Até Hoje", id = "71531533552899"},
        {name = "Amigo", id = "91119180724905"},
        {name = "Amor Verdadeiro", id = "123455164277076"},
        {name = "Boys Do Forró", id = "139462268046679"},
        {name = "Quem é o Louco", id = "106958630419629"},
        {name = "Off The King", id = "120324849313242"},
        {name = "Forró da Resenha", id = "120973520531216"},
        {name = "Forró do Dudu", id = "74404168179733"},
        {name = "Forró de São João", id = "106364874935196"},
        {name = "Forró Engraçado Divertido", id = "76524290482399"},
        {name = "Uno Zero", id = "112959083808887"},
        {name = "Iate do Neymar", id = "135738534706063"},
        {name = "Batidão na Aldeia", id = "79953696595578"},
        {name = "Humorous Samba", id = "1836175030"},
        {name = "Samba Tropical", id = "1838888602"}
    }
}, "Option 1")

-- Dropdown "Músicas e Memes Aleatórios"
createMusicDropdown("Músicas e Memes Aleatorios", {
    ["Músicas e Memes Aleatorios"] = {
        {name = "Buena la vida", id = "76650356472656"},
        {name = "Injustiça", id = "124989405084883"},
        {name = "Minha Namorada Não Me Ama Mais", id = "135090308544819"},
        {name = "GTA", id = "109337680029292"},
        {name = "Epstein", id = "79910195620356"},
        {name = "SIX SEVEN FUNK 67", id = "139780631670217"},
        {name = "67 FUNK SIX SEVEN", id = "118266718724986"},
        {name = "Não Sou Gay", id = "82816587043443"},
        {name = "União Flasco", id = "107991235917983"},
        {name = "Coin", id = "78878448738118"},
    	{ name = "Want To Love", id = 104846670980072 },
        {name = "30 ovos 10 reais", id = "3148329638"}
    }
}, "Option 1")

-- Dropdown "Vibe Tipo Festa"
createMusicDropdown("Vibe Tipo Festa", {
    ["Vibe Tipo Festa"] = {
        {name = "Koop_Cod", id = "78897336878154"},
        {name = "Bella Ciao", id = "123794300996826"},
        {name = "Bang Bang Bang", id = "90289127130880"},
        {name = "boy", id = "111841460604775"},
        {name = "Kiss Me", id = "124388294104823"},
        {name = "tomb", id = "140447408472411"},
        {name = "Fnaf", id = "140447408472411"},
        {name = "my heart", id = "82561126988856"},
        {name = "Cuddle me Ka", id = "116308785658619"},
        {name = "DASEN edmTH", id = "107265786318541"},
        {name = "Hashire EDM", id = "94939878294536"},
        {name = "Hawlower", id = "122933134275091"},
        {name = "Hawlower V2", id = "94635984925376"},
        {name = "likealways", id = "121888577857365"},
        {name = "Low Cortisol", id = "110919391228823"},
        {name = "Haru no fun", id = "97401233876313"},
        {name = "Bass Boost", id = "136893418307185"},
        {name = "MESMERIZER", id = "71934965392436"},
        {name = "いっしょにあそぼ", id = "76790581169424"},
        {name = "Ritmada Vida no Play Eletrofunk", id = "73324023761634"},
        {name = "Ritmada She'll be here Desande", id = "122661386912651"},
        {name = "เชิ้ปๆ", id = "120322544127249"},
        {name = "KAMNH VELOCITY (RD VERSI) 2025", id = "130721206402716"},
        {name = "HUAYF", id = "82152175089703"},
        {name = "Garoto de Copacabana", id = "135648634110254"},
        {name = "Boa vibe em Ubatuba", id = "139059061493558"},
        {name = "SLIP AWAY", id = "126152928520174"},
        {name = "Rally Girl", id = "76840497592345"},
        {name = "Beat - Sunflower", id = "127116171234509"},
        {name = "BEAT IMATUR0", id = "88449645926964"},
        {name = "Beautiful", id = "96270603953822"},
        {name = "Beat Retrospectiva", id = "99919752543935"},
        {name = "Fashion", id = "116003203490064"},
        {name = "Uauu", id = "80520116507969"},
        {name = "Fangs on Fire", id = "73778985963973"},
        {name = "The wheels on the bus go round and round!", id = "123268013026823"},
        {name = "hate me", id = "131378414686961"},
        {name = "jingel", id = "103522348985077"},
        {name = "akkeeezzzz000rrr", id = "104761277691296"},
        {name = "VER333", id = "94101740972196"},
        {name = "Winter Breath", id = "77283704759551"},
        {name = "Minecraft", id = "126753086148431"},
        {name = "LET YOU GO", id = "71410123147723"},
        {name = "Paradise", id = "108551901230281"},
        {name = "X Mark", id = "138392888216982"},
        {name = "Fred fron densire", id = "84185150763409"},
        {name = "AllNight", id = "98310334398449"},
        {name = "MONSTERS", id = "140021357514406"},
        {name = "Shine", id = "116149175636401"},
        {name = "the perfect pair", id = "93699644879957"},
        {name = "Warm Room", id = "77275718845641"},
        {name = "i like trains", id = "94410505324605"},
        {name = "6snot :3", id = "134183014721429"},
        {name = "GAME OVER", id = "139980842740039"},
        {name = "CrystalDaze", id = "128986414759194"},
        {name = "Sad", id = "128753420599043"},
        {name = "Treatment Love", id = "76591312767643"},
        {name = "Dream Water", id = "76312692501155"},
        {name = "PulseFrame", id = "72478420140778"},
        {name = "night two", id = "116629102249251"},
        {name = "Supershy But", id = "79079932172268"},
        {name = "9mare", id = "102172754546876"},
        {name = "Planeta", id = "121242462527636"},
        {name = "cast aside", id = "135733391424853"},
        {name = "FL0WWS04N", id = "94281718874647"},
        {name = "Ktistiee", id = "99159136877639"},
        {name = "glucci", id = "132391305999721"},
        {name = "chill breakfast", id = "121631120131597"},
        {name = "russian tech is ok", id = "127196587113703"},
        {name = "Fairy and Cats", id = "135907393503594"},
        {name = "zyf", id = "98209966069260"},
        {name = "Yellow Glove", id = "119087791000979"},
        {name = "TheFlow", id = "83916733906478"},
        {name = "virtual", id = "123986270017847"},
        {name = "Tristeza", id = "98839453510161"},
        {name = "MyHomage", id = "125812293155661"},
        {name = "trustme", id = "81732137163686"},
        {name = "Miss you", id = "98184705510569"},
        {name = "in motion", id = "91686549884884"},
        {name = "now", id = "137621276242203"},
        {name = "memories", id = "80230161200798"},
        {name = "Backrooms", id = "120817494107898"},
        {name = "Stray", id = "120102995443063"},
        {name = "Ai Đưa Em Về", id = "119589720384457"},
        {name = "ANXIETY (Amapiano Re-fix)", id = "101483901475189"},
        {name = "Megalovania but its only the melodies", id = "104500091160463"},
        {name = "androphono strikes back", id = "78312089943968"},
        {name = "Longe Demais", id = "124478512057763"},
        {name = "CELL!", id = "117634275895085"},
        {name = "SLIP AWAY", id = "126152928520174"},
        {name = "Alone in Motion", id = "122379348696948"},
        {name = "Fade Away", id = "81002139735874"},
        {name = "Wounds & Wishes", id = "109347979566607"},
        {name = "Ascensão do Monarca", id = "101864243033211"},
        {name = "MIKU MIKU HATSUNE", id = "112783541496955"},
        {name = "Air", id = "73197748961359"},
        {name = "COUNTIN STARS", id = "118957335322667"},
        {name = "WardrobeFox", id = "89258052168328"},
        {name = "BurningWorld", id = "111351357978027"},
        {name = "SunMoon", id = "91995598699901"},
        {name = "AllNight", id = "98310334398449"},
        {name = "No More", id = "1846458016"},
        {name = "Stephen Walking - JC-08", id = "7028970358"},
        {name = "Conro - All I Want", id = "7023680426"},
        {name = "Grant - Are We Still Young (feat. Juneau)", id = "5410086445"},
        {name = "Stonebank - Fire", id = "7028985831"},
        {name = "Rootkit - Taking Me Higher", id = "5410081542"},
        {name = "Duumu - Forward (feat. MIA)", id = "5410081471"},
        {name = "Tony Romera - I Can't", id = "5410082805"},
        {name = "Clair De Lune", id = "1838457617"},
        {name = "EUROPAPA LOUDER! (Nightcore)", id = "111346133543699"}
        
    }
}, "Option 1")

-- Dropdown "Funk"
createMusicDropdown("Funk", {
    ["Funk"] = {
        {name = "Vai Puta sua gostosa", id = "91225667489242"},
        {name = "Novinha", id = "95046137686947"},
        {name = "bala no aco", id = "125427893649267"},
        {name = "Sem Preocupação", id = "122126177666117"},
        {name = "RenknRenk (Estourado)", id = "108672579124479"},
        {name = "Ela kê Leitada (Estourado)", id = "98228200010571"},
        {name = "Piui Tik Tak(Estourado)", id = "139239312760455"},
        {name = "Eu Vou Come No Uno", id = "82284832948222"},
        {name = "Joga Bct", id = "132706975762383"},
        {name = "Din Din Dom", id = "135194449370589"},
        {name = "Colocar Colocar (Estourado)", id = "104226699513043"},
        {name = "Baile (Estourado)", id = "75531002354210"},
        {name = "Romeu e Julieta", id = "86803379923289"},
        {name = "Pisca Xrc no Parafal", id = "78247020542222"},
        {name = "Ajoelha Cai de Bc", id = "127052251825619"},
        {name = "Ta Batendo Meia Noite", id = "106285676892349"},
        {name = "Uber Moto", id = "115729538399089"},
        {name = "É o Antares", id = "100133382335077"},
        {name = "Botan Botan", id = "74904585870595"},
        {name = "Pantanal", id = "94880156546772"},
        {name = "vaiiiiiii", id = "101519980567219"},
        {name = "fica", id = "91506361861086"},
        {name = "Mente Milionária", id = "140600649204233"},
        {name = "Chumbo Na Bct", id = "131748498759806"},
        {name = "showw", id = "100966278801294"},
        {name = "Jogo Da Galera", id = "74362964495890"},
        {name = "Joga Essa Bct Po Pcc", id = "131935226569147"},
        {name = "Vem Mulher Com a Shota", id = "87600142346663"},
        {name = "faz o sinal", id = "104383515745988"},
        {name = "berimbau do alan", id = "89909853236568"},
        {name = "RUSH FUNK", id = "72451271928975"},
        {name = "PAPEL FUNK", id = "76981625332079"},
        {name = "e no final", id = "107230480488085"},
        {name = "Marketada", id = "138456268410435"},
        {name = "Escorrega vai garota(Estourado)", id = "75048565219972"},
        {name = "Senju Sounds 1", id = "125276472076218"},
        {name = "sadd", id = "131013862565986"},
        {name = "Tropa Do Gordão", id = "83400946888030"},
        {name = "Te Chamo de Amor", id = "111118068516413"},
        {name = "Tapete Mágico", id = "122488679897031"},
        {name = "Assombra Matrix", id = "84806858575292"},
        {name = "lei dos 3(Estourado)", id = "118279338474223"},
        {name = "(Conteúdo Explícito)", id = "129902784040741"},
        {name = "ela e do tipo(estorado)", id = "108808025565103"},
        {name = "Sacanagem (Estorado)", id = "124054822886984"},
        {name = "maria mariah(Estourado)", id = "110104902087908"},
        {name = "lei an", id = "91853368622225"},
        {name = "SO UMA SURUBINHA", id = "122259510323980"},
        {name = "multiplicou", id = "135750430892149"},
        {name = "Grupo De Pagode", id = "112088206507457"},
        {name = "Rebola Po Pai", id = "120075559226752"},
        {name = "juwlias cha", id = "87195083268833"},
        {name = "olha a explosao(Estourado)", id = "121075115415245"},
        {name = "Filminho na Tela", id = "118700341959988"},
        {name = "pipokinha", id = "70725650826656"},
        {name = "Amiguinha Best", id = "138021904914351"},
        {name = "TROPA FUNK", id = "125784363463466"},
        {name = "COCOTA CLXYAL x COLD", id = "130758596227702"},
        {name = "Chumbo na Bct", id = "131748498759806"},
        {name = "Truque de Magica", id = "115286590587630"},
        {name = "viagem multiversal", id = "93433890371027"},
        {name = "LANÇA DE CÔCO", id = "134656279550431"},
        {name = "Tenebrosa", id = "101012305582217"},
        {name = "Meia Noite(Estourado)", id = "131185438076634"},
        {name = "Quem Me Julgou (Funk)", id = "128958063446335"},
        {name = "Leal Até o Fim (Funk)", id = "131685935847186"},
        {name = "Surra de Piroca", id = "139582138143960"},
        {name = "eletro", id = "122871552019283"},
        {name = "Land Rover", id = "93896033115660"},
        {name = "Vem Vem me Fdd", id = "136574160308808"},
        {name = "Perna bamba", id = "86838668592481"},
        {name = "Luz do Luar", id = "134505988236731"},
        {name = "Meia Noite (Remake)", id = "86617433885915"},
        {name = "Black Lança(Estourado)", id = "97471613998368"},
        {name = "Menina Se Prepara", id = "113390738937611"},
        {name = "Baile no Morro", id = "138187826695336"},
        {name = "reluk", id = "88232201387507"},
        {name = "Místico", id = "126733506965411"},
        {name = "MTG ASSOMBRA MATRIX 8", id = "76063080783733"},
        {name = "Toma Toma", id = "137254194634453"},
        {name = "Ent Vai Se Preparar", id = "77428616866753"},
        {name = "Tropa do Rato", id = "74885231607109"},
        {name = "MELODIA ALUCINANTE 2", id = "73414602336971"},
        {name = "dois", id = "122292837904105"},
        {name = "Vou Comer Seu Uc", id = "75839538917529"},
        {name = "Oh Juliana", id = "84349909808037"},
        {name = "Pega Meu Boneco", id = "136514868732136"},
        {name = "To Com Peru Desgovernado", id = "115837046053738"},
        {name = "Meu Hd Chei de Cp", id = "118351471702293"},
        {name = "Blue Bird Tambor by Dzn", id = "89473100926016"},
        {name = "Funk Naruto", id = "89473100926016"},
        {name = "Saayonara", id = "123868933091795"},
        {name = "iPhone Branco", id = "103288558732219"},
        {name = "Pe Direito", id = "127870629973068"},
        {name = "Famosinha", id = "112406825739796"},
        {name = "Faz Striptease Na Minha Cama", id = "128011871344522"},
        {name = "TOMA TOMA TOMANDO (FUNK ARROCHA)", id = "88266916032720"},
        {name = "ENCOSTA FUNK", id = "101222653992044"},
        {name = "NAT FUNK", id = "107416893652681"},
        {name = "março vip", id = "104481380959795"},
        {name = "Tentando Eteder o poder dessa grt", id = "131847084942844"},
        {name = "Drak Flow", id = "79120642849019"},
        {name = "Rave nanah", id = "119020235792430"},
        {name = "montagem do silvio", id = "104828343009296"},
        {name = "montagem intergaláctica", id = "122039107528238"},
        {name = "Pancadão", id = "76312991186384"},
        {name = "RATIONAL", id = "73774331093132"},
        {name = "Em dezembro de 81 (Lxz)", id = "92492039534399"},
        {name = "cast aside", id = "135733391424853"},
        {name = "Seu Fã", id = "85342086082111"},
        {name = "Mensagem", id = "130637458480604"},
        {name = "Dança do Canguru", id = "86876136192157"},
        {name = "É FULGA NA VT", id = "131891110268352"},
        {name = "CVRL", id = "124244582950595"},
        {name = "MONTAGEM ARABIANA", id = "78076624091098"},
        {name = "Brega Violino (Beat Brega Funk)", id = "99399643204701"},
        {name = "Viver bem", id = "82805460494325"},
        {name = "Ritmo Pixelado (NGI)", id = "93928823862203"},
        {name = "SENTA (NGI & XL)", id = "124085422276732"},
        {name = "V7 (XL & NGI)", id = "80348640826643"}
    }
}, "Option 1")

-- Dropdown "Phonk"
createMusicDropdown("Phonk", {
    ["phonk"] = {
        {name = "DigitalType", id = "94871427242599"},
        {name = "brigadeiro", id = "121046655523341"},
        {name = "Montagem Bionica ", id = "121046655523341"},
        {name = "MONTAGEM MITRELOGICO by clxyal", id = "107513285979080"},
        {name = "UIUAH ", id = "82894376737849"},
        {name = "MONTAGEM AMOR SEM FINAL", id = "127038714548359"},
        {name = "ESPECTRAL", id = "119202700760169"},
        {name = "CUTEMAKMAK FUNK (Slowed)", id = "120871403922972"},
        {name = "Sento e Me Acabo", id = "124140125253346"},
        {name = "Wyles", id = "85385155970460"},
        {name = "SOUR PATCH KIDS", id = "91502410121438"},
        {name = "MONTAGEM POCK POCK", id = "102333419023382"},
        {name = "Tatiu Win", id = "122871512353520"},
        {name = "Shlay!", id = "126887144190812"},
        {name = "AUTOMOTIVO NIGHT - Sped Up", id = "115016589376700"},
        {name = "DISTORTION FUNK", id = "118740708757685"},
        {name = "(SLOWED) DISTORTION FUNK", id = "105126065014034"},
        {name = "FEMININO DO VAPO FUNK", id = "106317184644394"},
        {name = "FUNK DA PRAIA - Slowed", id = "112068892721408"},
        {name = "AUTOMOTIVO NIGHT-Super Slowed", id = "122852029094656"},
        {name = "Liberto Funk", id = "84733736048142"},
        {name = "HYPNOTIZED! (Sped Up)", id = "92175624643620"},
        {name = "ATMOSPHERIKA FUNK", id = "77857496821844"},
        {name = "Catuquanvan (NGI)", id = "88038595663211"},
        {name = "I Love", id = "82148953715595"},
        {name = "MONTAGEM FUTABA", id = "91834632690710"},
        {name = "GOTH FUNK", id = "97662362226511"},
        {name = "MONTAGEM SUBURBANA", id = "139825057894568"},
        {name = "Liberto Funk(Slowed)", id = "84733736048142"},
        {name = "Jumpstyle", id = "1839246711"},
        {name = "Blessed Mane", id = "16831108393"},
        {name = "Montagem Balada:", id = "83797836818857"},
        {name = "BEM SOLTO BRAZIL!", id = "119936139925486"},
        {name = "Kerosene", id = "17647322226"}
    }
}, "Option 1")

Tab9:AddButton({
    Name = "Stop",
    Description = "ALL music",
    Callback = function()
        tocarMusica("")
    end
})


---------------------------------------------------------------------------------------------------------------------------------
                                          -- === Tab Script === --
---------------------------------------------------------------------------------------------------------------------------------
local TabScript = Window:MakeTab({"Scripts ", "music"})

TabScript:AddSection({ Name = "Aprimoramentos" })

TabScript:AddButton({
    Name = "FE Emotes SAGAZx",
    Description = "",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/FE%20Emotes%20do%20SAGAZx%20HUB"))()
    end
})

TabScript:AddButton({
    Name = "Expand Hotbar",
    Description = "Expande Sua Hotbar de 10 Ate 20 Slots",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/Expand%20Hotbar%20"))()
    end
})
 
TabScript:AddButton({
    Name = "Fly Car",
    Description = "Faz Você Voar Com o Carro",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/raelhubfunctions/Save-scripts/refs/heads/main/CarMobile.lua"))()
    end
})

local FlyGui = loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/FLY%20GUI%20V3"))()

TabScript:AddToggle({
    Name = "Fly GUI",
    Description = "Faz Você Voar",
    Default = false,
    Callback = function(Value)
        if FlyGui then
            FlyGui.Enabled = Value
        end
    end
})

loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/DRONE"))()

TabScript:AddToggle({
  Name = "Drone",
  Default = false,
  Callback = function(Value)
    Frame.Visible = Value -- Se Value for true, aparece. Se for false, some.
  end
})

local InvisLoaded = false

TabScript:AddToggle({
    Name = "FE Invisível",
    Description = "Deixa Você Invisível",
    Default = false,
    Callback = function(Value)
        if Value then
            if not InvisLoaded then
                InvisLoaded = true
                loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/FE%20Invisible%20"))()
            end

            game:GetService("CoreGui").InvisButtonGui.Enabled = true
        else
            if game:GetService("CoreGui"):FindFirstChild("InvisButtonGui") then
                game:GetService("CoreGui").InvisButtonGui.Enabled = false
            end
        end
    end
})

loadstring(game:HttpGet("https://raw.githubusercontent.com/psychoSAGAZ/SAGAZx-HUB/refs/heads/main/Shiftlock%20"))()

TabScript:AddToggle({
    Name = "Shiftlock",
    Default = true, -- Mudado para true para o design do toggle começar ativado
    Callback = function(Value)
        if getgenv().ToggleShiftlockButton then
            if Value == true then
                getgenv().ToggleShiftlockButton(true)
            else
                -- Força o botão a sumir imediatamente, independente do shiftlock estar ativo ou não
                local CoreGui = game:GetService("CoreGui")
                local gui = CoreGui:FindFirstChild("Shiftlock (CoreGui)")
                if gui then
                    gui.Enabled = false
                end
            end
        end
    end
})

local ChatConnections = {}
local ChatEnabled = false

TabScript:AddToggle({
    Name = "Oculta Chat Global ",
    Description = "Certifique de Colocar o Chat em ''Aqui'' ",
    CurrentValue = false,
    Callback = function(Value)
        ChatEnabled = Value

        -- Desconecta tudo ao desativar
        if not Value then
            for _, Connection in ipairs(ChatConnections) do
                if Connection then
                    Connection:Disconnect()
                end
            end
            table.clear(ChatConnections)
            return
        end

        local CoreGui = game:GetService("CoreGui")

        local function RemoveChatParts()
            if not ChatEnabled then return end

            local Chat = CoreGui:FindFirstChild("ExperienceChat")
            if not Chat then return end

            local AppLayout = Chat:FindFirstChild("appLayout")
            if not AppLayout then return end

            local TopPadding = AppLayout:FindFirstChild("topPadding")
            if TopPadding then
                TopPadding:Destroy()
            end

            local ChannelBar = AppLayout:FindFirstChild("channelBar")
            if ChannelBar then
                ChannelBar:Destroy()
            end
        end

        RemoveChatParts()

        table.insert(ChatConnections, CoreGui.ChildAdded:Connect(function(Child)
            if not ChatEnabled then return end

            if Child.Name == "ExperienceChat" then
                task.wait()
                RemoveChatParts()

                local AppLayout = Child:FindFirstChild("appLayout") or Child:WaitForChild("appLayout", 10)
                if AppLayout then
                    table.insert(ChatConnections, AppLayout.ChildAdded:Connect(function()
                        if ChatEnabled then
                            task.wait()
                            RemoveChatParts()
                        end
                    end))
                end
            end
        end))

        local Chat = CoreGui:FindFirstChild("ExperienceChat")
        if Chat then
            local AppLayout = Chat:FindFirstChild("appLayout")
            if AppLayout then
                table.insert(ChatConnections, AppLayout.ChildAdded:Connect(function()
                    if ChatEnabled then
                        task.wait()
                        RemoveChatParts()
                    end
                end))
            end
        end
    end
})

TabScript:AddToggle({
    Name = "Interface de Botão Antiga Do Brookhaven",
    Default = false,
    Callback = function(Value)
        local player = game:GetService("Players").LocalPlayer
        local gui = player:WaitForChild("PlayerGui")

        local main = gui:WaitForChild("MainGUIHandler")
        local buttons = main:WaitForChild("MainButtons")

        local old = buttons:WaitForChild("Old")
        local new = buttons:WaitForChild("New")

        if Value then
            -- Mostra a interface antiga
            old.Visible = true
            old.Position = UDim2.new(0.200000003, 57, 0, 0)
            old.Size = UDim2.new(0.75, 0, 1, 0)

            new.Visible = false
        else
            -- Mostra a interface nova
            old.Visible = false
            new.Visible = true
        end
    end
})

TabScript:AddToggle({
    Name = "Shaders",
    Default = false,
    Callback = function(Value)
        if Value then
            local workspace = game:GetService("Workspace")
            local Lighting = game:GetService("Lighting")
            local RunService = game:GetService("RunService")
            local Debris = game:GetService("Debris")
            local TweenService = game:GetService("TweenService")
            local SoundService = game:GetService("SoundService")
            local Players = game:GetService("Players")
            local player = Players.LocalPlayer
            local model = workspace:FindFirstChild("Model")

            _G.SistemaAtivo = true
            _G.SistemaConnections = {}
            _G.SistemaInstances = {}

            local function addConnection(connection)
                table.insert(_G.SistemaConnections, connection)
            end

            local function addInstance(instance)
                table.insert(_G.SistemaInstances, instance)
            end

            local sound = Instance.new("Sound")
            sound.SoundId = "rbxassetid://131644923"
            sound.Volume = 1
            sound.Parent = SoundService
            sound:Play()
            addInstance(sound)

            if model then
                local function setMat(obj)
                    for _, c in pairs(obj:GetChildren()) do
                        if c:IsA("BasePart") then
                            c.Material = Enum.Material.Basalt
                        elseif c:IsA("Model") or c:IsA("Folder") then
                            setMat(c)
                        end
                    end
                end
                
                if model:FindFirstChild("001_SnowStreet") then
                    setMat(model["001_SnowStreet"])
                end
                
                if model:FindFirstChild("Street") then
                    for _, o in pairs(model.Street:GetDescendants()) do
                        if o:IsA("BasePart") then
                            o.Material = Enum.Material.Basalt
                        end
                    end
                end
                
                for _, o in pairs(model:GetChildren()) do
                    if o:IsA("BasePart") and (o.Name == "Sidewalk" or o.Name == "Wedge") and o.Material == Enum.Material.SmoothPlastic then
                        o.Material = Enum.Material.Cobblestone
                    end
                end
                
                local modelConnection = model.ChildAdded:Connect(function(obj)
                    if obj:IsA("BasePart") and (obj.Name == "Sidewalk" or obj.Name == "Wedge") and obj.Material == Enum.Material.SmoothPlastic then
                        obj.Material = Enum.Material.Cobblestone
                    end
                end)
                addConnection(modelConnection)
            end

            -- Sistema de som ambiente
            local soundPart = Instance.new("Part")
            soundPart.Size = Vector3.new(1,1,1)
            soundPart.Transparency = 1
            soundPart.Anchored = true
            soundPart.CanCollide = false
            soundPart.Parent = workspace
            addInstance(soundPart)

            local character = player.Character or player.CharacterAdded:Wait()
            local hrp = character:WaitForChild("HumanoidRootPart")

            local birdSound = Instance.new("Sound")
            birdSound.Name = "BirdsSound"
            birdSound.SoundId = "rbxassetid://1237969272"
            birdSound.Looped = true
            birdSound.Volume = 0.05
            birdSound.Parent = soundPart
            addInstance(birdSound)

            local wolfSound = Instance.new("Sound")
            wolfSound.SoundId = "rbxassetid://6654360741"
            wolfSound.Volume = 0.05
            wolfSound.Looped = false
            wolfSound.Parent = workspace
            addInstance(wolfSound)

            local heartbeatConn = RunService.Heartbeat:Connect(function()
                if hrp and hrp.Parent and _G.SistemaAtivo then
                    soundPart.Position = hrp.Position + Vector3.new(0,10,0)
                end
            end)
            addConnection(heartbeatConn)

            local function isNight()
                local t = Lighting.ClockTime
                return (t >= 18 or t <= 6)
            end

            local nightCycleConn = task.spawn(function()
                while _G.SistemaAtivo do
                    if isNight() then
                        if birdSound.IsPlaying then birdSound:Stop() end
                        if wolfSound.IsPlaying then wolfSound:Stop() end
                        wolfSound:Play()
                    else
                        if wolfSound.IsPlaying then wolfSound:Stop() end
                        if not birdSound.IsPlaying then birdSound:Play() end
                    end
                    wait(20)
                end
            end)
            addConnection(nightCycleConn)

            local fountainPart = Instance.new("Part")
            fountainPart.Anchored = true
            fountainPart.CanCollide = false
            fountainPart.Transparency = 1
            fountainPart.Size = Vector3.new(1,1,1)
            fountainPart.Position = Vector3.new(-27,19,15)
            fountainPart.Parent = workspace
            addInstance(fountainPart)

            local attachment = Instance.new("Attachment")
            attachment.Position = Vector3.new(-27,19,15)
            attachment.Parent = fountainPart
            addInstance(attachment)

            local fountainSound = Instance.new("Sound")
            fountainSound.Name = "FountainSound"
            fountainSound.SoundId = "rbxassetid://4766793559"
            fountainSound.Looped = true
            fountainSound.Volume = 0.03
            fountainSound.EmitterSize = 10
            fountainSound.RollOffMode = Enum.RollOffMode.Linear
            fountainSound.MaxDistance = 100
            fountainSound.Parent = attachment
            fountainSound:Play()
            addInstance(fountainSound)

            local customSound = Instance.new("Sound")
            customSound.Name = "MyCustomSound"
            customSound.SoundId = "rbxassetid://9048659736"
            customSound.Volume = 0.01
            customSound.Looped = true
            customSound.PlayOnRemove = false
            customSound.Parent = workspace
            customSound:Play()
            addInstance(customSound)

            local active = false
            local stars = {}
            local shootingStarsFolder = Instance.new("Folder",workspace)
            shootingStarsFolder.Name = "ShootingStars"
            addInstance(shootingStarsFolder)
            
            local STAR_COUNT = 300
            local SHOOTING_STAR_CHANCE = 0.3
            local SHOOTING_STAR_MAX = 12
            local shootingStarCooldown = 0.1

            local spaceSound = Instance.new("Sound",workspace)
            spaceSound.SoundId = "rbxassetid://1843520836"
            spaceSound.Volume = 0.3
            spaceSound.Looped = true
            spaceSound.Name = "SpaceAmbience"
            addInstance(spaceSound)

            local function createStar()
                if not _G.SistemaAtivo then return end
                local star = Instance.new("Part")
                local size = math.random(1,3)*0.5
                star.Size = Vector3.new(size,size,size)
                star.Position = Vector3.new(math.random(-1000,1000),math.random(300,700),math.random(-1000,1000))
                star.Anchored = true
                star.CanCollide = false
                star.Material = Enum.Material.Neon
                local colors = {Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,180),Color3.fromRGB(180,200,255)}
                star.Color = colors[math.random(1,#colors)]
                star.Name = "Star"
                star.Parent = workspace
                addInstance(star)
                
                local light = Instance.new("PointLight",star)
                light.Brightness = 2 + math.random()*1.5
                light.Range = 12
                addInstance(light)
                
                local starConn = spawn(function()
                    while star.Parent and active and _G.SistemaAtivo do
                        star.Transparency = 0.2 + math.sin(tick()*math.random(2,5))*0.2
                        RunService.Heartbeat:Wait()
                    end
                    if star.Parent then star:Destroy() end
                end)
                addConnection(starConn)
                table.insert(stars,star)
            end

            local function createShootingStar()
                if not active or not _G.SistemaAtivo then return end
                local startPos = Vector3.new(math.random(-1000,1000),math.random(350,600),math.random(-1000,1000))
                local dir = Vector3.new(math.random(-1,1),math.random(-0.1,0.1),math.random(-1,1)).Unit
                local speed = math.random(350,550)
                local isFire = math.random() <= SHOOTING_STAR_CHANCE
                local color = isFire and Color3.fromRGB(255,50,50) or Color3.fromRGB(255,255,220)
                local trailColor = isFire and ColorSequence.new(Color3.fromRGB(255,120,0),Color3.fromRGB(255,230,50)) or ColorSequence.new(Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,180))
                
                local star = Instance.new("Part")
                star.Size = Vector3.new(0.5,0.5,3)
                star.Position = startPos
                star.Anchored = true
                star.CanCollide = false
                star.Material = Enum.Material.Neon
                star.Color = color
                star.Name = "ShootingStar"
                star.Parent = shootingStarsFolder
                addInstance(star)
                
                local att0 = Instance.new("Attachment",star)
                local att1 = Instance.new("Attachment",star)
                att1.Position = Vector3.new(0,0,-3)
                addInstance(att0)
                addInstance(att1)
                
                local trail = Instance.new("Trail",star)
                trail.Attachment0 = att0
                trail.Attachment1 = att1
                trail.Lifetime = 0.35
                trail.Color = trailColor
                trail.LightEmission = 1
                trail.WidthScale = NumberSequence.new({NumberSequenceKeypoint.new(0,1),NumberSequenceKeypoint.new(1,0)})
                addInstance(trail)
                
                local light = Instance.new("PointLight",star)
                light.Brightness = isFire and 12 or 7
                light.Range = 35
                light.Color = color
                addInstance(light)
                
                if isFire then
                    local fire = Instance.new("Fire",star)
                    fire.Heat = 15
                    fire.Size = 3.5
                    fire.Color = Color3.fromRGB(255,110,0)
                    fire.SecondaryColor = Color3.fromRGB(255,210,0)
                    addInstance(fire)
                end
                
                local lifetime = math.random(1,1.5)
                local timePassed = 0
                local moveConn
                moveConn = RunService.Heartbeat:Connect(function(dt)
                    if not active or not _G.SistemaAtivo then 
                        moveConn:Disconnect() 
                        if star.Parent then star:Destroy() end 
                        return 
                    end
                    timePassed += dt
                    if timePassed >= lifetime then 
                        moveConn:Disconnect() 
                        if star.Parent then star:Destroy() end 
                        return 
                    end
                    local curve = math.sin(timePassed*20)*0.5
                    star.Position += (dir+Vector3.new(0,curve,0)).Unit*speed*dt
                end)
                addConnection(moveConn)
                Debris:AddItem(star,4)
            end

            local function updateSky()
                if not _G.SistemaAtivo then return end
                local hour = Lighting.ClockTime
                local shouldBeActive = hour >= 18 or hour < 6
                if shouldBeActive and not active then
                    active = true
                    Lighting.FogColor = Color3.fromRGB(10,10,30)
                    Lighting.FogEnd = 5000
                    Lighting.Brightness = 2
                    for _,s in ipairs(stars) do if s and s.Parent then s:Destroy() end end
                    stars = {}
                    for _,p in ipairs(shootingStarsFolder:GetChildren()) do p:Destroy() end
                    for i=1,STAR_COUNT do createStar() end
                    spaceSound:Play()
                elseif not shouldBeActive and active then
                    active = false
                    for _,s in ipairs(stars) do if s and s.Parent then s:Destroy() end end
                    stars = {}
                    for _,p in ipairs(shootingStarsFolder:GetChildren()) do p:Destroy() end
                    spaceSound:Stop()
                    Lighting.FogColor = Color3.fromRGB(192,192,192)
                    Lighting.FogEnd = 100000
                    Lighting.Brightness = 2
                end
            end

            local shootingStarConn = task.spawn(function()
                while _G.SistemaAtivo do
                    if active then
                        for i=1,SHOOTING_STAR_MAX do
                            createShootingStar()
                            task.wait(shootingStarCooldown)
                        end
                    else
                        task.wait(1)
                    end
                end
            end)
            addConnection(shootingStarConn)

            local skyUpdateConn = task.spawn(function()
                while _G.SistemaAtivo do
                    updateSky()
                    task.wait(1)
                end
            end)
            addConnection(skyUpdateConn)

            local rainFolder = Instance.new("Folder",workspace)
            rainFolder.Name = "FakeRain"
            addInstance(rainFolder)
            local isRaining = false

            local birds = Instance.new("Sound",SoundService)
            birds.SoundId = "rbxassetid://9111139882"
            birds.Volume = 0.2
            birds.Looped = true
            birds:Play()
            addInstance(birds)

            local rainSound = Instance.new("Sound",SoundService)
            rainSound.SoundId = "rbxassetid://9118823106"
            rainSound.Volume = 0.3
            rainSound.Looped = true
            rainSound:Play()
            addInstance(rainSound)

            local thunder = Instance.new("Sound",SoundService)
            thunder.SoundId = "rbxassetid://9120018695"
            thunder.Volume = 0.4
            addInstance(thunder)

            local function updateBirdSound()
                birds.Volume = isRaining and 0 or 0.2
            end

            local function spawnRain()
                if not _G.SistemaAtivo then return end
                isRaining = true
                updateBirdSound()
                for i=1,120 do
                    local drop = Instance.new("Part")
                    drop.Size = Vector3.new(0.1,2,0.1)
                    drop.Anchored = true
                    drop.CanCollide = false
                    drop.Material = Enum.Material.Glass
                    drop.Transparency = 0.5
                    drop.Color = Color3.fromRGB(160,160,255)
                    drop.Position = Vector3.new(math.random(-150,150),100,math.random(-150,150))
                    drop.Parent = rainFolder
                    addInstance(drop)
                    local tween = TweenService:Create(drop,TweenInfo.new(1),{Position=drop.Position-Vector3.new(0,60,0)})
                    tween:Play()
                    Debris:AddItem(drop,1.5)
                end
                wait(1.5)
                isRaining = false
                updateBirdSound()
            end

            local function lightningStrike()
                if not _G.SistemaAtivo then return end
                local flash = Instance.new("Part")
                flash.Size = Vector3.new(1,1000,1)
                flash.Anchored = true
                flash.CanCollide = false
                flash.Transparency = 0.4
                flash.Material = Enum.Material.Neon
                flash.Color = Color3.new(1,1,1)
                flash.Position = Vector3.new(math.random(-100,100),500,math.random(-100,100))
                flash.Parent = workspace
                addInstance(flash)
                Lighting.Brightness = Lighting.Brightness + 1.5
                thunder:Play()
                wait(0.1)
                Lighting.Brightness = Lighting.Brightness - 1.5
                flash:Destroy()
            end

            for _,part in pairs(workspace:GetDescendants()) do
                if part:IsA("BasePart") and part.Material == Enum.Material.SmoothPlastic then
                    part.Reflectance = 0.25
                end
            end

            local rainConn = task.spawn(function()
                while _G.SistemaAtivo do
                    spawnRain()
                    if math.random() < 0.2 then lightningStrike() end
                    wait(1)
                end
            end)
            addConnection(rainConn)

            Lighting.Brightness = 2
            Lighting.GlobalShadows = true
            Lighting.OutdoorAmbient = Color3.fromRGB(70, 70, 70)
            Lighting.FogColor = Color3.fromRGB(120, 130, 140)
            Lighting.FogStart = 80
            Lighting.FogEnd = 600
            Lighting.EnvironmentSpecularScale = 1
            Lighting.EnvironmentDiffuseScale = 0.5

            local sky = Instance.new("Sky")
            sky.SkyboxBk = "rbxassetid://159454299"
            sky.SkyboxDn = "rbxassetid://159454296"
            sky.SkyboxFt = "rbxassetid://159454293"
            sky.SkyboxLf = "rbxassetid://159454286"
            sky.SkyboxRt = "rbxassetid://159454300"
            sky.SkyboxUp = "rbxassetid://159454304"
            sky.Parent = Lighting
            addInstance(sky)

            local color = Instance.new("ColorCorrectionEffect", Lighting)
            color.Brightness = 0.03
            color.Contrast = 0.15
            color.Saturation = 0.05
            color.TintColor = Color3.fromRGB(255, 240, 220)
            addInstance(color)

            local bloom = Instance.new("BloomEffect", Lighting)
            bloom.Intensity = 0.8
            bloom.Size = 56
            bloom.Threshold = 0.9
            addInstance(bloom)

            local sunRays = Instance.new("SunRaysEffect", Lighting)
            sunRays.Intensity = 0.05
            sunRays.Spread = 0.8
            addInstance(sunRays)

            local blur = Instance.new("BlurEffect", Lighting)
            blur.Size = 0
            addInstance(blur)

        else
            _G.SistemaAtivo = false
            
            if _G.SistemaConnections then
                for _, connection in pairs(_G.SistemaConnections) do
                    if connection then
                        pcall(function() connection:Disconnect() end)
                    end
                end
                _G.SistemaConnections = {}
            end
            
            if _G.SistemaInstances then
                for _, instance in pairs(_G.SistemaInstances) do
                    if instance and instance.Parent then
                        pcall(function() instance:Destroy() end)
                    end
                end
                _G.SistemaInstances = {}
            end
            
            local Lighting = game:GetService("Lighting")
            Lighting.Brightness = 1
            Lighting.FogColor = Color3.fromRGB(191, 191, 191)
            Lighting.FogEnd = 100000
            Lighting.FogStart = 0
            Lighting.GlobalShadows = true
            Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
            
            for _, effect in pairs(Lighting:GetChildren()) do
                if effect:IsA("BloomEffect") or effect:IsA("ColorCorrectionEffect") or 
                   effect:IsA("SunRaysEffect") or effect:IsA("BlurEffect") or effect:IsA("Sky") then
                    effect:Destroy()
                end
            end
            
            if workspace:FindFirstChild("ShootingStars") then
                workspace.ShootingStars:Destroy()
            end
            if workspace:FindFirstChild("FakeRain") then
                workspace.FakeRain:Destroy()
            end
            
            for _, sound in pairs(workspace:GetDescendants()) do
                if sound:IsA("Sound") and (sound.Name == "SpaceAmbience" or sound.Name == "FountainSound" or sound.Name == "MyCustomSound") then
                    sound:Stop()
                end
            end
            
            for _, sound in pairs(SoundService:GetDescendants()) do
                if sound:IsA("Sound") then
                    sound:Stop()
                end
            end
        end
    end
})


