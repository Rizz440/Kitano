-- โหลด Library ที่ใช้ในการสร้าง UI
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/lime"))()

-- สร้างหน้าต่าง UI หลักชื่อ "Kitano Hub"
local w = Library:Window("Kitano Hub")

-- สร้างปุ่มที่เมื่อคลิกจะพิมพ์คำว่า "Printed" ลงในคอนโซล และสร้างเครื่องมือ Teleport
w:Button("บล็อกวาป", function()
    print("Printed")

    -- สร้างตัวแปร mouse และ tool
    local mouse = game.Players.LocalPlayer:GetMouse()
    local tool = Instance.new("Tool")
    
    tool.RequiresHandle = false
    tool.Name = "มอสเกย์พาวาป"
    
    tool.Activated:Connect(function()
        local pos = mouse.Hit + Vector3.new(0, 2.5, 0)
        pos = CFrame.new(pos.X, pos.Y, pos.Z)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = pos
    end)
    
    tool.Parent = game.Players.LocalPlayer.Backpack
end)

-- สร้าง Toggle สำหรับ "ล็อกเป้า"
local isAiming = false
local fov = 50
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local Cam = game.Workspace.CurrentCamera

local FOVring = Drawing.new("Circle")
FOVring.Visible = false
FOVring.Thickness = 2
FOVring.Color = Color3.fromRGB(128, 0, 128) -- Purple color
FOVring.Filled = false
FOVring.Radius = fov
FOVring.Position = Cam.ViewportSize / 2

local function updateDrawings()
    local camViewportSize = Cam.ViewportSize
    FOVring.Position = camViewportSize / 2
end

local function onKeyDown(input)
    if input.KeyCode == Enum.KeyCode.Delete then
        RunService:UnbindFromRenderStep("FOVUpdate")
        FOVring:Remove()
        isAiming = false
    end
end

UserInputService.InputBegan:Connect(onKeyDown)

local function lookAt(target)
    local lookVector = (target - Cam.CFrame.Position).unit
    local newCFrame = CFrame.new(Cam.CFrame.Position, Cam.CFrame.Position + lookVector)
    Cam.CFrame = newCFrame
end

local function getClosestPlayerInFOV(trg_part)
    local nearest = nil
    local last = math.huge
    local playerMousePos = Cam.ViewportSize / 2

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= Players.LocalPlayer then
            local part = player.Character and player.Character:FindFirstChild(trg_part)
            if part then
                local ePos, isVisible = Cam:WorldToViewportPoint(part.Position)
                local distance = (Vector2.new(ePos.x, ePos.y) - playerMousePos).Magnitude

                if distance < last and isVisible and distance < fov then
                    last = distance
                    nearest = player
                end
            end
        end
    end

    return nearest
end

w:Toggle("ล็อกเป้า", function(v)
    isAiming = v
    FOVring.Visible = v

    if v then
        RunService:BindToRenderStep("FOVUpdate", Enum.RenderPriority.Camera.Value, function()
            updateDrawings()
            local closest = getClosestPlayerInFOV("Head")
            if closest and closest.Character:FindFirstChild("Head") then
                lookAt(closest.Character.Head.Position)
            end
        end)
    else
        RunService:UnbindFromRenderStep("FOVUpdate")
        FOVring.Visible = false
    end
end)

