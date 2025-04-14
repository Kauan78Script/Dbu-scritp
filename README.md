-- Criação da Interface Gráfica (UI)
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer.PlayerGui
screenGui.ResetOnSpawn = false

-- Criando o botão de Auto Farm
local autoFarmButton = Instance.new("TextButton")
autoFarmButton.Size = UDim2.new(0, 200, 0, 50)
autoFarmButton.Position = UDim2.new(0, 20, 0, 20)
autoFarmButton.Text = "Auto Farm: Off"
autoFarmButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
autoFarmButton.TextColor3 = Color3.fromRGB(255, 255, 255)
autoFarmButton.Parent = screenGui

-- Criando o botão de Auto Rebirth
local autoRebirthButton = Instance.new("TextButton")
autoRebirthButton.Size = UDim2.new(0, 200, 0, 50)
autoRebirthButton.Position = UDim2.new(0, 20, 0, 80)
autoRebirthButton.Text = "Auto Rebirth: Off"
autoRebirthButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
autoRebirthButton.TextColor3 = Color3.fromRGB(255, 255, 255)
autoRebirthButton.Parent = screenGui

-- Variáveis de Configuração
local poderNecessarioParaFarm = 100
local poderNecessarioParaRebirth = 1000
local intervaloFarm = 1
local multiplicadorBonus = 2

-- Variáveis de Estado
local autoFarmAtivo = false
local autoRebirthAtivo = false

-- Função de Auto Farm
local function autoFarm(player)
    while autoFarmAtivo do
        local poder = player:FindFirstChild("Poder")
        if poder and poder.Value < poderNecessarioParaFarm then
            poder.Value = poder.Value + 10
        end
        wait(intervaloFarm)
    end
end

-- Função de Auto Rebirth
local function autoRebirth(player)
    while true do
        local poder = player:FindFirstChild("Poder")
        if poder and poder.Value >= poderNecessarioParaRebirth then
            poder.Value = 0
            local bonus = Instance.new("IntValue")
            bonus.Name = "MultiplicadorPoder"
            bonus.Value = multiplicadorBonus
            bonus.Parent = player
            print("Rebirth realizado! Multiplicador de poder ativado.")
            wait(5)
        end
        wait(1)
    end
end

-- Alternando o Auto Farm
autoFarmButton.MouseButton1Click:Connect(function()
    autoFarmAtivo = not autoFarmAtivo
    if autoFarmAtivo then
        autoFarmButton.Text = "Auto Farm: On"
        autoFarmButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        autoFarm(game.Players.LocalPlayer)
    else
        autoFarmButton.Text = "Auto Farm: Off"
        autoFarmButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    end
end)

-- Alternando o Auto Rebirth
autoRebirthButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local poder = player:FindFirstChild("Poder")

    if poder and poder.Value >= poderNecessarioParaRebirth then
        autoRebirthAtivo = not autoRebirthAtivo
        if autoRebirthAtivo then
            autoRebirthButton.Text = "Auto Rebirth: On"
            autoRebirthButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
            autoRebirth(player)
        else
            autoRebirthButton.Text = "Auto Rebirth: Off"
            autoRebirthButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        end
    else
        autoRebirthButton.Text = "Auto Rebirth: Off"
        autoRebirthButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        print("Você não tem poder suficiente para rebirth.")
    end
end)
# Dbu-scritp
