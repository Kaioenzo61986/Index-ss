local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local ExecuteButton = Instance.new("TextButton")
local ClearButton = Instance.new("TextButton")
local CopyButton = Instance.new("TextButton")
local ClipboardButton = Instance.new("TextButton")
local CommandInput = Instance.new("TextBox")

-- Configurações do GUI
ScreenGui.Name = "Index SS"  -- Nome do script
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
MainFrame.Parent = ScreenGui

CommandInput.Size = UDim2.new(1, 0, 0, 50)
CommandInput.Position = UDim2.new(0, 0, 0, 0)
CommandInput.PlaceholderText = "Digite seu comando aqui..."
CommandInput.Parent = MainFrame

ExecuteButton.Size = UDim2.new(0, 100, 0, 50)
ExecuteButton.Position = UDim2.new(0, 10, 0, 60)
ExecuteButton.Text = "Executar"
ExecuteButton.Parent = MainFrame

ClearButton.Size = UDim2.new(0, 100, 0, 50)
ClearButton.Position = UDim2.new(0, 10, 0, 120)
ClearButton.Text = "Limpar"
ClearButton.Parent = MainFrame

CopyButton.Size = UDim2.new(0, 100, 0, 50)
CopyButton.Position = UDim2.new(0, 10, 0, 180)
CopyButton.Text = "Copiar Script"
CopyButton.Parent = MainFrame

ClipboardButton.Size = UDim2.new(0, 100, 0, 50)
ClipboardButton.Position = UDim2.new(0, 10, 0, 240)
ClipboardButton.Text = "Executar da Área de Transferência"
ClipboardButton.Parent = MainFrame

-- Funções
local function executeCommand(command)
    local success, err = pcall(function()
        loadstring(command)()
    end)
    if not success then
        print("Erro: " .. err)
    end
end

ExecuteButton.MouseButton1Click:Connect(function()
    local command = CommandInput.Text
    executeCommand(command)
end)

ClearButton.MouseButton1Click:Connect(function()
    CommandInput.Text = ""
end)

CopyButton.MouseButton1Click:Connect(function()
    setclipboard(CommandInput.Text)
end)

ClipboardButton.MouseButton1Click:Connect(function()
    local clipboardText = getclipboard()
    executeCommand(clipboardText)
end)

