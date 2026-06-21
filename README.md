# hack.local x = library:CreateWindow("Hack")

local b = x:CreateFolder("local-player")

b:DestroyGui()

local S = 16
local J = 50

b:Box("speed", "number", function(val)
    S = tonumber(val) or 16
end)

b:Box("jump", "number", function(val)
    J = tonumber(val) or 50
end)

b:Toggle("Reset", function(kill)
    local Character = game.Players.LocalPlayer.Character
    local Humanoid = Character and Character:FindFirstChild("Humanoid")

    if Humanoid then
        if kill then
            Humanoid.Health = 0
        else
            Humanoid.Health = 100
        end
    end
end)

function Chat(Mes, Freq)
    spawn(function()
        while getgenv().Chat do
            local args = {
                [1] = Mes,
                [2] = "All"
            }

            game:GetService("ReplicatedStorage")
                .DefaultChatSystemChatEvents
                .SayMessageRequest
                :FireServer(unpack(args))

            wait(Freq)
        end
    end)
end

function Speed(Nume)
    spawn(function()
        while getgenv().Speed do
            local Humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")

            if Humanoid then
                Humanoid.WalkSpeed = Nume
            end

            wait()
        end

        local Humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if Humanoid then
            Humanoid.WalkSpeed = 16
        end
    end)
end

function Jump(Nume)
    spawn(function()
        while getgenv().Jump do
            local Humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")

            if Humanoid then
                Humanoid.JumpPower = Nume
            end

            wait()
        end

        local Humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if Humanoid then
            Humanoid.JumpPower = 50
        end
    end)
end