-- สร้าง Toggle สำหรับ "วิ่งเร็ว 80%"
w:Toggle("วิ่งเร็ว 80%", function(v)
    if v then
        print("ฟังก์ชันที่สอง เปิดใช้งาน")
        
        -- เพิ่มโค้ดสำหรับปรับความเร็วการเดิน
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
-- โหลด Library ที่ใช้ในการสร้าง UI
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/lime"))()

-- สร้างหน้าต่าง UI หลักชื่อ "Kitano Hub"
local w = Library:Window("Kitano Hub")

-- สร้างปุ่มที่เมื่อคลิกจะพิมพ์คำว่า "Printed" ลงในคอนโซล และสร้างเครื่องมือ Teleport
w:Button("บล็อกวาป", function()
    print("Printed")

    -- สร้างตัวแปร mouse และ tool
    local mouse = game.Players.LocalPlayer:GetMouse()
    local tool = Instance.new("Tool")
    
    tool.RequiresHandle = false
    tool.Name = "มอสเกย์พาวาป"
    
    tool.Activated:Connect(function()
        local pos = mouse.Hit + Vector3.new(0, 2.5, 0)
        pos = CFrame.new(pos.X, pos.Y, pos.Z)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = pos
    end)
    
    tool.Parent = game.Players.LocalPlayer.Backpack
end)

-- สร้าง Toggle สำหรับ "ล็อกเป้า"
local isAiming = false
local fov = 50
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local Cam = game.Workspace.CurrentCamera

local FOVring = Drawing.new("Circle")
FOVring.Visible = false
FOVring.Thickness = 2
FOVring.Color = Color3.fromRGB(128, 0, 128) -- Purple color
FOVring.Filled = false
FOVring.Radius = fov
FOVring.Position = Cam.ViewportSize / 2

local function updateDrawings()
    local camViewportSize = Cam.ViewportSize
    FOVring.Position = camViewportSize / 2
end

local function onKeyDown(input)
    if input.KeyCode == Enum.KeyCode.Delete then
        RunService:UnbindFromRenderStep("FOVUpdate")
        FOVring:Remove()
        isAiming = false
    end
end

UserInputService.InputBegan:Connect(onKeyDown)

local function lookAt(target)
    local lookVector = (target - Cam.CFrame.Position).unit
    local newCFrame = CFrame.new(Cam.CFrame.Position, Cam.CFrame.Position + lookVector)
    Cam.CFrame = newCFrame
end

local function getClosestPlayerInFOV(trg_part)
    local nearest = nil
    local last = math.huge
    local playerMousePos = Cam.ViewportSize / 2

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= Players.LocalPlayer then
            local part = player.Character and player.Character:FindFirstChild(trg_part)
            if part then
                local ePos, isVisible = Cam:WorldToViewportPoint(part.Position)
                local distance = (Vector2.new(ePos.x, ePos.y) - playerMousePos).Magnitude

                if distance < last and isVisible and distance < fov then
                    last = distance
                    nearest = player
                end
            end
        end
    end

    return nearest
end

w:Toggle("ล็อกเป้า", function(v)
    isAiming = v
    FOVring.Visible = v

    if v then
        RunService:BindToRenderStep("FOVUpdate", Enum.RenderPriority.Camera.Value, function()
            updateDrawings()
            local closest = getClosestPlayerInFOV("Head")
            if closest and closest.Character:FindFirstChild("Head") then
                lookAt(closest.Character.Head.Position)
            end
        end)
    else
        RunService:UnbindFromRenderStep("FOVUpdate")
        FOVring.Visible = false
    end
end)

-- สร้าง Toggle สำหรับ "วิ่งเร็ว 80%"
w:Toggle("วิ่งเร็ว 80%", function(v)
    if v then
        print("ฟังก์ชันที่สอง เปิดใช้งาน")
        
        -- เพิ่มโค้ดสำหรับปรับความเร็วการเดิน
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")

        local currentWalkSpeed = humanoid.WalkSpeed
        local newWalkSpeed = currentWalkSpeed * 1.8
        humanoid.WalkSpeed = newWalkSpeed
        
    else
        print("ฟังก์ชันที่สอง ปิดใช้งาน")
        
        -- รีเซ็ตความเร็วการเดินกลับไปยังค่าปกติ
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")

        humanoid.WalkSpeed = humanoid.WalkSpeed / 1.8
    end
end)

-- สร้าง Toggle สำหรับ "มุมมองแบบกว้าง"
local fovConnection
w:Toggle("มุมมองแบบกว้าง", function(v)
    if v then
        print("ฟังก์ชันที่สาม เปิดใช้งาน")
        
        -- เพิ่มโค้ดสำหรับการมองทะลุผ่านวัตถุ
        local camera = workspace.CurrentCamera
        
        local function onRenderStep()
            -- ปรับค่าของ FieldOfView เพื่อให้มองทะลุ
            camera.FieldOfView = 800  -- เพิ่มค่า FieldOfView เพื่อให้มองเห็นผ่านวัตถุ
        end

        -- เชื่อมต่อฟังก์ชันกับ RenderStepped
        fovConnection = game:GetService("RunService").RenderStepped:Connect(onRenderStep)

    else
        print("ฟังก์ชันที่สาม ปิดใช้งาน")

        -- รีเซ็ตค่า FieldOfView กลับเป็นค่าปกติ
        local camera = workspace.CurrentCamera
        camera.FieldOfView = 70  -- ค่า FieldOfView ปกติของกล้อง

        -- ยกเลิกการเชื่อมต่อฟังก์ชันกับ RenderStepped
        if fovConnection then
            fovConnection:Disconnect()
            fovConnection = nil
        end
    end
end)

-- สร้าง Toggle สำหรับ "กระโดดสูงไม่บอก%🤫"
w:Toggle("กระโดดสูงไม่บอก%🤫", function(v)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")

    if v then
        print("ฟังก์ชันที่สี่ เปิดใช้งาน")

        -- เพิ่มโค้ดสำหรับปรับค่า JumpPower
        humanoid.JumpPower = humanoid.JumpPower * 2

    else
        print("ฟังก์ชันที่สี่ ปิดใช้งาน")

        -- รีเซ็ตค่า JumpPower กลับเป็นค่าปกติ
        humanoid.JumpPower = humanoid.JumpPower / 2
    end
end)

-- สร้าง Toggle สำหรับ "ฟังก์ชันที่ห้า"
w:Toggle("ยังคิดไม่ออก", function(v)
    if v then
        print("ฟังก์ชันที่ห้า เปิดใช้งาน")
        -- ใส่โค้ดสำหรับฟังก์ชันที่ห้าที่นี่
    else
        print("ฟังก์ชันที่ห้า ปิดใช้งาน")
        -- ใส่โค้ดสำหรับฟังก์ชันที่ห้าที่นี่
    end
end)￼Enter
        local currentWalkSpeed = humanoid.WalkSpeed
        local newWalkSpeed = currentWalkSpeed * 1.8
        humanoid.WalkSpeed = newWalkSpeed
        
    else
        print("ฟังก์ชันที่สอง ปิดใช้งาน")
        
        -- รีเซ็ตความเร็วการเดินกลับไปยังค่าปกติ
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")

        humanoid.WalkSpeed = humanoid.WalkSpeed / 1.8
    end
end)

