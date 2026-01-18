-- HUB EDUCACIONAL FUNCIONAL

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local humanoid = char:WaitForChild("Humanoid")
local root = char:WaitForChild("HumanoidRootPart")

------------------------------------------------
-- ESTADOS
------------------------------------------------
local states = {
    InfiniteJump = false,
    Fly = false,
    Speed = false,
    GodMode = false
}

------------------------------------------------
-- GUI
------------------------------------------------
local gui = Instance.new("ScreenGui", player.PlayerGui)

-- BOTÃO PRETO
local openBtn = Instance.new("TextButton", gui)
openBtn.Size = UDim2.new(0,50,0,50)
openBtn.Position = UDim2.new(0,10,0.5,-25)
openBtn.BackgroundColor3 = Color3.new(0,0,0)
openBtn.Text = "≡"
openBtn.TextColor3 = Color3.new(1,1,1)
openBtn.TextScaled = true
openBtn.BorderSizePixel = 0
openBtn.Active = true
openBtn.Draggable = true

-- FRAME PRINCIPAL
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,260,0,320)
frame.Position = UDim2.new(0,70,0.3,0)
frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
frame.Visible = false
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,0,0,30)
title.Text = "HUB"
title.BackgroundColor3 = Color3.fromRGB(15,15,15)
title.TextColor3 = Color3.new(1,1,1)
title.BorderSizePixel = 0

-- SCROLL
local scroll = Instance.new("ScrollingFrame", frame)
scroll.Position = UDim2.new(0,0,0,35)
scroll.Size = UDim2.new(1,0,1,-35)
scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
scroll.CanvasSize = UDim2.new(0,0,0,0)
scroll.ScrollBarImageColor3 = Color3.new(1,1,1)

local layout = Instance.new("UIListLayout", scroll)
layout.Padding = UDim.new(0,8)

------------------------------------------------
-- FUNÇÃO BOTÃO TOGGLE REAL
------------------------------------------------
local function createToggle(name, callback)
    local btn = Instance.new("TextButton", scroll)
    btn.Size = UDim2.new(1,-10,0,35)
    btn.BackgroundColor3 = Color3.fromRGB(45,45,45)
    btn.TextColor3 = Color3.new(1,1,1)
    btn.BorderSizePixel = 0

    local on = false
    btn.Text = name .. " : OFF"

    btn.MouseButton1Click:Connect(function()
        on = not on
        btn.Text = name .. (on and " : ON" or " : OFF")
        callback(on)
    end)
end

------------------------------------------------
-- INFINITE JUMP (FUNCIONAL)
------------------------------------------------
UIS.JumpRequest:Connect(function()
    if states.InfiniteJump then
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

createToggle("Infinite Jump", function(v)
    states.InfiniteJump = v
end)

------------------------------------------------
-- SPEED (FUNCIONAL)
------------------------------------------------
createToggle("Speed", function(v)
    states.Speed = v
    humanoid.WalkSpeed = v and 50 or 16
end)

------------------------------------------------
-- GODMODE (FUNCIONAL)
------------------------------------------------
RunService.Stepped:Connect(function()
    if states.GodMode then
        humanoid.Health = humanoid.MaxHealth
    end
end)

createToggle("GodMode", function(v)
    states.GodMode = v
end)

------------------------------------------------
-- FLY (FUNCIONAL)
------------------------------------------------
local gyro, vel

createToggle("Fly", function(v)
    states.Fly = v

    if v then
        gyro = Instance.new("BodyGyro", root)
        vel = Instance.new("BodyVelocity", root)

        gyro.P = 9e4
        gyro.MaxTorque = Vector3.new(9e9,9e9,9e9)

        vel.MaxForce = Vector3.new(9e9,9e9,9e9)

        RunService:BindToRenderStep("Fly", 0, function()
            vel.Velocity = root.CFrame.LookVector * 60
            gyro.CFrame = workspace.CurrentCamera.CFrame
        end)
    else
        RunService:UnbindFromRenderStep("Fly")
        if gyro then gyro:Destroy() end
        if vel then vel:Destroy() end
    end
end)

------------------------------------------------
-- ABRIR / FECHAR
------------------------------------------------
openBtn.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)
