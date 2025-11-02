local Translations = {
    ["Main"] = "主菜单",
    ["Misc"] = "杂项",
    ["Settings"] = "设置",
    ["Themes"] = "主题",
    ["Config"] = "配置",
    ["Cooldowns"] = "冷却相关",
    ["No Dash Cooldown"] = "无冲刺冷却",
    ["No Stun"] = "无眩晕",
    ["Anti combo"] = "反连招",
    ["Invisibility"] = "隐身",
    ["Speedhack"] = "速度修改",
    ["Speed"] = "速度",
    ["Rejoin Server"] = "重新加入服务器",
    ["VFX color"] = "特效颜色",
    ["Tp to areas"] = "传送至区域",
    ["Select a area..."] = "选择一个区域...",
    ["Tp"] = "传送",
    ["toggle Speed"] = "切换速度",
    ["Toggle 速度"] = "切换速度",
    ["Middle"] = "中部区域",
    ["Subway"] = "地铁区域",
    ["Bar"] = "酒吧区域",
    ["On top of arena"] = "竞技场顶部",
    ["Background Buildings"] = "背景建筑区域",
    ["Outside of arena"] = "竞技场外部",
    ["Bleachers"] = "观众席区域"
}
 
local function translateText(text)
    if not text or type(text) ~= "string" then return text end
    
    if Translations[text] then
        return Translations[text]
    end
    
    for en, cn in pairs(Translations) do
        if text:find(en) then
            return text:gsub(en, cn)
        end
    end
    
    return text
end

local function setupTranslationEngine()
    local success, err = pcall(function()
        local oldIndex = getrawmetatable(game).__newindex
        setreadonly(getrawmetatable(game), false)
        
        getrawmetatable(game).__newindex = newcclosure(function(t, k, v)
            if (t:IsA("TextLabel") or t:IsA("TextButton") or t:IsA("TextBox")) and k == "Text" then
                v = translateText(tostring(v))
            end
            return oldIndex(t, k, v)
        end)
        
        setreadonly(getrawmetatable(game), true)
    end)
    
    if not success then
        warn("元表劫持失败:", err)
       
        local translated = {}
        local function scanAndTranslate()
            for _, gui in ipairs(game:GetService("CoreGui"):GetDescendants()) do
                if (gui:IsA("TextLabel") or gui:IsA("TextButton") or gui:IsA("TextBox")) and not translated[gui] then
                    pcall(function()
                        local text = gui.Text
                        if text and text ~= "" then
                            local translatedText = translateText(text)
                            if translatedText ~= text then
                                gui.Text = translatedText
                                translated[gui] = true
                            end
                        end
                    end)
                end
            end
            
            local player = game:GetService("Players").LocalPlayer
            if player and player:FindFirstChild("PlayerGui") then
                for _, gui in ipairs(player.PlayerGui:GetDescendants()) do
                    if (gui:IsA("TextLabel") or gui:IsA("TextButton") or gui:IsA("TextBox")) and not translated[gui] then
                        pcall(function()
                            local text = gui.Text
                            if text and text ~= "" then
                                local translatedText = translateText(text)
                                if translatedText ~= text then
                                    gui.Text = translatedText
                                    translated[gui] = true
                                end
                            end
                        end)
                    end
                end
            end
        end
        
        local function setupDescendantListener(parent)
            parent.DescendantAdded:Connect(function(descendant)
                if descendant:IsA("TextLabel") or descendant:IsA("TextButton") or descendant:IsA("TextBox") then
                    task.wait(0.1)
                    pcall(function()
                        local text = descendant.Text
                        if text and text ~= "" then
                            local translatedText = translateText(text)
                            if translatedText ~= text then
                                descendant.Text = translatedText
                            end
                        end
                    end)
                end
            end)
        end
        
        pcall(setupDescendantListener, game:GetService("CoreGui"))
        local player = game:GetService("Players").LocalPlayer
        if player and player:FindFirstChild("PlayerGui") then
            pcall(setupDescendantListener, player.PlayerGui)
        end
        
        while true do
            scanAndTranslate()
            task.wait(3)
        end
    end
end

task.wait(2)

setupTranslationEngine()

local success, err = pcall(function()
loadstring(game:HttpGet("https://raw.githubusercontent.com/solarastuff/hbg/refs/heads/main/academic.lua"))()


end)

if not success then
    warn("加载失败:", err)
end
