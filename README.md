local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

local function CreateESP(player)
    local BillboardGui = Instance.new("BillboardGui")
    BillboardGui.Name = "ESP"
    BillboardGui.AlwaysOnTop = true
    BillboardGui.Size = UDim2.new(0, 200, 0, 50)
    BillboardGui.StudsOffset = Vector3.new(0, 3, 0)

    local TextLabel = Instance.new("TextLabel", BillboardGui)
    TextLabel.Text = player.Name
    TextLabel.BackgroundTransparency = 1
    TextLabel.TextSize = 14
    TextLabel.Font = Enum.Font.SourceSans
    TextLabel.TextColor3 = Color3.new(1, 0, 0)
    TextLabel.Size = UDim2.new(1, 0, 1, 0)

    BillboardGui.Parent = player.Character:WaitForChild("Head")
end

local function OnPlayerAdded(player)
    if player ~= LocalPlayer then
        player.CharacterAdded:Connect(function(character)
            CreateESP(player)
        end)
    end
end

Players.PlayerAdded:Connect(OnPlayerAdded)

for _, player in pairs(Players:GetPlayers()) do
    OnPlayerAdded(player)
end
