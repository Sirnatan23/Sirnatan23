-- GymRafinha com Menu Interativo
-- Aviso: Use este script por sua conta e risco.

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Configurações Iniciais
local treinoRapido = false
local autoEvento = false
local autoPocao = false
local autoEquipe = false
local intervaloMusculacao = 0.1

-- Função de musculação rápida
function iniciarMusculacao()
    while treinoRapido do
        local tool = character:FindFirstChildOfClass("Tool")
        if tool and tool:FindFirstChild("Activate") then
            tool:Activate()
        end
        wait(intervaloMusculacao)
    end
end

-- Função de auto evento
function participarEvento()
    while autoEvento do
        for _, evento in pairs(game.Workspace:GetDescendants()) do
            if evento:IsA("Part") and evento.Name == "Evento" then
                character:MoveTo(evento.Position)
                wait(1)
            end
        end
        wait(5)
    end
end

-- Criar o menu
local gui = Instance.new("ScreenGui")
gui.Name = "GymRafinhaMenu"
gui.Parent = game.CoreGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 250)
frame.Position = UDim2.new(0.5, -100, 0.5, -125)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
frame.Parent = gui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 50)
title.BackgroundTransparency = 1
title.Text = "GymRafinha Menu"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 20
title.Parent = frame

-- Criar botões para cada funcionalidade
local function criarBotao(nome, posicaoY, ativarFuncao)
    local botao = Instance.new("TextButton")
    botao.Size = UDim2.new(0.8, 0, 0, 40)
    botao.Position = UDim2.new(0.1, 0, 0, posicaoY)
    botao.Text = nome
    botao.TextColor3 = Color3.new(1, 1, 1)
    botao.Font = Enum.Font.SourceSans
    botao.TextSize = 18
    botao.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
    botao.Parent = frame

    -- Função ao clicar
    botao.MouseButton1Click:Connect(function()
        local estado = ativarFuncao()
        botao.Text = nome .. (estado and " (Ativado)" or " (Desativado)")
    end)
end

-- Ativar/desativar funções
criarBotao("Treino Rápido", 60, function()
    treinoRapido = not treinoRapido
    if treinoRapido then
        spawn(iniciarMusculacao)
    end
    return treinoRapido
end)

criarBotao("Auto Evento", 110, function()
    autoEvento = not autoEvento
    if autoEvento then
        spawn(participarEvento)
    end
    return autoEvento
end)

criarBotao("Auto Poção", 160, function()
    autoPocao = not autoPocao
    if autoPocao then
        -- Adicionar função de auto poção aqui
    end
    return autoPocao
end)

criarBotao("Auto Equipe", 210, function()
    autoEquipe = not autoEquipe
    if autoEquipe then
        -- Adicionar função de auto equipe aqui
    end
    return autoEquipe
end)

