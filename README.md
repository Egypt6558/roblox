local library = loadstring(game:HttpGet(('https://github.com/DevSloPo/Auto/raw/main/Ware-obfuscated.lua')))()

    local window = library:new("新脚本")
    local XKHub = window:Tab("关于", "7733774602")
    local XK = XKHub:section("示例", true)
    
    XK:Label("文本标签")
    
    XK:Button(
        "点击",
        function()
            
        end)
    
    XK:Toggle("开关", "", false, function(state)

    end)
    
    XK:Slider("滑块", "", 16, 0, 100, false, function(v)

    end)
    
    XK:Dropdown("Dropdown", "", { "0", "1", "2", "3", "4", "5", "6", "7", "8", "9" }, function(s)
	print(s)
    end)

    XK:Textbox("输入文本", "", "输入", function(s)
	
    end)    
    
    local XKHub = window:Tab("其他", "78892482588180")
    local XKNB = XKHub:section("内容", true)
    
    XKNB:Label("文本标签")
    
    XKNB:Button(
        "点击",
        function()
            
        end)
    
    XKNB:Toggle("开关", "", false, function(state)

    end)
    
    XKNB:Slider("滑块", "", 16, 0, 100, false, function(v)

    end)
    
    XKNB:Dropdown("Dropdown", "", { "0", "1", "2", "3", "4", "5", "6", "7", "8", "9" }, function(s)
	print(s)
    end)

    XKNB:Textbox("输入文本", "", "输入", function(s)
	
    end)
