local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- สร้างหน้าต่าง UI
local Window = Rayfield:CreateWindow({
    Name = "Auto Clicker - GameService",
    LoadingTitle = "กำลังโหลดระบบ...",
    LoadingSubtitle = "by กูเอง",
    ConfigurationSaving = {
        Enabled = false,
    },
    KeySystem = false,
})

local Tab = Window:CreateTab("Main", "home")

-- ตัวแปรควบคุมระบบ
local running = false
local args = { 3 }
local remote = game:GetService("ReplicatedStorage")
    :WaitForChild("src")
    :WaitForChild("Packages")
    :WaitForChild("Knit")
    :WaitForChild("Services")
    :WaitForChild("GameService")
    :WaitForChild("RE")
    :WaitForChild("HandleClick")

-- ฟังก์ชันลูปยิง
task.spawn(function()
    while true do
        if running then
            pcall(function()
                remote:FireServer(unpack(args))
            end)
        end
        task.wait(0.1) -- ปรับเวลาหน่วงตรงนี้ได้ตามใจชอบ (วินาที)
    end
end)

-- ปุ่มเปิด-ปิด
Tab:CreateToggle({
    Name = "เปิด/ปิด ระบบคลิก",
    CurrentValue = false,
    Flag = "AutoClickToggle",
    Callback = function(Value)
        running = Value
        if Value then
            print("เปิดระบบแล้วไอ้สัตว์!")
        else
            print("ปิดระบบละ!")
        end
    end,
})
