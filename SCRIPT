local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")

local aimbotEnabled = false
local aimbotTarget = nil

function findNearestEnemy()
    local nearestDistance = math.huge
    local nearestPlayer = nil

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Team ~= LocalPlayer.Team then
            local distance = (player.Character.Head.Position - LocalPlayer.Character.Head.Position).magnitude
            if distance < nearestDistance then
                nearestDistance = distance
                nearestPlayer = player
            end
        end
    end

    return nearestPlayer
end

function aimAtTarget()
    if aimbotTarget then
        local cameraCFrame = LocalPlayer.Character.Head.CFrame
        local targetCFrame = aimbotTarget.Character.Head.CFrame
        local direction = (targetCFrame.p - cameraCFrame.p).unit
        LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(cameraCFrame.p, cameraCFrame.p + direction * 100)
    end
end

UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end

    if input.KeyCode == Enum.KeyCode.Q then
        aimbotEnabled = not aimbotEnabled
        aimbotTarget = aimbotEnabled and findNearestEnemy() or nil
    end
end)

RunService:BindToRenderStep("AimAtTarget", Enum.RenderPriority.Last.Value, function()
    if aimbotEnabled then
        aimAtTarget()
    end
end)