-- สร้าง Toggle สำหรับ "มุมมองแบบกว้าง"
local fovConnection
w:Toggle("มุมมองแบบกว้าง", function(v)
    if v then
        print("ฟังก์ชันที่สาม เปิดใช้งาน")
        
        -- เพิ่มโค้ดสำหรับการมองทะลุผ่านวัตถุ
        local camera = workspace.CurrentCamera
        
  local function onRenderStep()
            -- ปรับค่าของ FieldOfView เพื่อให้มองทะลุ
            camera.FieldOfView = 800  -- เพิ่มค่า FieldOfView เพื่อให้มองเห็นผ่านวัตถุ
        end

        -- เชื่อมต่อฟังก์ชันกับ RenderStepped
        fovConnection = game:GetService("RunService").RenderStepped:Connect(onRenderStep)

    else
        print("ฟังก์ชันที่สาม ปิดใช้งาน")

        -- รีเซ็ตค่า FieldOfView กลับเป็นค่าปกติ
        local camera = workspace.CurrentCamera
        camera.FieldOfView = 70  -- ค่า FieldOfView ปกติของกล้อง

        -- ยกเลิกการเชื่อมต่อฟังก์ชันกับ RenderStepped
        if fovConnection then
            fovConnection:Disconnect()
            fovConnection = nil
        end
    end
end)

-- สร้าง Toggle สำหรับ "กระโดดสูงไม่บอก%🤫"
w:Toggle("กระโดดสูงไม่บอก%🤫", function(v)
    local player = game.Players.LocalPlayer
