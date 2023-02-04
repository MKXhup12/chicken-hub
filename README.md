do
    local gui = game:GetService("CoreGui"):FindFirstChild("HovxrzGui")
    if gui then
        gui:Destroy()
    end
end

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local function MakeDraggable(topbarobject, object)
	local Dragging = nil
	local DragInput = nil
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos =
			UDim2.new(
				StartPosition.X.Scale,
				StartPosition.X.Offset + Delta.X,
				StartPosition.Y.Scale,
				StartPosition.Y.Offset + Delta.Y
			)
		local Tween = TweenService:Create(object, TweenInfo.new(0.2), {Position = pos})
		Tween:Play()
	end

	topbarobject.InputBegan:Connect(
		function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				Dragging = true
				DragStart = input.Position
				StartPosition = object.Position

				input.Changed:Connect(
					function()
						if input.UserInputState == Enum.UserInputState.End then
							Dragging = false
						end
					end
				)
			end
		end
	)

	topbarobject.InputChanged:Connect(
		function(input)
			if
				input.UserInputType == Enum.UserInputType.MouseMovement or
				input.UserInputType == Enum.UserInputType.Touch
			then
				DragInput = input
			end
		end
	)

	UserInputService.InputChanged:Connect(
		function(input)
			if input == DragInput and Dragging then
				Update(input)
			end
		end
	)
end

local library = {}

function library:CreateWindow(text,maincolor,text2,logo)
    logo = logo or 0
    maincolor = maincolor or Color3.fromRGB(63,233,233)
    local isselected = false

    local HovxrzGui = Instance.new("ScreenGui")
    HovxrzGui.Name = "HovxrzGui"
    HovxrzGui.Parent = game:GetService("CoreGui")
    HovxrzGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

    local Main = Instance.new("Frame")
    Main.Name = "Main"
    Main.Parent = HovxrzGui
    Main.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    Main.BorderColor3 = Color3.fromRGB(25, 25, 25)
    Main.Position = UDim2.new(0.5, 0,0.499, 0)
    -- Main.Size = UDim2.new(0, 375, 0, 460)
    Main.AnchorPoint = Vector2.new(0.5,0.5)

    local Top = Instance.new("Frame")
    Top.Name = "Top"
    Top.Parent = Main
    Top.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Top.BorderSizePixel = 0
    -- Top.Size = UDim2.new(0, 375, 0, 20)
    Top.ClipsDescendants = true
    
    local NameHub = Instance.new("TextLabel")
    NameHub.Name = "NameHub"
    NameHub.Parent = Top
    NameHub.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    NameHub.BackgroundTransparency = 1.000
    NameHub.Position = UDim2.new(0, 25, 0, 0)
    NameHub.Size = UDim2.new(0, 50, 0, 20)
    NameHub.Font = Enum.Font.GothamSemibold
    NameHub.Text = string.upper(text)
    NameHub.TextColor3 = Color3.fromRGB(225, 225, 225)
    NameHub.TextSize = 15.000
    
    local Hub = Instance.new("TextLabel")
    Hub.Name = "Hub"
    Hub.Parent = Top
    Hub.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Hub.BackgroundTransparency = 1.000
    Hub.Position = UDim2.new(0, 75, 0, 0)
    Hub.Size = UDim2.new(0, 60, 0, 20)
    Hub.Font = Enum.Font.GothamSemibold
    Hub.Text = "HUB"
    Hub.TextColor3 = maincolor
    Hub.TextSize = 15.000
    Hub.TextXAlignment = Enum.TextXAlignment.Left
    
    local Logo = Instance.new("ImageLabel")
    Logo.Name = "Logo"
    Logo.Parent = Top
    Logo.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Logo.BackgroundTransparency = 1.000
    Logo.BorderSizePixel = 0
    Logo.Position = UDim2.new(0, 5, 0, 0)
    Logo.Size = UDim2.new(0, 20, 0, 20)
    Logo.Image = "rbxassetid://12220187925"..tostring(logo)

    local Barrier = Instance.new("Frame")
    Barrier.Name = "Barrier"
    Barrier.Parent = Top
    Barrier.BackgroundColor3 = Color3.fromRGB(225, 225, 225)
    Barrier.BorderColor3 = Color3.fromRGB(27, 42, 53)
    Barrier.BorderSizePixel = 0
    Barrier.Position = UDim2.new(0, 115, 0, 3)
    Barrier.Size = UDim2.new(0, 2, 0, 14)

    local Description = Instance.new("TextLabel")
    Description.Name = "Description"
    Description.Parent = Top
    Description.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Description.BackgroundTransparency = 1.000
    Description.Position = UDim2.new(0, 125, 0, 0)
    Description.Size = UDim2.new(0, 250, 0, 20)
    Description.Font = Enum.Font.GothamSemibold
    Description.Text = text2
    Description.TextColor3 = Color3.fromRGB(225, 225, 225)
    Description.TextSize = 15.000
    Description.TextXAlignment = Enum.TextXAlignment.Left

    local Tab = Instance.new("Frame")
    Tab.Name = "Tab"
    Tab.Parent = Main
    Tab.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Tab.BorderSizePixel = 0
    Tab.Position = UDim2.new(0, 5, 0, 25)
    Tab.Size = UDim2.new(0, 365, 0, 25)

    local ScrollTab = Instance.new("ScrollingFrame")
    ScrollTab.Name = "ScrollTab"
    ScrollTab.Parent = Tab
    ScrollTab.Active = true
    ScrollTab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ScrollTab.BackgroundTransparency = 1.000
    ScrollTab.BorderSizePixel = 0
    ScrollTab.Size = UDim2.new(0, 365, 0, 25)
    ScrollTab.CanvasSize = UDim2.new(0, 0, 0, 0)
    ScrollTab.ScrollBarThickness = 0

    local TabListLayout = Instance.new("UIListLayout")
    TabListLayout.Name = "TabListLayout"
    TabListLayout.Parent = ScrollTab
    TabListLayout.FillDirection = Enum.FillDirection.Horizontal
    TabListLayout.SortOrder = Enum.SortOrder.LayoutOrder
    TabListLayout.Padding = UDim.new(0, 5)

    local Page = Instance.new("Frame")
    Page.Name = "Page"
    Page.Parent = Main
    Page.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    Page.BorderSizePixel = 0
    Page.Position = UDim2.new(0.0133333337, 0, 0.130434781, 0)
    Page.Size = UDim2.new(0, 365, 0, 395)

    local pagesFolder = Instance.new("Folder")
    pagesFolder.Name = "pagesFolder"
    pagesFolder.Parent = Page

    MakeDraggable(Top,Main)
    
    Main.BackgroundTransparency = 1
    Tab.Visible = false
    Page.Visible = false
    Main.Size = UDim2.new(0,375,0,0)
    Top.Size = UDim2.new(0,0,0,20)
    TweenService:Create(
        Top,
        TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
        {Size = UDim2.new(0, 375, 0, 20)}
    ):Play()
    repeat wait() until Top.Size == UDim2.new(0, 375, 0, 20)
    Main.BackgroundTransparency = 0
    TweenService:Create(
        Main,
        TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
        {Size = UDim2.new(0, 375, 0, 460)}
    ):Play()
    repeat wait() until Main.Size == UDim2.new(0, 375, 0, 460)
    Tab.Visible = true
    Page.Visible = true

    local uihide = false
    local ScreenGui = Instance.new("ScreenGui")
    local ImageButton = Instance.new("ImageButton")

    ScreenGui.Parent = game.CoreGui

    ImageButton.Parent = ScreenGui
    ImageButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
    ImageButton.Position = UDim2.new(0.120833337, 0, 0.0952890813, 0)
    ImageButton.Size = UDim2.new(0, 50, 0, 50)
    ImageButton.BorderSizePixel = 0
    ImageButton.Image = "rbxassetid://12235359506" -- LOGO
    ImageButton.MouseButton1Down:connect(function()
        if uihide == false then
            uihide = true
            Tab.Visible = false
            Page.Visible = false
            TweenService:Create(
                Main,
                TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                {Size = UDim2.new(0,375,0,0)}
            ):Play()
            repeat wait() until Main.Size == UDim2.new(0,375,0,0)
            Main.BackgroundTransparency = 1
            TweenService:Create(
                Top,
                TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                {Size = UDim2.new(0,0,0,20)}
            ):Play()
        else
            uihide = false
            TweenService:Create(
                Top,
                TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                {Size = UDim2.new(0, 375, 0, 20)}
            ):Play()
            repeat wait() until Top.Size == UDim2.new(0, 375, 0, 20)
            Main.BackgroundTransparency = 0
            TweenService:Create(
                Main,
                TweenInfo.new(1,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                {Size = UDim2.new(0, 375, 0, 460)}
            ):Play()
            repeat wait() until Main.Size == UDim2.new(0, 375, 0, 460)
            Tab.Visible = true
            Page.Visible = true
        end
    end)

    local uitab = {}
    function uitab:AddTab(text)
        local TabButton = Instance.new("TextButton")
        TabButton.Name = "TabButton"
        TabButton.Parent = ScrollTab
        TabButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TabButton.BackgroundTransparency = 1.000
        TabButton.Size = UDim2.new(0, 80, 0, 25)
        TabButton.Font = Enum.Font.GothamSemibold
        TabButton.Text = text
        TabButton.TextColor3 = Color3.fromRGB(225, 225, 225)
        TabButton.TextSize = 14.000
        TabButton.TextTransparency = 0.5

        local MainPage = Instance.new("Frame")
        MainPage.Name = "MainPage"
        MainPage.Parent = pagesFolder
        MainPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        MainPage.BackgroundTransparency = 1.000
        MainPage.Size = UDim2.new(0, 365, 0, 395)
        MainPage.Visible = false

        local MainFramePage = Instance.new("ScrollingFrame")
        MainFramePage.Name = "MainFramePage"
        MainFramePage.Parent = MainPage
        MainFramePage.Active = true
        MainFramePage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        MainFramePage.BackgroundTransparency = 1.000
        MainFramePage.BorderSizePixel = 0
        MainFramePage.Size = UDim2.new(0, 365, 0, 395)
        MainFramePage.CanvasSize = UDim2.new(0, 0, 0, 0)
        MainFramePage.ScrollBarThickness = 0

        local PageListLayout = Instance.new("UIListLayout")
        PageListLayout.Name = "PageListLayout"
        PageListLayout.Padding = UDim.new(0, 15)
        PageListLayout.Parent = MainFramePage
        PageListLayout.SortOrder = Enum.SortOrder.LayoutOrder

        local PagePadding = Instance.new("UIPadding")
        PagePadding.Name = "PagePadding"
        PagePadding.Parent = MainFramePage
        PagePadding.PaddingLeft = UDim.new(0,15)
        PagePadding.PaddingTop = UDim.new(0,15)

        TabButton.MouseButton1Click:Connect(function()
            for i,v in next,pagesFolder:GetChildren() do
                if v.Name == "MainPage" then
                    v.Visible = false
                end
                MainPage.Visible = true
            end
            for i,v in next,ScrollTab:GetChildren() do
                if v:IsA("TextButton") then
                    TweenService:Create(
                        v,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                end
                TweenService:Create(
                    TabButton,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextTransparency = 0}
                ):Play()
            end
        end)

        if isselected == false then
            for i,v in next,pagesFolder:GetChildren() do
                if v.Name == "MainPage" then
                    v.Visible = false
                end
                MainPage.Visible = true
            end
            for i,v in next,ScrollTab:GetChildren() do
                if v:IsA("TextButton") then
                    TweenService:Create(
                        v,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {TextTransparency = 0.5}
                    ):Play()
                end
                TweenService:Create(
                    TabButton,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextTransparency = 0}
                ):Play()
            end
            isselected = true
        end

        game:GetService("RunService").Stepped:Connect(function()
            ScrollTab.CanvasSize = UDim2.new(0, TabListLayout.AbsoluteContentSize.X + 10, 0, 0)
            MainFramePage.CanvasSize = UDim2.new(0, 0, 0, PageListLayout.AbsoluteContentSize.Y + 30)
        end)

        local main = {}
        function main:AddButton(text,callback)
            local ButtonFrame = Instance.new("Frame")
            ButtonFrame.Name = "ButtonFrame"
            ButtonFrame.Parent = MainFramePage
            ButtonFrame.BackgroundColor3 = maincolor
            ButtonFrame.BorderSizePixel = 0
            ButtonFrame.Size = UDim2.new(0, 335, 0, 30)
            
            local UICorner = Instance.new("UICorner")
            UICorner.Parent = ButtonFrame
            UICorner.CornerRadius = UDim.new(0,5)
            
            local Button = Instance.new("TextButton")
            Button.Name = "Button"
            Button.Parent = ButtonFrame
            Button.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
            Button.BorderSizePixel = 0
            Button.Position = UDim2.new(0, 1, 0, 1)
            Button.Size = UDim2.new(0, 333, 0, 28)
            Button.AutoButtonColor = false
            Button.Font = Enum.Font.GothamSemibold
            Button.Text = text
            Button.TextColor3 = Color3.fromRGB(225, 225, 225)
            Button.TextSize = 14.000

            local UICorner_2 = Instance.new("UICorner")
            UICorner_2.Parent = Button
            UICorner_2.CornerRadius = UDim.new(0,5)
            
            local Black = Instance.new("Frame")
            Black.Name = "Black"
            Black.Parent = Button
            Black.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
            Black.BackgroundTransparency = 1.000
            Black.Size = UDim2.new(0, 335, 0, 28)

            Button.MouseEnter:Connect(function()
                TweenService:Create(
                    Button,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextColor3 = maincolor}
                ):Play()
                TweenService:Create(
                    Black,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {BackgroundTransparency = 0.7}
                ):Play()
            end)

            Button.MouseLeave:Connect(function()
                TweenService:Create(
                    Button,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {TextColor3 = Color3.fromRGB(225, 225, 225)}
                ):Play()
                TweenService:Create(
                    Black,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {BackgroundTransparency = 1}
                ):Play()
            end)

            Button.MouseButton1Click:Connect(function()
                callback()
                Button.TextSize = 0
				TweenService:Create(
					Button,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{TextSize = 14}
				):Play()
            end)
        end

        function main:AddToggle(text,config,callback)
            config = config or false
            local istoggled = config

            local ToggleFrame = Instance.new("Frame")
            ToggleFrame.Name = "ToggleFrame"
            ToggleFrame.Parent = MainFramePage
            ToggleFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            ToggleFrame.BackgroundTransparency = 1.000
            ToggleFrame.Size = UDim2.new(0, 335, 0, 25)

            local ToggleButton = Instance.new("TextButton")
            ToggleButton.Name = "ToggleButton"
            ToggleButton.Parent = ToggleFrame
            ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            ToggleButton.BackgroundTransparency = 1.000
            ToggleButton.Size = UDim2.new(0, 335, 0, 25)
            ToggleButton.Font = Enum.Font.SourceSans
            ToggleButton.Text = ""
            ToggleButton.TextColor3 = Color3.fromRGB(0, 0, 0)
            ToggleButton.TextSize = 14.000

            local ToggleLabel = Instance.new("TextLabel")
            ToggleLabel.Name = "ToggleLabel"
            ToggleLabel.Parent = ToggleFrame
            ToggleLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            ToggleLabel.BackgroundTransparency = 1.000
            ToggleLabel.Position = UDim2.new(0.0447761193, 0, 0, 0)
            ToggleLabel.Size = UDim2.new(0, 276, 0, 25)
            ToggleLabel.Font = Enum.Font.GothamSemibold
            ToggleLabel.Text = text
            ToggleLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
            ToggleLabel.TextSize = 15.000
            ToggleLabel.TextXAlignment = Enum.TextXAlignment.Left

            local ToggleImage = Instance.new("Frame")
            ToggleImage.Name = "ToggleImage"
            ToggleImage.Parent = ToggleFrame
            ToggleImage.BackgroundColor3 = Color3.fromRGB(225, 225, 225)
            ToggleImage.Position = UDim2.new(0, 290, 0, 1)
            ToggleImage.Size = UDim2.new(0, 46, 0, 21)

            local UICorner = Instance.new("UICorner")
            UICorner.CornerRadius = UDim.new(0, 10)
            UICorner.Parent = ToggleImage

            local Circle = Instance.new("Frame")
            Circle.Name = "Circle"
            Circle.Parent = ToggleImage
            Circle.BackgroundColor3 = Color3.fromRGB(233, 63, 63)
            Circle.Position = UDim2.new(0, 2, 0, 1)
            Circle.Size = UDim2.new(0, 19, 0, 19)

            local UICorner_2 = Instance.new("UICorner")
            UICorner_2.CornerRadius = UDim.new(0, 10)
            UICorner_2.Parent = Circle

            ToggleButton.MouseButton1Click:Connect(function()
                if istoggled == false then
                    istoggled = true
                    TweenService:Create(
                        Circle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {Position = UDim2.new(0, 24, 0, 1)}
                    ):Play()
                    TweenService:Create(
                        Circle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundColor3 = maincolor}
                    ):Play()
                else
                    istoggled = false
                    TweenService:Create(
                        Circle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {Position = UDim2.new(0, 2, 0, 1)}
                    ):Play()
                    TweenService:Create(
                        Circle,
                        TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                        {BackgroundColor3 = Color3.fromRGB(233, 63, 63)}
                    ):Play()
                end
                pcall(callback,istoggled)
            end)

            if config == true then
                if istoggled == false then
                    istoggled = true
                end
                TweenService:Create(
                    Circle,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {Position = UDim2.new(0, 24, 0, 1)}
                ):Play()
                TweenService:Create(
                    Circle,
                    TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
                    {BackgroundColor3 = maincolor}
                ):Play()
                pcall(callback,istoggled)
            end
		end

        function main:AddDropdown(text,option,callback)
			local isdropping = false
			local Dropdown = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local DropTitle = Instance.new("TextLabel")
			local DropScroll = Instance.new("ScrollingFrame")
			local UIListLayout = Instance.new("UIListLayout")
			local UIPadding = Instance.new("UIPadding")
			local DropButton = Instance.new("TextButton")
			local DropImage = Instance.new("ImageLabel")
			
			Dropdown.Name = "Dropdown"
			Dropdown.Parent = MainFramePage
			Dropdown.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
			Dropdown.ClipsDescendants = true
			Dropdown.Size = UDim2.new(0, 335, 0, 30)
			
			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = Dropdown
			
			DropTitle.Name = "DropTitle"
			DropTitle.Parent = Dropdown
			DropTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropTitle.BackgroundTransparency = 1.000
			DropTitle.Size = UDim2.new(0, 335, 0, 30)
			DropTitle.Font = Enum.Font.GothamSemibold
			DropTitle.Text = text.. " : "
			DropTitle.TextColor3 = Color3.fromRGB(225, 225, 225)
			DropTitle.TextSize = 15.000
            DropTitle.TextXAlignment = Enum.TextXAlignment.Left

            local UIPaddingHAHA = Instance.new("UIPadding")
            UIPaddingHAHA.Parent = DropTitle
            UIPaddingHAHA.Name = "UIPaddingHAHA"
            UIPaddingHAHA.PaddingLeft = UDim.new(0,15)
			
			DropScroll.Name = "DropScroll"
			DropScroll.Parent = Dropdown
			DropScroll.Active = true
			DropScroll.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropScroll.BackgroundTransparency = 1.000
			DropScroll.BorderSizePixel = 0
			DropScroll.Position = UDim2.new(0, 0, 0, 31)
			DropScroll.Size = UDim2.new(0, 335, 0, 70)
			DropScroll.CanvasSize = UDim2.new(0, 0, 0, 0)
			DropScroll.ScrollBarThickness = 3
			
			UIListLayout.Parent = DropScroll
			UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			UIListLayout.Padding = UDim.new(0, 5)
			
			UIPadding.Parent = DropScroll
			UIPadding.PaddingLeft = UDim.new(0, 5)
			UIPadding.PaddingTop = UDim.new(0, 5)
			
			DropImage.Name = "DropImage"
			DropImage.Parent = Dropdown
			DropImage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropImage.BackgroundTransparency = 1.000
			DropImage.Position = UDim2.new(0, 305, 0, 5)
			DropImage.Rotation = 180.000
			DropImage.Size = UDim2.new(0, 20, 0, 20)
			DropImage.Image = "rbxassetid://6031090990"
			
			DropButton.Name = "DropButton"
			DropButton.Parent = Dropdown
			DropButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropButton.BackgroundTransparency = 1.000
			DropButton.Size = UDim2.new(0, 335, 0, 30)
			DropButton.Font = Enum.Font.SourceSans
			DropButton.Text = ""
			DropButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			DropButton.TextSize = 14.000

			for i,v in next,option do
				local Item = Instance.new("TextButton")

				Item.Name = "Item"
				Item.Parent = DropScroll
				Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Item.BackgroundTransparency = 1.000
				Item.Size = UDim2.new(0, 335, 0, 26)
				Item.Font = Enum.Font.GothamSemibold
				Item.Text = tostring(v)
				Item.TextColor3 = Color3.fromRGB(225, 225, 225)
				Item.TextSize = 13.000
				Item.TextTransparency = 0.500

				Item.MouseEnter:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0}
					):Play()
				end)

				Item.MouseLeave:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end)

				Item.MouseButton1Click:Connect(function()
					isdropping = false
					Dropdown:TweenSize(UDim2.new(0,335,0,30),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = 180}
					):Play()
					callback(Item.Text)
					DropTitle.Text = text.." : "..Item.Text
				end)
			end

			DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)

			DropButton.MouseButton1Click:Connect(function()
				if isdropping == false then
					isdropping = true
					Dropdown:TweenSize(UDim2.new(0,335,0,100),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = 0}
					):Play()
				else
					isdropping = false
					Dropdown:TweenSize(UDim2.new(0,335,0,30),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = 180}
					):Play()
				end
			end)

			local dropfunc = {}
			function dropfunc:Add(t)
				local Item = Instance.new("TextButton")
				Item.Name = "Item"
				Item.Parent = DropScroll
				Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Item.BackgroundTransparency = 1.000
				Item.Size = UDim2.new(0, 335, 0, 26)
				Item.Font = Enum.Font.GothamSemibold
				Item.Text = tostring(t)
				Item.TextColor3 = Color3.fromRGB(225, 225, 225)
				Item.TextSize = 13.000
				Item.TextTransparency = 0.500

				Item.MouseEnter:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0}
					):Play()
				end)

				Item.MouseLeave:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end)

				Item.MouseButton1Click:Connect(function()
					isdropping = false
					Dropdown:TweenSize(UDim2.new(0,335,0,30),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = 180}
					):Play()
					callback(Item.Text)
					DropTitle.Text = text.." : "..Item.Text
				end)
			end
			function dropfunc:Clear()
				DropTitle.Text = tostring(text).." : "
				isdropping = false
				Dropdown:TweenSize(UDim2.new(0,335,0,30),"Out","Quad",0.3,true)
				TweenService:Create(
					DropImage,
					TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{Rotation = 180}
				):Play()
				for i,v in next, DropScroll:GetChildren() do
					if v:IsA("TextButton") then
						v:Destroy()
					end
				end
			end
			return dropfunc
		end
        function main:AddSlider(text,min,max,set,callback)
			local Slider = Instance.new("Frame")
			local slidercorner = Instance.new("UICorner")
			local sliderr = Instance.new("Frame")
			local sliderrcorner = Instance.new("UICorner")
			local SliderLabel = Instance.new("TextLabel")
			local HAHA = Instance.new("Frame")
			local AHEHE = Instance.new("TextButton")
			local bar = Instance.new("Frame")
			local bar1 = Instance.new("Frame")
			local bar1corner = Instance.new("UICorner")
			local barcorner = Instance.new("UICorner")
			local circlebar = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local slidervalue = Instance.new("Frame")
			local valuecorner = Instance.new("UICorner")
			local TextBox = Instance.new("TextBox")
			local UICorner_2 = Instance.new("UICorner")

			Slider.Name = "Slider"
			Slider.Parent = MainFramePage
			Slider.BackgroundColor3 = maincolor
			Slider.BackgroundTransparency = 0
			Slider.Size = UDim2.new(0, 335, 0, 51)

			slidercorner.CornerRadius = UDim.new(0, 5)
			slidercorner.Name = "slidercorner"
			slidercorner.Parent = Slider

			sliderr.Name = "sliderr"
			sliderr.Parent = Slider
			sliderr.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
			sliderr.Position = UDim2.new(0, 1, 0, 1)
			sliderr.Size = UDim2.new(0, 333, 0, 49)

			sliderrcorner.CornerRadius = UDim.new(0, 5)
			sliderrcorner.Name = "sliderrcorner"
			sliderrcorner.Parent = sliderr

			SliderLabel.Name = "SliderLabel"
			SliderLabel.Parent = sliderr
			SliderLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			SliderLabel.BackgroundTransparency = 1.000
			SliderLabel.Position = UDim2.new(0, 15, 0, 0)
			SliderLabel.Size = UDim2.new(0, 180, 0, 26)
			SliderLabel.Font = Enum.Font.GothamSemibold
			SliderLabel.Text = text
			SliderLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
			SliderLabel.TextSize = 16.000
			SliderLabel.TextTransparency = 0
			SliderLabel.TextXAlignment = Enum.TextXAlignment.Left

			HAHA.Name = "HAHA"
			HAHA.Parent = sliderr
			HAHA.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			HAHA.BackgroundTransparency = 1.000
			HAHA.Size = UDim2.new(0, 333, 0, 29)

			AHEHE.Name = "AHEHE"
			AHEHE.Parent = sliderr
			AHEHE.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			AHEHE.BackgroundTransparency = 1.000
			AHEHE.Position = UDim2.new(0, 10, 0, 35)
			AHEHE.Size = UDim2.new(0, 313, 0, 5)
			AHEHE.Font = Enum.Font.SourceSans
			AHEHE.Text = ""
			AHEHE.TextColor3 = Color3.fromRGB(0, 0, 0)
			AHEHE.TextSize = 14.000

			bar.Name = "bar"
			bar.Parent = AHEHE
			bar.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
			bar.Size = UDim2.new(0, 313, 0, 5)

			bar1.Name = "bar1"
			bar1.Parent = bar
			bar1.BackgroundColor3 = maincolor
			bar1.BackgroundTransparency = 0
			bar1.Size = UDim2.new(set/max, 0, 0, 5)

			bar1corner.CornerRadius = UDim.new(0, 5)
			bar1corner.Name = "bar1corner"
			bar1corner.Parent = bar1

			barcorner.CornerRadius = UDim.new(0, 5)
			barcorner.Name = "barcorner"
			barcorner.Parent = bar

			circlebar.Name = "circlebar"
			circlebar.Parent = bar1
			circlebar.BackgroundColor3 = Color3.fromRGB(225, 225, 225)
			circlebar.Position = UDim2.new(1, -2, 0, -3)
			circlebar.Size = UDim2.new(0, 10, 0, 10)

			UICorner.CornerRadius = UDim.new(0, 100)
			UICorner.Parent = circlebar

			slidervalue.Name = "slidervalue"
			slidervalue.Parent = sliderr
			slidervalue.BackgroundColor3 = maincolor
			slidervalue.BackgroundTransparency = 0
			slidervalue.Position = UDim2.new(0, 265, 0, 5)
			slidervalue.Size = UDim2.new(0, 65, 0, 18)

			valuecorner.CornerRadius = UDim.new(0, 5)
			valuecorner.Name = "valuecorner"
			valuecorner.Parent = slidervalue

			TextBox.Parent = slidervalue
			TextBox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
			TextBox.Position = UDim2.new(0, 1, 0, 1)
			TextBox.Size = UDim2.new(0, 63, 0, 16)
			TextBox.Font = Enum.Font.GothamSemibold
			TextBox.TextColor3 = Color3.fromRGB(225, 225, 225)
			TextBox.TextSize = 9.000
			TextBox.Text = set
			TextBox.TextTransparency = 0

			UICorner_2.CornerRadius = UDim.new(0, 5)
			UICorner_2.Parent = TextBox

			local mouse = game.Players.LocalPlayer:GetMouse()
			local uis = game:GetService("UserInputService")

			if Value == nil then
				Value = set
				pcall(function()
					callback(Value)
				end)
			end
			
			AHEHE.MouseButton1Down:Connect(function()
				Value = math.floor((((tonumber(max) - tonumber(min)) / 315) * bar1.AbsoluteSize.X) + tonumber(min)) or 0
				pcall(function()
					callback(Value)
				end)
				bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 315), 0, 5)
				circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 305), 0, -3)
				moveconnection = mouse.Move:Connect(function()
					TextBox.Text = Value
					Value = math.floor((((tonumber(max) - tonumber(min)) / 315) * bar1.AbsoluteSize.X) + tonumber(min))
					pcall(function()
						callback(Value)
					end)
					bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 315), 0, 5)
					circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 305), 0, -3)
				end)
				releaseconnection = uis.InputEnded:Connect(function(Mouse)
					if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
						Value = math.floor((((tonumber(max) - tonumber(min)) / 315) * bar1.AbsoluteSize.X) + tonumber(min))
						pcall(function()
							callback(Value)
						end)
						bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 315), 0, 5)
						circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 305), 0, -3)
						moveconnection:Disconnect()
						releaseconnection:Disconnect()
					end
				end)
			end)
			releaseconnection = uis.InputEnded:Connect(function(Mouse)
				if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
					Value = math.floor((((tonumber(max) - tonumber(min)) / 315) * bar1.AbsoluteSize.X) + tonumber(min))
					TextBox.Text = Value
				end
			end)

			TextBox.FocusLost:Connect(function()
				if tonumber(TextBox.Text) > max then
					TextBox.Text  = max
				end
				bar1.Size = UDim2.new((TextBox.Text or 0) / max, 0, 0, 5)
				circlebar.Position = UDim2.new(1, -2, 0, -3)
				TextBox.Text = tostring(TextBox.Text and math.floor( (TextBox.Text / max) * (max - min) + min) )
				pcall(callback, TextBox.Text)
			end)
		end

        function main:AddTextbox(text,disappear,callback)
			local Textbox = Instance.new("Frame")
			local TextboxCorner = Instance.new("UICorner")
			local Textboxx = Instance.new("Frame")
			local TextboxxCorner = Instance.new("UICorner")
			local TextboxLabel = Instance.new("TextLabel")
			local txtbtn = Instance.new("TextButton")
			local RealTextbox = Instance.new("TextBox")
			local UICorner = Instance.new("UICorner")

			Textbox.Name = "Textbox"
			Textbox.Parent = MainFramePage
			Textbox.BackgroundColor3 = maincolor
			Textbox.BackgroundTransparency = 0
			Textbox.Size = UDim2.new(0, 335, 0, 31)

			TextboxCorner.CornerRadius = UDim.new(0, 5)
			TextboxCorner.Name = "TextboxCorner"
			TextboxCorner.Parent = Textbox

			Textboxx.Name = "Textboxx"
			Textboxx.Parent = Textbox
			Textboxx.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
			Textboxx.Position = UDim2.new(0, 1, 0, 1)
			Textboxx.Size = UDim2.new(0, 333, 0, 29)

			TextboxxCorner.CornerRadius = UDim.new(0, 5)
			TextboxxCorner.Name = "TextboxxCorner"
			TextboxxCorner.Parent = Textboxx

			TextboxLabel.Name = "TextboxLabel"
			TextboxLabel.Parent = Textbox
			TextboxLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextboxLabel.BackgroundTransparency = 1.000
			TextboxLabel.Position = UDim2.new(0, 15, 0, 0)
			TextboxLabel.Text = text
			TextboxLabel.Size = UDim2.new(0, 145, 0, 31)
			TextboxLabel.Font = Enum.Font.GothamSemibold
			TextboxLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
			TextboxLabel.TextSize = 16.000
			TextboxLabel.TextTransparency = 0
			TextboxLabel.TextXAlignment = Enum.TextXAlignment.Left

			txtbtn.Name = "txtbtn"
			txtbtn.Parent = Textbox
			txtbtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			txtbtn.BackgroundTransparency = 1.000
			txtbtn.Position = UDim2.new(0, 1, 0, 1)
			txtbtn.Size = UDim2.new(0, 333, 0, 29)
			txtbtn.Font = Enum.Font.SourceSans
			txtbtn.Text = ""
			txtbtn.TextColor3 = Color3.fromRGB(0, 0, 0)
			txtbtn.TextSize = 14.000

			RealTextbox.Name = "RealTextbox"
			RealTextbox.Parent = Textbox
            RealTextbox.ClipsDescendants = true
			RealTextbox.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
			RealTextbox.BackgroundTransparency = 0
			RealTextbox.Position = UDim2.new(0, 255, 0, 6)
			RealTextbox.Size = UDim2.new(0, 75, 0, 20)
			RealTextbox.Font = Enum.Font.GothamSemibold
			RealTextbox.Text = ""
			RealTextbox.TextColor3 = Color3.fromRGB(225, 225, 225)
			RealTextbox.TextSize = 11.000
			RealTextbox.TextTransparency = 0

			RealTextbox.FocusLost:Connect(function()
				callback(RealTextbox.Text)
				if disappear then
					RealTextbox.Text = ""
				end
			end)

			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = RealTextbox
		end
		function main:AddLabel(text)
			local Label = Instance.new("TextLabel")
			local PaddingLabel = Instance.new("UIPadding")
			local labell = {}
	
			Label.Name = "Label"
			Label.Parent = MainFramePage
			Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Label.BackgroundTransparency = 1.000
			Label.Size = UDim2.new(0, 335, 0, 20)
			Label.Font = Enum.Font.GothamSemibold
			Label.TextColor3 = Color3.fromRGB(225, 225, 225)
			Label.TextSize = 16.000
			Label.Text = text
			Label.TextXAlignment = Enum.TextXAlignment.Left

			PaddingLabel.PaddingLeft = UDim.new(0,15)
			PaddingLabel.Parent = Label
			PaddingLabel.Name = "PaddingLabel"
	
			function labell:Set(newtext)
				Label.Text = newtext
			end

			return labell
		end
		function main:AddSeperator(text)
			local Seperator = Instance.new("Frame")
			local Sep1 = Instance.new("Frame")
			local Sep2 = Instance.new("TextLabel")
			local Sep3 = Instance.new("Frame")
			
			Seperator.Name = "Seperator"
			Seperator.Parent = MainFramePage
			Seperator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Seperator.BackgroundTransparency = 1.000
			Seperator.Size = UDim2.new(0, 335, 0, 20)
			
			Sep1.Name = "Sep1"
			Sep1.Parent = Seperator
			Sep1.BackgroundColor3 = maincolor
			Sep1.BorderSizePixel = 0
			Sep1.Position = UDim2.new(0, 0, 0, 10)
			Sep1.Size = UDim2.new(0, 80, 0, 1)
			
			Sep2.Name = "Sep2"
			Sep2.Parent = Seperator
			Sep2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Sep2.BackgroundTransparency = 1.000
			Sep2.Position = UDim2.new(0, 120, 0, 0)
			Sep2.Size = UDim2.new(0, 100, 0, 20)
			Sep2.Font = Enum.Font.GothamSemibold
			Sep2.Text = text
			Sep2.TextColor3 = Color3.fromRGB(255, 255, 255)
			Sep2.TextSize = 14.000
			
			Sep3.Name = "Sep3"
			Sep3.Parent = Seperator
			Sep3.BackgroundColor3 = maincolor
			Sep3.BorderSizePixel = 0
			Sep3.Position = UDim2.new(0, 255, 0, 10)
			Sep3.Size = UDim2.new(0, 80, 0, 1)
		end

		function main:AddLine()
			local Linee = Instance.new("Frame")
			local Line = Instance.new("Frame")
			
			Linee.Name = "Linee"
			Linee.Parent = MainFramePage
			Linee.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Linee.BackgroundTransparency = 1.000
			Linee.Position = UDim2.new(0, 0, 0.119999997, 0)
			Linee.Size = UDim2.new(0, 335, 0, 20)
			
			Line.Name = "Line"
			Line.Parent = Linee
			Line.BackgroundColor3 = maincolor
			Line.BorderSizePixel = 0
			Line.Position = UDim2.new(0, 0, 0, 10)
			Line.Size = UDim2.new(0, 335, 0, 1)
		end
        return main
    end
    return uitab
end

-------------------------------------------------------------------
if game.PlaceId == 2753915549 then
        W = true
    elseif game.PlaceId == 4442272183 then
        W2 = true
    elseif game.PlaceId == 7449423635 then
        W3 = true
    end
    
    function CheckQuest() 
        Level = game:GetService("Players").LocalPlayer.Data.Level.Value
        if W then
            if Level == 1 or Level <= 9 then
                Mon = "Bandit [Lv. 5]"
                LQuest = 1
                NQuest = "BanditQuest1"
                NameMon = "Bandit"
                CFrameQuest = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
            elseif Level == 10 or Level <= 14 then
                Mon = "Monkey [Lv. 14]"
                LQuest = 1
                NQuest = "JungleQuest"
                NameMon = "Monkey"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
            elseif Level == 15 or Level <= 29 then
                Mon = "Gorilla [Lv. 20]"
                LQuest = 2
                NQuest = "JungleQuest"
                NameMon = "Gorilla"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
            elseif Level == 30 or Level <= 39 then
                Mon = "Pirate [Lv. 35]"
                LQuest = 1
                NQuest = "BuggyQuest1"
                NameMon = "Pirate"
                CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
            elseif Level == 40 or Level <= 59 then
                Mon = "Brute [Lv. 45]"
                LQuest = 2
                NQuest = "BuggyQuest1"
                NameMon = "Brute"
                CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
            elseif Level == 60 or Level <= 74 then
                Mon = "Desert Bandit [Lv. 60]"
                LQuest = 1
                NQuest = "DesertQuest"
                NameMon = "Desert Bandit"
                CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693)
            elseif Level == 75 or Level <= 89 then
                Mon = "Desert Officer [Lv. 70]"
                LQuest = 2
                NQuest = "DesertQuest"
                NameMon = "Desert Officer"
                CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693)
            elseif Level == 90 or Level <= 99 then
                Mon = "Snow Bandit [Lv. 90]"
                LQuest = 1
                NQuest = "SnowQuest"
                NameMon = "Snow Bandit"
                CFrameQuest = CFrame.new(1389.74451, 88.1519318, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
            elseif Level == 100 or Level <= 119 then
                Mon = "Snowman [Lv. 100]"
                LQuest = 2
                NQuest = "SnowQuest"
                NameMon = "Snowman"
                CFrameQuest = CFrame.new(1389.74451, 88.1519318, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
            elseif Level == 120 or Level <= 149 then
                Mon = "Chief Petty Officer [Lv. 120]"
                LQuest = 1
                NQuest = "MarineQuest2"
                NameMon = "Chief Petty Officer"
                CFrameQuest = CFrame.new(-5039.58643, 27.3500385, 4324.68018, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 150 or Level <= 174 then
                Mon = "Sky Bandit [Lv. 150]"
                LQuest = 1
                NQuest = "SkyQuest"
                NameMon = "Sky Bandit"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
            elseif Level == 175 or Level <= 189 then
                Mon = "Dark Master [Lv. 175]"
                LQuest = 2
                NQuest = "SkyQuest"
                NameMon = "Dark Master"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
            elseif Level == 190 or Level <= 209 then
                Mon = "Prisoner [Lv. 190]"
                LQuest = 1
                NQuest = "PrisonerQuest"
                NameMon = "Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
            elseif Level == 210 or Level <= 249 then
                Mon = "Dangerous Prisoner [Lv. 210]"
                LQuest = 2
                NQuest = "PrisonerQuest"
                NameMon = "Dangerous Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
            elseif Level == 250 or Level <= 274 then
                Mon = "Toga Warrior [Lv. 250]"
                LQuest = 1
                NQuest = "ColosseumQuest"
                NameMon = "Toga Warrior"
                CFrameQuest = CFrame.new(-1580.04663, 6.35000277, -2986.47534, -0.515037298, 0, -0.857167721, 0, 1, 0, 0.857167721, 0, -0.515037298)
            elseif Level == 275 or Level <= 299 then
                Mon = "Gladiator [Lv. 275]"
                LQuest = 2
                NQuest = "ColosseumQuest"
                NameMon = "Gladiator"
                CFrameQuest = CFrame.new(-1580.04663, 6.35000277, -2986.47534, -0.515037298, 0, -0.857167721, 0, 1, 0, 0.857167721, 0, -0.515037298)
            elseif Level == 300 or Level <= 324 then
                Mon = "Military Soldier [Lv. 300]"
                LQuest = 1
                NQuest = "MagmaQuest"
                NameMon = "Military Soldier"
                CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469)
            elseif Level == 325 or Level <= 374 then
                Mon = "Military Spy [Lv. 325]"
                LQuest = 2
                NQuest = "MagmaQuest"
                NameMon = "Military Spy"
                CFrameQuest = CFrame.new(-5313.37012, 10.9500084, 8515.29395, -0.499959469, 0, 0.866048813, 0, 1, 0, -0.866048813, 0, -0.499959469)
            elseif Level == 375 or Level <= 399 then
                Mon = "Fishman Warrior [Lv. 375]"
                LQuest = 1
                NQuest = "FishmanQuest"
                NameMon = "Fishman Warrior"
                CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                end
            elseif Level == 400 or Level <= 449 then
                Mon = "Fishman Commando [Lv. 400]"
                LQuest = 2
                NQuest = "FishmanQuest"
                NameMon = "Fishman Commando"
                CFrameQuest = CFrame.new(61122.65234375, 18.497442245483, 1569.3997802734)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                end
            elseif Level == 450 or Level <= 474 then
                Mon = "God's Guard [Lv. 450]"
                LQuest = 1
                NQuest = "SkyExp1Quest"
                NameMon = "God's Guard"
                CFrameQuest = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
                end
            elseif Level == 475 or Level <= 524 then
                Mon = "Shanda [Lv. 475]"
                LQuest = 2
                NQuest = "SkyExp1Quest"
                NameMon = "Shanda"
                CFrameQuest = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
                end
            elseif Level == 525 or Level <= 549 then
                Mon = "Royal Squad [Lv. 525]"
                LQuest = 1
                NQuest = "SkyExp2Quest"
                NameMon = "Royal Squad"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 550 or Level <= 624 then
                Mon = "Royal Soldier [Lv. 550]"
                LQuest = 2
                NQuest = "SkyExp2Quest"
                NameMon = "Royal Soldier"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 625 or Level <= 649 then
                Mon = "Galley Pirate [Lv. 625]"
                LQuest = 1
                NQuest = "FountainQuest"
                NameMon = "Galley Pirate"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
            elseif Level >= 650 then
                Mon = "Galley Captain [Lv. 650]"
                LQuest = 2
                NQuest = "FountainQuest"
                NameMon = "Galley Captain"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
            end
        elseif W2 then
            if Level == 700 or Level <= 724 then
                Mon = "Raider [Lv. 700]"
                LQuest = 1
                NQuest = "Area1Quest"
                NameMon = "Raider"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
            elseif Level == 725 or Level <= 774 then
                Mon = "Mercenary [Lv. 725]"
                LQuest = 2
                NQuest = "Area1Quest"
                NameMon = "Mercenary"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
            elseif Level == 775 or Level <= 799 then
                Mon = "Swan Pirate [Lv. 775]"
                LQuest = 1
                NQuest = "Area2Quest"
                NameMon = "Swan Pirate"
                CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
            elseif Level == 800 or Level <= 874 then
                Mon = "Factory Staff [Lv. 800]"
                NQuest = "Area2Quest"
                LQuest = 2
                NameMon = "Factory Staff"
                CFrameQuest = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
            elseif Level == 875 or Level <= 899 then
                Mon = "Marine Lieutenant [Lv. 875]"
                LQuest = 1
                NQuest = "MarineQuest3"
                NameMon = "Marine Lieutenant"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
            elseif Level == 900 or Level <= 949 then
                Mon = "Marine Captain [Lv. 900]"
                LQuest = 2
                NQuest = "MarineQuest3"
                NameMon = "Marine Captain"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
            elseif Level == 950 or Level <= 974 then
                Mon = "Zombie [Lv. 950]"
                LQuest = 1
                NQuest = "ZombieQuest"
                NameMon = "Zombie"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
            elseif Level == 975 or Level <= 999 then
                Mon = "Vampire [Lv. 975]"
                LQuest = 2
                NQuest = "ZombieQuest"
                NameMon = "Vampire"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
            elseif Level == 1000 or Level <= 1049 then
                Mon = "Snow Trooper [Lv. 1000]"
                LQuest = 1
                NQuest = "SnowMountainQuest"
                NameMon = "Snow Trooper"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
            elseif Level == 1050 or Level <= 1099 then
                Mon = "Winter Warrior [Lv. 1050]"
                LQuest = 2
                NQuest = "SnowMountainQuest"
                NameMon = "Winter Warrior"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
            elseif Level == 1100 or Level <= 1124 then
                Mon = "Lab Subordinate [Lv. 1100]"
                LQuest = 1
                NQuest = "IceSideQuest"
                NameMon = "Lab Subordinate"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
            elseif Level == 1125 or Level <= 1174 then
                Mon = "Horned Warrior [Lv. 1125]"
                LQuest = 2
                NQuest = "IceSideQuest"
                NameMon = "Horned Warrior"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
            elseif Level == 1175 or Level <= 1199 then
                Mon = "Magma Ninja [Lv. 1175]"
                LQuest = 1
                NQuest = "FireSideQuest"
                NameMon = "Magma Ninja"
                CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
            elseif Level == 1200 or Level <= 1249 then
                Mon = "Lava Pirate [Lv. 1200]"
                LQuest = 2
                NQuest = "FireSideQuest"
                NameMon = "Lava Pirate"
                CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
            elseif Level == 1250 or Level <= 1274 then
                Mon = "Ship Deckhand [Lv. 1250]"
                LQuest = 1
                NQuest = "ShipQuest1"
                NameMon = "Ship Deckhand"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016)         
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                end
            elseif Level == 1275 or Level <= 1299 then
                Mon = "Ship Engineer [Lv. 1275]"
                LQuest = 2
                NQuest = "ShipQuest1"
                NameMon = "Ship Engineer"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016)   
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                end             
            elseif Level == 1300 or Level <= 1324 then
                Mon = "Ship Steward [Lv. 1300]"
                LQuest = 1
                NQuest = "ShipQuest2"
                NameMon = "Ship Steward"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125)         
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                end
            elseif Level == 1325 or Level <= 1349 then
                Mon = "Ship Officer [Lv. 1325]"
                LQuest = 2
                NQuest = "ShipQuest2"
                NameMon = "Ship Officer"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                end
            elseif Level == 1350 or Level <= 1374 then
                Mon = "Arctic Warrior [Lv. 1350]"
                LQuest = 1
                NQuest = "FrostQuest"
                NameMon = "Arctic Warrior"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
                if _G.AutoFarm and (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 10000 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 5000.034996032715, -132.83953857422))
                end
            elseif Level == 1375 or Level <= 1424 then
                Mon = "Snow Lurker [Lv. 1375]"
                LQuest = 2
                NQuest = "FrostQuest"
                NameMon = "Snow Lurker"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
            elseif Level == 1425 or Level <= 1449 then
                Mon = "Sea Soldier [Lv. 1425]"
                LQuest = 1
                NQuest = "ForgottenQuest"
                NameMon = "Sea Soldier"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
            elseif Level >= 1450 then
                Mon = "Water Fighter [Lv. 1450]"
                LQuest = 2
                NQuest = "ForgottenQuest"
                NameMon = "Water Fighter"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
            end
        elseif W3 then
            if Level == 1500 or Level <= 1524 then
                Mon = "Pirate Millionaire [Lv. 1500]"
                LQuest = 1
                NQuest = "PiratePortQuest"
                NameMon = "Pirate Millionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
            elseif Level == 1525 or Level <= 1574 then
                Mon = "Pistol Billionaire [Lv. 1525]"
                LQuest = 2
                NQuest = "PiratePortQuest"
                NameMon = "Pistol Billionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
            elseif Level == 1575 or Level <= 1599 then
                Mon = "Dragon Crew Warrior [Lv. 1575]"
                LQuest = 1
                NQuest = "AmazonQuest"
                NameMon = "Dragon Crew Warrior"
                CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
            elseif Level == 1600 or Level <= 1624 then 
                Mon = "Dragon Crew Archer [Lv. 1600]"
                NQuest = "AmazonQuest"
                LQuest = 2
                NameMon = "Dragon Crew Archer"
                CFrameQuest = CFrame.new(5833.1147460938, 51.60498046875, -1103.0693359375)
            elseif Level == 1625 or Level <= 1649 then
                Mon = "Female Islander [Lv. 1625]"
                NQuest = "AmazonQuest2"
                LQuest = 1
                NameMon = "Female Islander"
                CFrameQuest = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
            elseif Level == 1650 or Level <= 1699 then 
                Mon = "Giant Islander [Lv. 1650]"
                NQuest = "AmazonQuest2"
                LQuest = 2
                NameMon = "Giant Islander"
                CFrameQuest = CFrame.new(5446.8793945313, 601.62945556641, 749.45672607422)
            elseif Level == 1700 or Level <= 1724 then
                Mon = "Marine Commodore [Lv. 1700]"
                LQuest = 1
                NQuest = "MarineTreeIsland"
                NameMon = "Marine Commodore"
                CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
            elseif Level == 1725 or Level <= 1774 then
                Mon = "Marine Rear Admiral [Lv. 1725]"
                NameMon = "Marine Rear Admiral"
                NQuest = "MarineTreeIsland"
                LQuest = 2
                CFrameQuest = CFrame.new(2179.98828125, 28.731239318848, -6740.0551757813)
            elseif Level == 1775 or Level <= 1799 then
                Mon = "Fishman Raider [Lv. 1775]"
                LQuest = 1
                NQuest = "DeepForestIsland3"
                NameMon = "Fishman Raider"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)   
            elseif Level == 1800 or Level <= 1824 then
                Mon = "Fishman Captain [Lv. 1800]"
                LQuest = 2
                NQuest = "DeepForestIsland3"
                NameMon = "Fishman Captain"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)   
            elseif Level == 1825 or Level <= 1849 then
                Mon = "Forest Pirate [Lv. 1825]"
                LQuest = 1
                NQuest = "DeepForestIsland"
                NameMon = "Forest Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
            elseif Level == 1850 or Level <= 1899 then
                Mon = "Mythological Pirate [Lv. 1850]"
                LQuest = 2
                NQuest = "DeepForestIsland"
                NameMon = "Mythological Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)   
            elseif Level == 1900 or Level <= 1924 then
                Mon = "Jungle Pirate [Lv. 1900]"
                LQuest = 1
                NQuest = "DeepForestIsland2"
                NameMon = "Jungle Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
            elseif Level == 1925 or Level <= 1974 then
                Mon = "Musketeer Pirate [Lv. 1925]"
                LQuest = 2
                NQuest = "DeepForestIsland2"
                NameMon = "Musketeer Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
            elseif Level == 1975 or Level <= 1999 then
                Mon = "Reborn Skeleton [Lv. 1975]"
                LQuest = 1
                NQuest = "HauntedQuest1"
                NameMon = "Reborn Skeleton"
                CFrameQuest = CFrame.new(-9479.2168, 141.215088, 5566.09277, 0, 0, 1, 0, 1, -0, -1, 0, 0)
            elseif Level == 2000 or Level <= 2024 then
                Mon = "Living Zombie [Lv. 2000]"
                LQuest = 2
                NQuest = "HauntedQuest1"
                NameMon = "Living Zombie"
                CFrameQuest = CFrame.new(-9479.2168, 141.215088, 5566.09277, 0, 0, 1, 0, 1, -0, -1, 0, 0)
            elseif Level == 2025 or Level <= 2049 then
                Mon = "Demonic Soul [Lv. 2025]"
                LQuest = 1
                NQuest = "HauntedQuest2"
                NameMon = "Demonic Soul"
                CFrameQuest = CFrame.new(-9516.99316, 172.017181, 6078.46533, 0, 0, -1, 0, 1, 0, 1, 0, 0) 
            elseif Level == 2050 or Level <= 2074 then
                Mon = "Posessed Mummy [Lv. 2050]"
                LQuest = 2
                NQuest = "HauntedQuest2"
                NameMon = "Posessed Mummy"
                CFrameQuest = CFrame.new(-9516.99316, 172.017181, 6078.46533, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 2075 or Level <= 2099 then
                Mon = "Peanut Scout [Lv. 2075]"
                LQuest = 1
                NQuest = "NutsIslandQuest"
                NameMon = "Peanut Scout"
                CFrameQuest = CFrame.new(-2104.3908691406, 38.104167938232, -10194.21875, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 2100 or Level <= 2124 then
                Mon = "Peanut President [Lv. 2100]"
                LQuest = 2
                NQuest = "NutsIslandQuest"
                NameMon = "Peanut President"
                CFrameQuest = CFrame.new(-2104.3908691406, 38.104167938232, -10194.21875, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 2125 or Level <= 2149 then
                Mon = "Ice Cream Chef [Lv. 2125]"
                LQuest = 1
                NQuest = "IceCreamIslandQuest"
                NameMon = "Ice Cream Chef"
                CFrameQuest = CFrame.new(-820.64825439453, 65.819526672363, -10965.795898438, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 2150 or Level <= 2199 then
                Mon = "Ice Cream Commander [Lv. 2150]"
                LQuest = 2
                NQuest = "IceCreamIslandQuest"
                NameMon = "Ice Cream Commander"
                CFrameQuest = CFrame.new(-820.64825439453, 65.819526672363, -10965.795898438, 0, 0, -1, 0, 1, 0, 1, 0, 0)
            elseif Level == 2200 or Level <= 2224 then
                Mon = "Cookie Crafter [Lv. 2200]"
                LQuest = 1
                NQuest = "CakeQuest1"
                NameMon = "Cookie Crafter"
                CFrameQuest = CFrame.new(-2021.32007, 37.7982254, -12028.7295, 0.957576931, -8.80302053e-08, 0.288177818, 6.9301187e-08, 1, 7.51931211e-08, -0.288177818, -5.2032135e-08, 0.957576931)
            elseif Level == 2225 or Level <= 2249 then
                Mon = "Cake Guard [Lv. 2225]"
                LQuest = 2
                NQuest = "CakeQuest1"
                NameMon = "Cake Guard"
                CFrameQuest = CFrame.new(-2021.32007, 37.7982254, -12028.7295, 0.957576931, -8.80302053e-08, 0.288177818, 6.9301187e-08, 1, 7.51931211e-08, -0.288177818, -5.2032135e-08, 0.957576931)
            elseif Level == 2250 or Level <= 2274 then
                Mon = "Baking Staff [Lv. 2250]"
                LQuest = 1
                NQuest = "CakeQuest2"
                NameMon = "Baking Staff"
                CFrameQuest = CFrame.new(-1927.91602, 37.7981339, -12842.5391, -0.96804446, 4.22142143e-08, 0.250778586, 4.74911062e-08, 1, 1.49904711e-08, -0.250778586, 2.64211941e-08, -0.96804446)
            elseif Level == 2275 or Level <=2299 then
                Mon = "Head Baker [Lv. 2275]"
                LQuest = 2
                NQuest = "CakeQuest2"
                NameMon = "Head Baker"
                CFrameQuest = CFrame.new(-1927.91602, 37.7981339, -12842.5391, -0.96804446, 4.22142143e-08, 0.250778586, 4.74911062e-08, 1, 1.49904711e-08, -0.250778586, 2.64211941e-08, -0.96804446)
         elseif Level == 2300 or Level <= 2324 then
               Mon = "Cocoa Warrior [Lv. 2300]"
               LQuest = 1
               NQuest = "ChocQuest1"
               NameMon = "Cocoa Warrior"
               CFrameQuest = CFrame.new(231.742981, 25.3354111, -12199.0537, 0.998278677, -5.16006757e-08, 0.0586484075, 4.79685092e-08, 1, 6.33390442e-08, -0.0586484075, -6.04167383e-08, 0.998278677)
              elseif Level == 2325 or Level <= 2349 then
               Mon = "Chocolate Bar Battler [Lv. 2325]"
               LQuest = 2
               NQuest = "ChocQuest1"
               NameMon = "Chocolate Bar Battler"
              CFrameQuest = CFrame.new(231.742981, 25.3354111, -12199.0537, 0.998278677, -5.16006757e-08, 0.0586484075, 4.79685092e-08, 1, 6.33390442e-08, -0.0586484075, -6.04167383e-08, 0.998278677)
              elseif Level == 2350 or Level <= 2374 then
               Mon = "Sweet Thief [Lv. 2350]"
               LQuest = 1
               NQuest = "ChocQuest2"
               NameMon = "Sweet Thief"
              CFrameQuest = CFrame.new(149.867218, 24.8196201, -12775.5283, -0.0371122323, -7.14229245e-08, -0.99931109, -6.93553162e-08, 1, -6.88964548e-08, 0.99931109, 6.6750637e-08, -0.0371122323)
             elseif Level == 2375 or Level <= 2400 then
               Mon = "Candy Rebel [Lv. 2375]"
               LQuest = 2
               NQuest = "ChocQuest2"
               NameMon = "Candy Rebel"
              CFrameQuest = CFrame.new(149.867218, 24.8196201, -12775.5283, -0.0371122323, -7.14229245e-08, -0.99931109, -6.93553162e-08, 1, -6.88964548e-08, 0.99931109, 6.6750637e-08, -0.0371122323)
            elseif Level == 2400 or Level <= 2424 then
               Mon = "Candy Pirate [Lv. 2400]"
               LQuest = 1
               NQuest = "CandyQuest1"
               NameMon = "Candy Pirate"
              CFrameQuest = CFrame.new(-1231.29004, 91.3840179, -14434.6465, -0.333769143, 4.57979716e-08, 0.942654848, -1.57369762e-08, 1, -5.41560752e-08, -0.942654848, -3.29101617e-08, -0.333769143)
             elseif Level >= 2425 then
               Mon = "Snow Demon [Lv. 2425]"
               LQuest = 2
               NQuest = "CandyQuest1"
               NameMon = "Snow Demon"
              CFrameQuest = CFrame.new(-940.256104, 63.1305504, -14555.0703, 0.221367463, -5.74154591e-08, -0.975190461, 8.0360671e-08, 1, -4.06343403e-08, 0.975190461, -6.93718434e-08, 0.221367463)
        end
    end
end

function Hop()
        local PlaceID = game.PlaceId
        local AllIDs = {}
        local foundAnything = ""
        local actualHour = os.date("!*t").hour
        local Deleted = false
        function TPReturner()
            local Site;
            if foundAnything == "" then
                Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
            else
                Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
            end
            local ID = ""
            if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
                foundAnything = Site.nextPageCursor
            end
            local num = 0;
            for i,v in pairs(Site.data) do
                local Possible = true
                ID = tostring(v.id)
                if tonumber(v.maxPlayers) > tonumber(v.playing) then
                    for _,Existing in pairs(AllIDs) do
                        if num ~= 0 then
                            if ID == tostring(Existing) then
                                Possible = false
                            end
                        else
                            if tonumber(actualHour) ~= tonumber(Existing) then
                                local delFile = pcall(function()
                                    AllIDs = {}
                                    table.insert(AllIDs, actualHour)
                                end)
                            end
                        end
                        num = num + 1
                    end
                    if Possible == true then
                        table.insert(AllIDs, ID)
                        wait()
                        pcall(function()
                            wait()
                            game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                        end)
                        wait(4)
                    end
                end
            end
        end
        function Teleport() 
            while wait() do
                pcall(function()
                    TPReturner()
                    if foundAnything ~= "" then
                        TPReturner()
                    end
                end)
            end
        end
        Teleport()
    end                   
    
	function isnil(thing)
		return (thing == nil)
	end
	local function round(n)
		return math.floor(tonumber(n) + 0.5)
	end
	Number = math.random(1, 1000000)
	function UpdateEspPlayer()
		for i,v in pairs(game:GetService'Players':GetChildren()) do
			pcall(function()
				if not isnil(v.Character) then
					if ESPPlayer then
						if not isnil(v.Character.Head) and not v.Character.Head:FindFirstChild('NameEsp'..Number) then
							local bill = Instance.new('BillboardGui',v.Character.Head)
							bill.Name = 'NameEsp'..Number
							bill.ExtentsOffset = Vector3.new(0, 1, 0)
							bill.Size = UDim2.new(1,200,1,30)
							bill.Adornee = v.Character.Head
							bill.AlwaysOnTop = true
							local name = Instance.new('TextLabel',bill)
							name.Font = "GothamBold"
							name.FontSize = "Size14"
							name.TextWrapped = true
							name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M')
							name.Size = UDim2.new(1,0,1,0)
							name.TextYAlignment = 'Top'
							name.BackgroundTransparency = 1
							name.TextStrokeTransparency = 0.5
							if v.Team == game.Players.LocalPlayer.Team then
								name.TextColor3 = Color3.new(0,255,0)
							else
								name.TextColor3 = Color3.new(255,0,0)
							end
						else
							v.Character.Head['NameEsp'..Number].TextLabel.Text = (v.Name ..' | '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M\nHealth : ' .. round(v.Character.Humanoid.Health*100/v.Character.Humanoid.MaxHealth) .. '%')
						end
					else
						if v.Character.Head:FindFirstChild('NameEsp'..Number) then
							v.Character.Head:FindFirstChild('NameEsp'..Number):Destroy()
						end
					end
				end
			end)
		end
	end
    
    function UpdateIslandESP() 
        for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
            pcall(function()
                if IslandESP then 
                    if v.Name ~= "Sea" then
                        if not v:FindFirstChild('NameEsp') then
                            local bill = Instance.new('BillboardGui',v)
                            bill.Name = 'NameEsp'
                            bill.ExtentsOffset = Vector3.new(0, 1, 0)
                            bill.Size = UDim2.new(1,200,1,30)
                            bill.Adornee = v
                            bill.AlwaysOnTop = true
                            local name = Instance.new('TextLabel',bill)
                            name.Font = "GothamBold"
                            name.FontSize = "Size14"
                            name.TextWrapped = true
                            name.Size = UDim2.new(1,0,1,0)
                            name.TextYAlignment = 'Top'
                            name.BackgroundTransparency = 1
                            name.TextStrokeTransparency = 0.5
                            name.TextColor3 = Color3.fromRGB(80, 245, 245)
                        else
                            v['NameEsp'].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                        end
                    end
                else
                    if v:FindFirstChild('NameEsp') then
                        v:FindFirstChild('NameEsp'):Destroy()
                    end
                end
            end)
        end
    end
    
    function UpdateChestEsp() 
        for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            pcall(function()
                if string.find(v.Name,"Chest") then
                    if ChestESP then
                        if string.find(v.Name,"Chest") then
                            if not v:FindFirstChild('NameEsp'..Number) then
                                local bill = Instance.new('BillboardGui',v)
                                bill.Name = 'NameEsp'..Number
                                bill.ExtentsOffset = Vector3.new(0, 1, 0)
                                bill.Size = UDim2.new(1,200,1,30)
                                bill.Adornee = v
                                bill.AlwaysOnTop = true
                                local name = Instance.new('TextLabel',bill)
                                name.Font = "GothamBold"
                                name.FontSize = "Size14"
                                name.TextWrapped = true
                                name.Size = UDim2.new(1,0,1,0)
                                name.TextYAlignment = 'Top'
                                name.BackgroundTransparency = 1
                                name.TextStrokeTransparency = 0.5
                                name.TextColor3 = Color3.fromRGB(0, 255, 250)
                            if v.Name == "Chest1" then
                                name.Text = ("Chest 1" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                            end
                            if v.Name == "Chest2" then
                                name.Text = ("Chest 2" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                            end
                        if v.Name == "Chest3" then
                            name.Text = ("Chest 3" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                        end
                        else
                            v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                        end
                    end
                else
                    if v:FindFirstChild('NameEsp'..Number) then
                    v:FindFirstChild('NameEsp'..Number):Destroy()
                    end
                end
                end
            end)
        end
    end
    
    function UpdateBfEsp() 
        for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            pcall(function()
                if DevilFruitESP then
                    if string.find(v.Name, "Fruit") then   
                        if not v.Handle:FindFirstChild('NameEsp'..Number) then
                            local bill = Instance.new('BillboardGui',v.Handle)
                            bill.Name = 'NameEsp'..Number
                            bill.ExtentsOffset = Vector3.new(0, 1, 0)
                            bill.Size = UDim2.new(1,200,1,30)
                            bill.Adornee = v.Handle
                            bill.AlwaysOnTop = true
                            local name = Instance.new('TextLabel',bill)
                            name.Font = "GothamBold"
                            name.FontSize = "Size14"
                            name.TextWrapped = true
                            name.Size = UDim2.new(1,0,1,0)
                            name.TextYAlignment = 'Top'
                            name.BackgroundTransparency = 1
                            name.TextStrokeTransparency = 0.5
                            name.TextColor3 = Color3.fromRGB(255, 0, 0)
                            name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
                        else
                            v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
                        end
                    end
                else
                    if v.Handle:FindFirstChild('NameEsp'..Number) then
                        v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
                        end
                end
            end)
        end
    end
    
    function UpdateFlowerEsp() 
        for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
            pcall(function()
                if v.Name == "Flower2" or v.Name == "Flower1" then
                    if FlowerESP then 
                        if not v:FindFirstChild('NameEsp'..Number) then
                            local bill = Instance.new('BillboardGui',v)
                            bill.Name = 'NameEsp'..Number
                            bill.ExtentsOffset = Vector3.new(0, 1, 0)
                            bill.Size = UDim2.new(1,200,1,30)
                            bill.Adornee = v
                            bill.AlwaysOnTop = true
                            local name = Instance.new('TextLabel',bill)
                            name.Font = "GothamBold"
                            name.FontSize = "Size14"
                            name.TextWrapped = true
                            name.Size = UDim2.new(1,0,1,0)
                            name.TextYAlignment = 'Top'
                            name.BackgroundTransparency = 1
                            name.TextStrokeTransparency = 0.5
                            name.TextColor3 = Color3.fromRGB(255, 0, 0)
                        if v.Name == "Flower1" then 
                            name.Text = ("Blue Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                            name.TextColor3 = Color3.fromRGB(255, 0, 0)
                        end
                        if v.Name == "Flower2" then
                            name.Text = ("Red Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                            name.TextColor3 = Color3.fromRGB(255, 0, 0)
                        end
                    else
                        v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
                    end
                    else
                        if v:FindFirstChild('NameEsp'..Number) then
                            v:FindFirstChild('NameEsp'..Number):Destroy()
                        end
                    end
                end   
            end)
        end
    end
    
    function InfAb()
        if InfAbility then
            if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("Agility") then
                local inf = Instance.new("ParticleEmitter")
                inf.Acceleration = Vector3.new(0,0,0)
                inf.Archivable = true
                inf.Drag = 20
                inf.EmissionDirection = Enum.NormalId.Top
                inf.Enabled = true
                inf.Lifetime = NumberRange.new(0,0)
                inf.LightInfluence = 0
                inf.LockedToPart = true
                inf.Name = "Agility"
                inf.Rate = 500
                local numberKeypoints2 = {
                    NumberSequenceKeypoint.new(0, 0);
                    NumberSequenceKeypoint.new(1, 4); 
                }
                inf.Size = NumberSequence.new(numberKeypoints2)
                inf.RotSpeed = NumberRange.new(9999, 99999)
                inf.Rotation = NumberRange.new(0, 0)
                inf.Speed = NumberRange.new(30, 30)
                inf.SpreadAngle = Vector2.new(0,0,0,0)
                inf.Texture = ""
                inf.VelocityInheritance = 0
                inf.ZOffset = 2
                inf.Transparency = NumberSequence.new(0)
                inf.Color = ColorSequence.new(Color3.fromRGB(0,0,0),Color3.fromRGB(0,0,0))
                inf.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
            end
        else
            if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("Agility") then
                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("Agility"):Destroy()
            end
        end
    end
    
    local LocalPlayer = game:GetService'Players'.LocalPlayer
    local originalstam = LocalPlayer.Character.Energy.Value
    function infinitestam()
        LocalPlayer.Character.Energy.Changed:connect(function()
            if InfiniteEnergy then
                LocalPlayer.Character.Energy.Value = originalstam
            end 
        end)
    end
    
    spawn(function()
        pcall(function()
            while wait(.1) do
                if InfiniteEnergy then
                    wait(0.1)
                    originalstam = LocalPlayer.Character.Energy.Value
                    infinitestam()
                end
            end
        end)
    end)
    
    function NoDodgeCool()
        if nododgecool then
            for i,v in next, getgc() do
                if game:GetService("Players").LocalPlayer.Character.Dodge then
                    if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.Character.Dodge then
                        for i2,v2 in next, getupvalues(v) do
                            if tostring(v2) == "0.1" then
                            repeat wait(.1)
                                setupvalue(v,i2,0)
                            until not nododgecool
                            end
                        end
                    end
                end
            end
        end
    end
    
    function fly()
        local mouse=game:GetService("Players").LocalPlayer:GetMouse''
        localplayer=game:GetService("Players").LocalPlayer
        game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart")
        local torso = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
        local speedSET=25
        local keys={a=false,d=false,w=false,s=false}
        local e1
        local e2
        local function start()
            local pos = Instance.new("BodyPosition",torso)
            local gyro = Instance.new("BodyGyro",torso)
            pos.Name="EPIXPOS"
            pos.maxForce = Vector3.new(math.huge, math.huge, math.huge)
            pos.position = torso.Position
            gyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
            gyro.CFrame = torso.CFrame
            repeat
                    wait()
                    localplayer.Character.Humanoid.PlatformStand=true
                    local new=gyro.CFrame - gyro.CFrame.p + pos.position
                    if not keys.w and not keys.s and not keys.a and not keys.d then
                    speed=1
                    end
                    if keys.w then
                    new = new + workspace.CurrentCamera.CoordinateFrame.lookVector * speed
                    speed=speed+speedSET
                    end
                    if keys.s then
                    new = new - workspace.CurrentCamera.CoordinateFrame.lookVector * speed
                    speed=speed+speedSET
                    end
                    if keys.d then
                    new = new * CFrame.new(speed,0,0)
                    speed=speed+speedSET
                    end
                    if keys.a then
                    new = new * CFrame.new(-speed,0,0)
                    speed=speed+speedSET
                    end
                    if speed>speedSET then
                    speed=speedSET
                    end
                    pos.position=new.p
                    if keys.w then
                    gyro.CFrame = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(-math.rad(speed*15),0,0)
                    elseif keys.s then
                    gyro.CFrame = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(math.rad(speed*15),0,0)
                    else
                    gyro.CFrame = workspace.CurrentCamera.CoordinateFrame
                    end
            until not Fly
            if gyro then 
                    gyro:Destroy() 
            end
            if pos then 
                    pos:Destroy() 
            end
            flying=false
            localplayer.Character.Humanoid.PlatformStand=false
            speed=0
        end
        e1=mouse.KeyDown:connect(function(key)
            if not torso or not torso.Parent then 
                    flying=false e1:disconnect() e2:disconnect() return 
            end
            if key=="w" then
                keys.w=true
            elseif key=="s" then
                keys.s=true
            elseif key=="a" then
                keys.a=true
            elseif key=="d" then
                keys.d=true
            end
        end)
        e2=mouse.KeyUp:connect(function(key)
            if key=="w" then
                keys.w=false
            elseif key=="s" then
                keys.s=false
            elseif key=="a" then
                keys.a=false
            elseif key=="d" then
                keys.d=false
            end
        end)
        start()
    end
    
    function Click()
        game:GetService'VirtualUser':CaptureController()
        game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
    end
    
    function AutoHaki()
        if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
        end
    end
    
    function UnEquipWeapon(Weapon)
        if game.Players.LocalPlayer.Character:FindFirstChild(Weapon) then
            _G.NotAutoEquip = true
            wait(.5)
            game.Players.LocalPlayer.Character:FindFirstChild(Weapon).Parent = game.Players.LocalPlayer.Backpack
            wait(.1)
            _G.NotAutoEquip = false
        end
    end
    
    function EquipWeapon(ToolSe)
        if not _G.NotAutoEquip then
            if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
                Tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
                wait(.1)
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
            end
        end
    end
    function topos(Pos)
        Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
        if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
        pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/210, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
        tween:Play()
        if Distance <= 250 then
            tween:Cancel()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
        end
        if _G.StopTween == true then
            tween:Cancel()
            _G.Clip = false
        end
    end

function TP(Pos)
        Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
        if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
        pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/210, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
        tween:Play()
        if Distance <= 200 then
            tween:Cancel()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
        end
        if _G.StopTween == true then
            tween:Cancel()
            _G.Clip = false
        end
    end
    
    function GetDistance(target)
        return math.floor((target.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude)
    end
    
    function TP1(Pos)
     Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude

    if Distance < 360 then

        Speed = 1200
    elseif Distance < 1000 then
        Speed = 360
    elseif Distance < 360 then
        Speed = 1200
    elseif Distance >= 1000 then
        Speed = 360
    end
    game:GetService("TweenService"):Create(
        game.Players.LocalPlayer.Character.HumanoidRootPart,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = Pos}
    ):Play()
    end

    function TP(Pos)
        Distance = (Pos.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
        if Distance < 250 then
            Speed = 600
        elseif Distance >= 1000 then
            Speed = 350
        end
        game:GetService("TweenService"):Create(
            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart,
            TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
            {CFrame = Pos}
        ):Play()
        _G.Clip = true
        wait(Distance/Speed)
        _G.Clip = false
    end
    
    spawn(function()
        pcall(function()
            while wait() do
                if _G.AutoAdvanceDungeon or _G.AutoDoughtBoss or _G.Auto_Open_Dough_Dungeon or _G.Auto_DungeonMobAura or _G.AutoFarmBone or _G.AutoFarmBossHallow or _G.AutoFarmSwanGlasses or _G.AutoLongSword or _G.AutoBlackSpikeycoat or _G.AutoElectricClaw or _G.AutoFarmGunMastery or _G.AutoHolyTorch or _G.AutoLawRaid or _G.AutoFarmBoss or _G.AutoTwinHooks or _G.AutoOpenSwanDoor or _G.AutoDragon_Trident or _G.AutoSaber or _G.AutoFarmFruitMastery or _G.AutoFarmGunMastery or _G.TeleportIsland or _G.Auto_EvoRace or _G.AutoFarmAllMsBypassType or _G.AutoObservationv2 or _G.AutoMusketeerHat or _G.AutoEctoplasm or _G.AutoRengoku or _G.Auto_Rainbow_Haki or _G.AutoObservation or _G.AutoDarkDagger or _G.Safe_Mode or _G.MasteryFruit or _G.AutoBudySword or _G.AutoOderSword or _G.AutoBounty or _G.AutoAllBoss or _G.Auto_Bounty or _G.AutoSharkman or _G.Auto_Mastery_Fruit or _G.Auto_Mastery_Gun or _G.Auto_Dungeon or _G.Auto_Cavender or _G.Auto_Pole or _G.Auto_Kill_Ply or _G.Auto_Factory or _G.AutoSecondSea or _G.TeleportPly or _G.AutoBartilo or _G.Auto_DarkBoss or _G.GrabChest or _G.AutoFarmBounty or _G.Holy_Torch or _G.AutoFarm or _G.Clip or FarmBoss or _G.AutoElitehunter or _G.AutoThirdSea or _G.Auto_Bone or _G.AutoFarmCandy or _G.AutoHook1 or _G.AutoHook3 or _G.Auto_Soul_Guitar == true then
                    if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                        local Noclip = Instance.new("BodyVelocity")
                        Noclip.Name = "BodyClip"
                        Noclip.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
                        Noclip.MaxForce = Vector3.new(100000,100000,100000)
                        Noclip.Velocity = Vector3.new(0,0,0)
                    end
                end
            end
        end)
    end)
    
    spawn(function()
        pcall(function()
            game:GetService("RunService").Stepped:Connect(function()
                if _G.AutoAdvanceDungeon or _G.AutoDoughtBoss or _G.Auto_Open_Dough_Dungeon or _G.Auto_DungeonMobAura or _G.AutoFarmChest or _G.AutoFarmBossHallow or _G.AutoFarmSwanGlasses or _G.AutoLongSword or _G.AutoDoughtBoss or _G.AutoElectricClaw or _G.AutoFarmGunMastery or _G.AutoHolyTorch or _G.AutoLawRaid or _G.AutoFarmBoss or _G.AutoTwinHooks or _G.AutoOpenSwanDoor or _G.AutoDragon_Trident or _G.AutoSaber or _G.NOCLIP or _G.AutoFarmFruitMastery or _G.AutoFarmGunMastery or _G.TeleportIsland or _G.Auto_EvoRace or _G.AutoFarmAllMsBypassType or _G.AutoObservationv2 or _G.AutoMusketeerHat or _G.AutoEctoplasm or _G.AutoRengoku or _G.Auto_Rainbow_Haki or _G.AutoObservation or _G.AutoDarkDagger or _G.Safe_Mode or _G.MasteryFruit or _G.AutoBudySword or _G.AutoOderSword or _G.AutoBounty or _G.AutoAllBoss or _G.Auto_Bounty or _G.AutoSharkman or _G.Auto_Mastery_Fruit or _G.Auto_Mastery_Gun or _G.Auto_Dungeon or _G.Auto_Cavender or _G.Auto_Pole or _G.Auto_Kill_Ply or _G.Auto_Factory or _G.AutoSecondSea or _G.TeleportPly or _G.AutoBartilo or _G.Auto_DarkBoss or _G.GrabChest or _G.AutoFarmBounty or _G.Holy_Torch or _G.AutoFarm or _G.Clip or _G.AutoElitehunter or _G.AutoThirdSea or _G.Auto_Bone or _G.AutoFarmCandy or _G.AutoHook1 or _G.AutoHook3 == true then
                    for _, v in pairs(game:GetService("Players").LocalPlayer.Character:GetDescendants()) do
                        if v:IsA("BasePart") then
                            v.CanCollide = false    
                        end
                    end
                end
            end)
        end)
    end)
    
    spawn(function()
        while wait() do
            if _G.AutoDoughtBoss or _G.Auto_Open_Dough_Dungeon or _G.Auto_DungeonMobAura or _G.AutoFarmChest or _G.AutoFarmBossHallow or _G.AutoFarmSwanGlasses or _G.AutoLongSword or _G.AutoBlackSpikeycoat or _G.AutoElectricClaw or _G.AutoFarmGunMastery or _G.AutoHolyTorch or _G.AutoLawRaid or _G.AutoFarmBoss or _G.AutoTwinHooks or _G.AutoOpenSwanDoor or _G.AutoDragon_Trident or _G.AutoSaber or _G.NOCLIP or _G.AutoFarmFruitMastery or _G.AutoFarmGunMastery or _G.TeleportIsland or _G.Auto_EvoRace or _G.AutoFarmAllMsBypassType or _G.AutoObservationv2 or _G.AutoMusketeerHat or _G.AutoEctoplasm or _G.AutoRengoku or _G.Auto_Rainbow_Haki or _G.AutoObservation or _G.AutoDarkDagger or _G.Safe_Mode or _G.MasteryFruit or _G.AutoBudySword or _G.AutoOderSword or _G.AutoAllBoss or _G.Auto_Bounty or _G.AutoSharkman or _G.Auto_Mastery_Fruit or _G.Auto_Mastery_Gun or _G.Auto_Dungeon or _G.Auto_Cavender or _G.Auto_Pole or _G.Auto_Kill_Ply or _G.Auto_Factory or _G.AutoSecondSea or _G.TeleportPly or _G.AutoBartilo or _G.Auto_DarkBoss or _G.AutoFarm or _G.Clip or _G.AutoElitehunter or _G.AutoThirdSea or _G.Auto_Bone or _G.AutoFarmCandy or _G.AutoHook1 or _G.AutoHook3 == true then
                pcall(function()
                    game:GetService("ReplicatedStorage").Remotes.CommE:FireServer("Ken",true)
                end)
            end    
        end
    end)
    
    function StopTween(target)
        if not target then
            _G.StopTween = true
            wait()
            topos(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
            wait()
            if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
            end
            _G.StopTween = false
            _G.Clip = false
        end
    end
    
    spawn(function()
        pcall(function()
            while wait() do
                for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do  
                    if v:IsA("Tool") then
                        if v:FindFirstChild("RemoteFunctionShoot") then 
                            SelectWeaponGun = v.Name
                        end
                    end
                end
            end
        end)
    end)
    
    game:GetService("Players").LocalPlayer.Idled:connect(function()
        game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        wait(1)
        game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
    end)
    
    spawn(function()
	game:GetService("RunService").Stepped:Connect(function()
		if _G.Lol then
			if not KRNL_LOADED and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
				setfflag("HumanoidParallelRemoveNoPhysics", "False")
				setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
				game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
			else
				if not game:GetService("Workspace"):FindFirstChild("LOL") then
					local LOL = Instance.new("Part")
					LOL.Name = "LOL"
					LOL.Parent = game.Workspace
					LOL.Anchored = true
					LOL.Transparency = 0.8
					LOL.Size = Vector3.new(50,0.5,50)
				elseif game:GetService("Workspace"):FindFirstChild("LOL") then
					game.Workspace["LOL"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Y - 3.8,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
				end
			end
			for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
				if v:IsA("BasePart") then
					v.CanCollide = false
				end
			end
		end
	end)
end) 


    
spawn(function()
    while wait() do
        pcall(function()
            if string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 88 then
                KillMob = (tonumber(string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,41)) - 500)
            elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 87 then
                KillMob = (tonumber(string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),40,41)) - 500)
            elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 86 then
                KillMob = (tonumber(string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),41,41)) - 500)
            end
        end)
    end
end)

spawn(function()
    while wait() do
        if _G.AutoDoughtBoss then
            pcall(function()
                if game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                        if v.Name == "Cake Prince [Lv. 2300] [Raid Boss]" then
                            if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                repeat task.wait()
                                    AutoHaki()
                                    EquipWeapon(_G.SelectWeapon)
                                    v.HumanoidRootPart.CanCollide = false
                                    v.Humanoid.WalkSpeed = 0
                                    topos(v.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                    game:GetService("VirtualUser"):CaptureController()
                                    game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                    sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                                until not _G.AutoDoughtBoss or not v.Parent or v.Humanoid.Health <= 0
                            end
                        end
                    end
                else
                    if game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
                        topos(game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
					else
                        if KillMob == 0 then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner",true)
                        end                    
                        if game:GetService("Workspace").Map.CakeLoaf.BigMirror.Other.Transparency == 1 then
                            if game:GetService("Workspace").Enemies:FindFirstChild("Cookie Crafter [Lv. 2200]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Guard [Lv. 2225]") or game:GetService("Workspace").Enemies:FindFirstChild("Baking Staff [Lv. 2250]") or game:GetService("Workspace").Enemies:FindFirstChild("Head Baker [Lv. 2275]") then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]" then
                                        if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                            repeat task.wait()
                                                AutoHaki()
                                                EquipWeapon(_G.SelectWeapon)
                                                v.HumanoidRootPart.CanCollide = false
                                                v.Humanoid.WalkSpeed = 0
                                                v.Head.CanCollide = false 
                                                MagnetDought = true
                                                PosMonDoughtOpenDoor = v.HumanoidRootPart.CFrame
                                                topos(v.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                                game:GetService("VirtualUser"):CaptureController()
                                                game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                            until not _G.AutoDoughtBoss or not v.Parent or v.Humanoid.Health <= 0 or game:GetService("Workspace").Map.CakeLoaf.BigMirror.Other.Transparency == 0 or game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or KillMob == 0
                                        end
                                    end
                                end
                            else
                                MagnetDought = false
                                if game:GetService("ReplicatedStorage"):FindFirstChild("Cookie Crafter [Lv. 2200]") then
                                    topos(game:GetService("ReplicatedStorage"):FindFirstChild("Cookie Crafter [Lv. 2200]").HumanoidRootPart.CFrame * CFrame.new(0,35,0)) 
                                else
                                    if game:GetService("ReplicatedStorage"):FindFirstChild("Cake Guard [Lv. 2225]") then
                                        topos(game:GetService("ReplicatedStorage"):FindFirstChild("Cake Guard [Lv. 2225]").HumanoidRootPart.CFrame * CFrame.new(0,35,0)) 
                                    else
                                        if game:GetService("ReplicatedStorage"):FindFirstChild("Baking Staff [Lv. 2250]") then
                                            topos(game:GetService("ReplicatedStorage"):FindFirstChild("Baking Staff [Lv. 2250]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                        else
                                            if game:GetService("ReplicatedStorage"):FindFirstChild("Head Baker [Lv. 2275]") then
                                                topos(game:GetService("ReplicatedStorage"):FindFirstChild("Head Baker [Lv. 2275]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                            end
                                        end
                                    end
                                end                       
                            end
                        else
                            if game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
                                topos(game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                            else
                                if game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
                                    topos(game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                end
                            end
                        end
                    end
                end
            end)
        end
    end
end)

function StopTween(target)
    if not target then
        _G.StopTween = true
        wait()
        topos(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
        wait()
        if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
        end
        _G.StopTween = false
        _G.Clip = false
    end
end

--------------------------------------------------------------------
local RenUi = library:CreateWindow("chicken  ",Color3.fromRGB(255,0,0),"Blox Fruits")
--------------------------------------------------------------------

local Main = RenUi:AddTab("Main")
local Combat = RenUi:AddTab("Combat")
local Stats = RenUi:AddTab("Stats")
local Teleport = RenUi:AddTab("Teleport")
local Dungeon = RenUi:AddTab("Dungeon")
local Shop = RenUi:AddTab("Shop")
local Misc = RenUi:AddTab("Misc")
local DevilFruit = RenUi:AddTab("Devil Fruit")
--------------------------------------------------------------------
Main:AddSeperator("Settings")

Time = Main:AddLabel("Server Time")

function UpdateTime()
    local GameTime = math.floor(workspace.DistributedGameTime+0.5)
    local Hour = math.floor(GameTime/(60^2))%24
    local Minute = math.floor(GameTime/(60^1))%60
    local Second = math.floor(GameTime/(60^0))%60
    Time:Set("Hr(s) : "..Hour.." Min(s) : "..Minute.." Sec(s) : "..Second)
end

spawn(function()
    while task.wait() do
        pcall(function()
            UpdateTime()
        end)
    end
end)

Main:AddToggle("Auto Set Spawn Points",true,function(value)
    _G.AutoSetSpawn = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoSetSpawn then
                if game:GetService("Players").LocalPlayer.Character.Humanoid.Health > 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                end
            end
        end
    end)
end)

local AutoFarm = Main:AddToggle("Auto Farm Level",_G.AutoFarm,function(value)
    _G.AutoFarm = value
end)

spawn(function()
    while task.wait() do
        pcall(function()
            if _G.AutoFarm then
                CheckQuest()
                if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,NameMon) then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                end
                if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if v.Name == Mon then
                            if v:FindFirstChild("HumanoidRootPart") then
                                repeat task.wait()
                                    MouseTween(v.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                until not _G.AutoFarm or not v.Parent or v.Humanoid.Health <= 0
                            end
                        end
                    end
                    for x,y in pairs(game.ReplicatedStorage:GetChildren()) do
                        if y.Name == Mon then
                            if y:FindFirstChild("HumanoidRootPart") then
                                repeat task.wait()
                                    MouseTween(y.HumanoidRootPart.CFrame * CFrame.new(0,25,0))
                                until not _G.AutoFarm or not y.Parent or y.Humanoid.Health <= 0
                            end
                        end
                    end
                    for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].EnemySpawns:GetChildren()) do
                        if string.find(v.Name,NameMon) then
                            if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude >= 10 then
                                MouseTween(v.CFrame * CFrame.new(0,25,0))
                            end
                        end
                    end
                else
                    MouseTween(CFrameQuest)
                    if (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - CFrameQuest.Position).Magnitude <= 20 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest",NQuest,LQuest)
                    end
                end
            end
        end)
    end
end)


WeaponList = {}

for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
        table.insert(WeaponList ,v.Name)
    end
end

local SelectWeapona = Main:AddDropdown("Select Weapon",WeaponList,function(value)
    _G.SelectWeapon = value
end)

Main:AddButton("Refresh Weapon",function()
    SelectWeapona:Clear()
    for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do  
        SelectWeapona:Add(v.Name)
    end
end)

local AutoFarm = Main:AddToggle("Auto Farm Bone",_G.AutoFarm,function(value)
    _G.AutoFarmBone = value
    StopTween(_G.AutoFarmBone)
end)

spawn(function()
    while wait() do 
        if _G.AutoFarmBone and W3 then
            pcall(function()
				if game:GetService("Workspace").Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") or game:GetService("Workspace").Enemies:FindFirstChild("Living Zombie [Lv. 2000]") or game:GetService("Workspace").Enemies:FindFirstChild("Domenic Soul [Lv. 2025]") or game:GetService("Workspace").Enemies:FindFirstChild("Posessed Mummy [Lv. 2050]") then
					for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]" then
							if v.Humanoid.Health > 0 then
								repeat task.wait()
                                    AutoHaki()
                                    EquipWeapon(_G.SelectWeapon)
									v.HumanoidRootPart.CanCollide = false
                                    v.Head.CanCollide = false 
                                    topos(v.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                    game:GetService("VirtualUser"):CaptureController()
                                    game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
									PosMonBone = v.HumanoidRootPart.CFrame
									StartMagnetBoneMon = true
								until not _G.AutoFarmBone or v.Humanoid.Health <= 0 or not v.Parent
							end
						end
					end
				else
					StartMagnetBoneMon = false
                    topos(CFrame.new(-9515.3720703125, 164.00624084473, 5786.0610351562))                    
				end
			end)
		end
	end
end)

Main:AddToggle("Auto Random Bone ",_G.Auto_Random_Bone,function(value)
    _G.Auto_Random_Bone = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.Auto_Random_Bone then    
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
            end
        end
    end)
end)

Main:AddToggle("Fast Attack",true,function(abc)
	_G.FastAttack = abc
_G.FastAttackNormalSpeed = abc
_G.FastAttack = abc
end)


local Module = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
local CombatFramework = debug.getupvalues(Module)[2]
local CameraShakerR = require(game.ReplicatedStorage.Util.CameraShaker)

spawn(function()
    while true do
        if _G.FastAttack then
            pcall(function()
                CameraShakerR:Stop()
                CombatFramework.activeController.attacking = false
                CombatFramework.activeController.timeToNextAttack = 0
                CombatFramework.activeController.increment = 3
                CombatFramework.activeController.hitboxMagnitude = 100
                CombatFramework.activeController.blocking = false
                CombatFramework.activeController.timeToNextBlock = 0
                CombatFramework.activeController.focusStart = 0
                CombatFramework.activeController.humanoid.AutoRotate = true
            end)
        end
        task.wait()
    end
end)


Main:AddToggle("Bring Mob",true,function(value)
    _G.BringMonster = value
end)

spawn(function()
    while task.wait() do
        pcall(function()
            if _G.BringMonster then
                CheckQuest()
                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                    if _G.AutoFarm and StartMagnet and v.Name == Mon and (Mon == "Factory Staff [Lv. 800]" or Mon == "Monkey [Lv. 14]" or Mon == "Dragon Crew Warrior [Lv. 1575]" or Mon == "Dragon Crew Archer [Lv. 1600]" or Mon == "Head Baker [Lv. 2275]" or Mon == "Baking Staff [Lv. 2250]" or Mon == "Cake Guard [Lv. 2225]") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 220 then
                        v.HumanoidRootPart.CFrame = PosMon
                        v.Humanoid:ChangeState(14)
                        v.HumanoidRootPart.CanCollide = false
                        v.Head.CanCollide = false
                        if v.Humanoid:FindFirstChild("Animator") then
                            v.Humanoid.Animator:Destroy()
                        end
                        sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                    elseif _G.AutoFarm and StartMagnet and v.Name == Mon and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 275 then
                        v.HumanoidRootPart.CFrame = PosMon
                        v.Humanoid:ChangeState(14)
                        v.HumanoidRootPart.CanCollide = false
                        v.Head.CanCollide = false
                        if v.Humanoid:FindFirstChild("Animator") then
                            v.Humanoid.Animator:Destroy()
                        end
                        sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                    end
                    if _G.AutoEctoplasm and StartEctoplasmMagnet then
                        if string.find(v.Name, "Ship") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position - EctoplasmMon.Position).Magnitude <= 250 then
                            v.HumanoidRootPart.CFrame = EctoplasmMon
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoRengoku and StartRengokuMagnet then
                        if (v.Name == "Snow Lurker [Lv. 1375]" or v.Name == "Arctic Warrior [Lv. 1350]") and (v.HumanoidRootPart.Position - RengokuMon.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = RengokuMon
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoMusketeerHat and StartMagnetMusketeerhat then
                        if v.Name == "Forest Pirate [Lv. 1825]" and (v.HumanoidRootPart.Position - MusketeerHatMon.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = MusketeerHatMon
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.Auto_EvoRace and StartEvoMagnet then
                        if v.Name == "Zombie [Lv. 950]" and (v.HumanoidRootPart.Position - PosMonEvo.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = PosMonEvo
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoBartilo and AutoBartiloBring then
                        if v.Name == "Swan Pirate [Lv. 775]" and (v.HumanoidRootPart.Position - PosMonBarto.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = PosMonBarto
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoFarmFruitMastery and StartMasteryFruitMagnet then
                        if v.Name == Mon then
                            if (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                v.Humanoid:ChangeState(14)
                                v.HumanoidRootPart.CanCollide = false
                                v.Head.CanCollide = false
                                v.HumanoidRootPart.CFrame = PosMonMasteryFruit
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                            end
                        end
                    end
                    if _G.AutoFarmGunMastery and StartMasteryGunMagnet then
                        if v.Name == "Monkey [Lv. 14]" then
                            if (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                v.Humanoid:ChangeState(14)
                                v.HumanoidRootPart.CanCollide = false
                                v.Head.CanCollide = false
                                v.HumanoidRootPart.CFrame = PosMonMasteryGun
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                            end
                        elseif v.Name == "Factory Staff [Lv. 800]" then
                            if (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                v.Humanoid:ChangeState(14)
                                v.HumanoidRootPart.CanCollide = false
                                v.Head.CanCollide = false
                                v.HumanoidRootPart.CFrame = PosMonMasteryGun
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                            end
                        elseif v.Name == Mon then
                            if (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                v.Humanoid:ChangeState(14)
                                v.HumanoidRootPart.CanCollide = false
                                v.Head.CanCollide = false
                                v.HumanoidRootPart.CFrame = PosMonMasteryGun
                                if v.Humanoid:FindFirstChild("Animator") then
                                    v.Humanoid.Animator:Destroy()
                                end
                                sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                            end
                        end
                    end
                    if _G.AutoFarmBone and StartMagnetBoneMon then
                        if (v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]") and (v.HumanoidRootPart.Position - PosMonBone.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = PosMonBone
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoDoughtBoss and MagnetDought then
                        if (v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]") and (v.HumanoidRootPart.Position - PosMonDoughtOpenDoor.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = PosMonDoughtOpenDoor
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                    if _G.AutoCandy and StartMagnetCandy then
                        if (v.HumanoidRootPart.Position - PosMonCandy.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            v.Humanoid:ChangeState(14)
                            v.HumanoidRootPart.CanCollide = false
                            v.Head.CanCollide = false
                            v.HumanoidRootPart.CFrame = PosMonCandy
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
                        end
                    end
                end
            end
        end)
    end
end)

      
                
                

Main:AddSeperator("Dought")

local MobKilled = Main:AddLabel("Killed")

spawn(function()
    while wait() do
        pcall(function()
            if string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 88 then
                MobKilled:Set("Defeat : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,41))
            elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 87 then
                MobKilled:Set("Defeat : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,40))
            elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 86 then
                MobKilled:Set("Defeat : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,39))
            else
                MobKilled:Set("Boss Is Spawning")
            end
        end)
    end
end)

Main:AddToggle("Auto Dought Boss",_G.AutoDoughtBoss,function(value)
    _G.AutoDoughtBoss = value
    StopTween(_G.AutoDoughtBoss)
end)



Stats:AddSeperator("Auto Stats")

local Pointstat = Stats:AddLabel("Stat Points")

spawn(function()
    while wait() do
        pcall(function()
            Pointstat:Set("Stat Points : "..tostring(game:GetService("Players")["LocalPlayer"].Data.Points.Value))
        end)
    end
end)

Stats:AddToggle("Auto Melee",_G.Auto_Melee,function(value)
    _G.Auto_Melee = value
end)

Stats:AddToggle("Auto Defense",_G.Auto_Defense,function(value)
    _G.Auto_Defense = value
end)

Stats:AddToggle("Auto Sword",_G.Auto_Sword,function(value)
    _G.Auto_Sword = value
end)

Stats:AddToggle("Auto Gun",_G.Auto_Gun,function(value)
    _G.Auto_Gun = value
end)

Stats:AddToggle("Auto Devil Fruits",_G.Auto_DevilFruit,function(value)
    _G.Auto_DevilFruit = value
end)

_G.PointStats = 1
Stats:AddSlider("Select Point",1,100,1,function(value)
    _G.PointStats = value
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Melee then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Melee",_G.PointStats)
                end
            end
        end)
    end
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Defense then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Defense",_G.PointStats)
                end
            end
        end)
    end
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Sword then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Sword",_G.PointStats)
                end
            end
        end)
    end
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Gun then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Gun",_G.PointStats)
                end
            end
        end)
    end
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_DevilFruit then
                if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Demon Fruit",_G.PointStats)
                end
            end
        end)
    end
end)

Stats:AddSeperator("Status")

local locallv = Stats:AddLabel("Level")

spawn(function()
    while wait() do
        pcall(function()
            locallv:Set("Level :".." "..game:GetService("Players").LocalPlayer.Data.Level.Value)
        end)
    end
end)

local localrace = Stats:AddLabel("Race")

spawn(function()
    while wait() do
        pcall(function()
            localrace:Set("Race :".." "..game:GetService("Players").LocalPlayer.Data.Race.Value)
        end)
    end
end)

local localbeli = Stats:AddLabel("Beli")

spawn(function()
    while wait() do
        pcall(function()
            localbeli:Set("Beli :".." "..game:GetService("Players").LocalPlayer.Data.Beli.Value)
        end)
    end
end)

local localfrag = Stats:AddLabel("Fragment")

spawn(function()
    while wait() do
        pcall(function()
            localfrag:Set("Fragments :".." "..game:GetService("Players").LocalPlayer.Data.Fragments.Value)
        end)
    end
end)

local localexp = Stats:AddLabel("ExP")

spawn(function()
    while wait() do
        pcall(function()
            localexp:Set("ExP Points :".." "..game:GetService("Players").LocalPlayer.Data.Exp.Value)
        end)
    end
end)

local localstat = Stats:AddLabel("Stats Points")

spawn(function()
    while wait() do
        pcall(function()
            localstat:Set("Stats Points :".." "..game:GetService("Players").LocalPlayer.Data.Points.Value)
        end)
    end
end)

local localbountyhornor = Stats:AddLabel("Bounty")

spawn(function()
    while wait() do
        pcall(function()
            localbountyhornor:Set("Bounty / Honor :".." "..game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value)
        end)
    end
end)

local localDevil = Stats:AddLabel("Devil Fruit")

spawn(function()
    while wait() do
        pcall(function()
            if game:GetService("Players").LocalPlayer.Character:FindFirstChild(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value) or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value) then
                localDevil:Set("Devil Fruit :".." "..game:GetService("Players").LocalPlayer.Data.DevilFruit.Value)
            else
                localDevil:Set("Not Have Devil Fruit")
            end
        end)
    end
end)

Stats:AddSeperator("Fake")

Stats:AddToggle("Enabled Fake",_G.EnabledStat,function(value)
    _G.EnabledStat = value
end)

Stats:AddTextbox("Level","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Level.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Exp ","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Exp.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Beli","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Beli.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Fragments","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["Localplayer"].Data.Fragments.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Melee","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Stats.Melee.Level.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Defense","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Stats.Defense.Level.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Sword","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Stats.Sword.Level.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Gun","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Stats.Gun.Level.Value = tonumber(value)
    end
end)
Stats:AddTextbox("Fruit","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].Data.Stats["Demon Fruit"].Level.Value = tonumber(value)
    end
end)

Stats:AddTextbox("Bounty","",true,function(value)
    if _G.EnabledStat then
        game:GetService("Players")["LocalPlayer"].leaderstats["Bounty/Honor"].Value = tonumber(value)
    end
end)

Teleport:AddSeperator("World - Monster")

Teleport:AddButton("Teleport To Old World",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
end)

Teleport:AddButton("Teleport To Second Sea",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
end)

Teleport:AddButton("Teleport To Third Sea",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
end)

Teleport:AddButton("Teleport to Seabeast",function()
    for i,v in pairs(game:GetService("Workspace").SeaBeasts:GetChildren()) do
        if v:FindFirstChild("HumanoidRootPart") then
            topos(v.HumanoidRootPart.CFrame*CFrame.new(0,100,0))
        end
    end
end)
Misc:AddSeperator("State")

Misc:AddDropdown("Select Haki State",{"State 0","State 1","State 2","State 3","State 4","State 5"},function(value)
    _G.SelectStateHaki = value
end)

Misc:AddButton("Change Buso Haki State",function()
    if _G.SelectStateHaki == "State 0" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",0)
    elseif _G.SelectStateHaki == "State 1" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",1)
    elseif _G.SelectStateHaki == "State 2" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",2)
    elseif _G.SelectStateHaki == "State 3" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",3)
    elseif _G.SelectStateHaki == "State 4" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",4)
    elseif _G.SelectStateHaki == "State 5" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",5)
    end
end)

Misc:AddSeperator("Graphic")

local a = game.Lighting
local c = Instance.new("ColorCorrectionEffect", a)
local e = Instance.new("ColorCorrectionEffect", a)
OldAmbient = a.Ambient
OldBrightness = a.Brightness
OldColorShift_Top = a.ColorShift_Top
OldBrightnessc = c.Brightness
OldContrastc = c.Contrast
OldTintColorc = c.TintColor
OldTintColore = e.TintColor
Misc:AddToggle("RTX Mode",_G.RTXMode,function(value)
    _G.RTXMode = value
    if not _G.RTXMode then return end
    while _G.RTXMode do wait()
        a.Ambient = Color3.fromRGB(33, 33, 33)
        a.Brightness = 0.3
        c.Brightness = 0.176
        c.Contrast = 0.39
        c.TintColor = Color3.fromRGB(217, 145, 57)
        game.Lighting.FogEnd = 999
        if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("PointLight") then
            local a2 = Instance.new("PointLight")
            a2.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
            a2.Range = 15
            a2.Color = Color3.fromRGB(217, 145, 57)
        end
        if not _G.RTXMode then
            a.Ambient = OldAmbient
            a.Brightness = OldBrightness
            a.ColorShift_Top = OldColorShift_Top
            c.Contrast = OldContrastc
            c.Brightness = OldBrightnessc
            c.TintColor = OldTintColorc
            e.TintColor = OldTintColore
            game.Lighting.FogEnd = 2500
            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("PointLight"):Destroy()
        end
    end
end)

Misc:AddToggle("White Screen ",_G.WhiteScreen,function(value)

    _G.WhiteScreen = value

if _G.WhiteScreen == true then
    game:GetService("RunService"):Set3dRenderingEnabled(false)
elseif _G.WhiteScreen == false then
    game:GetService("RunService"):Set3dRenderingEnabled(true)
end
end)

Misc:AddToggle("Remove Fog ลบหมอก ",RemoveFog,function(value)
    RemoveFog = value
    if not RemoveFog then return end
    while RemoveFog do wait()
        game.Lighting.FogEnd = 9e9
        if not RemoveFog then
            game.Lighting.FogEnd = 2500
        end
    end
end)

Main:AddButton("Unlock FPS [W1-2]",function()
    setfpscap(120)
end)
Main:AddButton("Kaitan Fps",function()
    setfpscap(10)
end)



Misc:AddSeperator("ESP")

Misc:AddToggle("ESP Player",false,function(value)
    ESPPlayer = value
    while ESPPlayer do wait()
        UpdateEspPlayer()
    end
end)

Misc:AddToggle("ESP Chest",false,function(value)
    ChestESP = value
    while ChestESP do wait()
        UpdateChestEsp() 
    end
end)

Misc:AddToggle("ESP Fruit",false,function(value)
    DevilFruitESP = value
    while DevilFruitESP do wait()
        UpdateBfEsp() 
    end
end)

Misc:AddToggle("ESP Flower",false,function(value)
    FlowerESP = value
    while FlowerESP do wait()
        UpdateFlowerEsp() 
    end
end)

Misc:AddToggle("ESP Island",IslandESP,function(value)
    IslandESP = value
    while IslandESP do wait()
        UpdateIslandESP() 
    end
end)



local YaY = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)
local CameraShakerR = require(game.ReplicatedStorage.Util.CameraShaker)
spawn(function()
    while task.wait() do
        if _G.FastAttack then
            pcall(function()
                for i,CombatFrameworkR in pairs(debug.getupvalues(YaY)) do
                    if i == 2 then
                        CameraShakerR:Stop()
                        CombatFrameworkR.activeController.attacking = false
                        CombatFrameworkR.activeController.timeToNextAttack = 0
                        CombatFrameworkR.activeController.increment = 4
                        CombatFrameworkR.activeController.increment = 2
                        CombatFrameworkR.activeController.hitboxMagnitude = 80
                        CombatFrameworkR.activeController.blocking = false
                        CombatFrameworkR.activeController.timeToNextBlock = 0
                        CombatFrameworkR.activeController.focusStart = 0
                        CombatFrameworkR.activeController.humanoid.AutoRotate = true
                    end
                end
            end)
        else
            for i,CombatFrameworkR in pairs(debug.getupvalues(YaY)) do
                if i == 2 then
                    pcall(function()
                        CameraShakerR:Stop()
                        CombatFrameworkR.activeController.attacking = false
                        CombatFrameworkR.activeController.hitboxMagnitude = 80
                        CombatFrameworkR.activeController.blocking = false
                        CombatFrameworkR.activeController.focusStart = 0
                        CombatFrameworkR.activeController.humanoid.AutoRotate = true
                    end)
                end
            end
        end
    end
end)



            
            local SeraphFrame = debug.getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts:WaitForChild("CombatFramework")))[2]
            local VirtualUser = game:GetService('VirtualUser')
            local RigControllerR = debug.getupvalues(require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework.RigController))[2]
            local Client = game:GetService("Players").LocalPlayer
            local DMG = require(Client.PlayerScripts.CombatFramework.Particle.Damage)
            
            function SeraphFuckWeapon() 
                local p13 = SeraphFrame.activeController
                local wea = p13.blades[1]
                if not wea then return end
                while wea.Parent~=game.Players.LocalPlayer.Character do wea=wea.Parent end
                return wea
            end
            
            function getHits(Size)
                local Hits = {}
                local Enemies = workspace.Enemies:GetChildren()
                local Characters = workspace.Characters:GetChildren()
                for i=1,#Enemies do local v = Enemies[i]
                    local Human = v:FindFirstChildOfClass("Humanoid")
                    if Human and Human.RootPart and Human.Health > 0 and game.Players.LocalPlayer:DistanceFromCharacter(Human.RootPart.Position) < Size+55 then
                        table.insert(Hits,Human.RootPart)
                    end
                end
                for i=1,#Characters do local v = Characters[i]
                    if v ~= game.Players.LocalPlayer.Character then
                        local Human = v:FindFirstChildOfClass("Humanoid")
                        if Human and Human.RootPart and Human.Health > 0 and game.Players.LocalPlayer:DistanceFromCharacter(Human.RootPart.Position) < Size+55 then
                            table.insert(Hits,Human.RootPart)
                        end
                    end
                end
                return Hits
            end
            
            task.spawn(
                function()
                while wait(0) do
                    if  _G.FastAttackNormalSpeed then
                        if SeraphFrame.activeController then
                            if v.Humanoid.Health > 0 then
                              SeraphFrame.activeController.attacking = false
                                SeraphFrame.activeController.timeToNextBlock = 0
                               SeraphFrame.activeController.humanoid.AutoRotate = true
                               SeraphFrame.activeController.increment = 3
                               SeraphFrame.activeController.blocking = false
                               SeraphFrame.activeController.hitboxMagnitude = 150
                                SeraphFrame.activeController.timeToNextAttack = 0
                                SeraphFrame.activeController.focusStart = 0
                                SeraphFrame.activeController.humanoid.AutoRotate = true
                                SeraphFrame.activeController.increment = 1 + 1 / 1
                             end
                        end
                    end
                end
            end)
            
            function Boost()
                spawn(function()
                game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("weaponChange",tostring(SeraphFuckWeapon()))
                end)
            end
            
            function Unboost()
                spawn(function()
                    game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("unequipWeapon",tostring(SeraphFuckWeapon()))
                end)
            end
            
            local cdnormal = 8.0
            local Animation = Instance.new("Animation")
            local CooldownFastAttack = 0
            Attack = function()
                local ac = SeraphFrame.activeController
                if ac and ac.equipped then
                    task.spawn(
                        function()
                        if tick() - cdnormal > 9.0 then
                            ac:attack()
                            cdnormal = tick()
                        else
                             Animation.AnimationId = ac.anims.basic[2]
                            ac.humanoid:LoadAnimation(Animation):Play(100, 99) --ท่าไม่ทำงานแก้เป็น (1,1)
                            game:GetService("ReplicatedStorage").RigControllerEvent:FireServer("hit", getHits(120), 2, "")
                        end
                    end)
                end
            end
            
            b = tick()
            spawn(function()
                while wait(0) do
                    if  _G.FastAttackNormalSpeed then
                        if b - tick() > 0.75 then
                            wait(.2)
                            b = tick()
                        end
                        pcall(function()
                            for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                                if v.Humanoid.Health > 0 then
                                    if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 40 then
                                        Attack()
                                        wait(0)
                                        Boost()
                                    end
                                end
                            end
                        end)
                    end
                end
            end)
            
            k = tick()
            spawn(function()
                while wait(0) do
                    if  _G.FastAttackNormalSpeed then
                        if k - tick() > 0.75 then
                            wait(0)
                            k = tick()
                        end
                        pcall(function()
                            for i, v in pairs(game.Workspace.Enemies:GetChildren()) do
                                if v.Humanoid.Health > 0 then
                                    if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 40 then
                                    wait(0)
                                    Unboost()
                                    end
                                end
                            end
                        end)
                    end
                end
            end)
            
            tjw1 = true
            task.spawn(
                function()
                    local a = game.Players.LocalPlayer
                    local b = require(a.PlayerScripts.CombatFramework.Particle)
                    local c = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
                    if not shared.orl then
                        shared.orl = c.wrapAttackAnimationAsync
                    end
                    if not shared.cpc then
                        shared.cpc = b.play
                    end
                    if tjw1 then
                        pcall(
                            function()
                                c.wrapAttackAnimationAsync = function(d, e, f, g, h)
                                    local i = c.getBladeHits(e, f, g)
                                    if i then
                                        b.play = function()
                                        end
                                        d:Play(15.25, 15.25, 15.25)
                                        h(i)
                                        b.play = shared.cpc
                                        wait(0)
                                        d:Stop()
                                    end
                                end
                            end
                        )
                    end
                end
            )
            
            
            
            local CameRa = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework.CameraShaker)
            CameRa.CameraShakeInstance.CameraShakeState = {FadingIn = 3,FadingOut = 2,Sustained = 0,Inactive =1}
            
            local Client = game.Players.LocalPlayer
            local STOP = require(Client.PlayerScripts.CombatFramework.Particle)
            local STOPRL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
            task.spawn(function()
                pcall(function()
                    if not shared.orl then
                        shared.orl = STOPRL.wrapAttackAnimationAsync
                    end
                        if not shared.cpc then
                            shared.cpc = STOP.play 
                        end
                    spawn(function()
                    require(game.ReplicatedStorage.Util.CameraShaker):Stop()
                  require(game.ReplicatedStorage.Util.CameraShaker):Stop()
                        game:GetService("RunService").Stepped:Connect(function()
                            STOPRL.wrapAttackAnimationAsync = function(a,b,c,d,func)
                                local Hits = STOPRL.getBladeHits(b,c,d)
                                if Hits then
                                    if  _G.FastAttackNormalSpeed then
                                        STOP.play = function() end
                                        a:Play(20.1,15.1,10.1)
                                        func(Hits)
                                        STOP.play = shared.cpc
                                        wait(a.length * 1000000000.5)
                                        a:Stop()
                                    else
                                        func(Hits)
                                        STOP.play = shared.cpc
                                        wait(a.length * 10000000000.5)
                                        a:Stop()
                                    end
                                end
                            end
                        end)
                    end)
                end)
                end)
                
                
Main:AddSeperator("Saber")

Main:AddToggle("Auto Saber",_G.AutoSaber,function(value)
    _G.AutoSaber = value
    StopTween(_G.AutoSaber)
end)

Main:AddToggle("Auto Saber Hop",_G.AutoSaber_Hop,function(value)
    _G.AutoSaber_Hop = value
end)

spawn(function()
    while wait() do
        if _G.AutoSaber then
            pcall(function()
                if game:GetService("Workspace").Map.Jungle.Final:FindFirstChild("Part").Transparency == 0 then
                    TP(CFrame.new(-1421.6824951171875, 48.252071380615234, 21.318946838378906))
                    wait(.5)
                    TP(CFrame.new(-1181.1640625, 22.34051513671875, 188.13186645507812))
                    wait(.5)
                    TP(CFrame.new(-1648.1024169921875, 23.252126693725586, 438.4625549316406))
                    wait(.5)
                    TP(CFrame.new(-1153.3184814453125, 2.464047908782959, -701.0916748046875))
                    wait(.5)
                    TP(CFrame.new(-1325.6697998046875, 34.64987564086914, -463.0443420410156))
                    wait(.7)
                    TP(CFrame.new(-1610.5228271484375, 12.052069664001465, 162.6676025390625))
                    wait(.6)
                    EquipWeapon("Torch")
                    wait(.5)
                    TP(CFrame.new(1115.79688, 4.92147732, 4350.17334, -0.639640629, -4.97708896e-09, 0.768674076, -2.51370613e-09, 1, 4.38315872e-09, -0.768674076, 8.71425709e-10, -0.639640629))
                    wait(6.5)
                    TP(CFrame.new(1113.51929, 5.50669432, 4365.20752, -0.821950078, -4.84191531e-08, -0.569559574, 1.90744176e-09, 1, -8.77642634e-08, 0.569559574, -7.32242427e-08, -0.821950078))
                    wait(.5)
                    EquipWeapon("Cup")
                    wait(.8)
                    TP(CFrame.new(1392.83411, 37.3479347, -1323.19702, -0.0098256059, -1.19435768e-07, -0.99995172, 1.04197984e-08, 1, -1.19543927e-07, 0.99995172, -1.15938867e-08, -0.0098256059))
                    wait(5)
                    TP(CFrame.new(1458.23046875, 88.25215911865234, -1389.040283203125))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan")
                    wait(.6)
                    TP(CFrame.new(-908.8209838867188, 13.752044677734375, 4078.2666015625))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                    wait(.5)
                    TP(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
                    wait(1)
                    if game:GetService("Workspace").Enemies:FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if v.Name == "Mob Leader [Lv. 120] [Boss]" then
                                if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                    repeat task.wait()
                                        AutoHaki()
                                        EquipWeapon(_G.SelectWeapon)
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        topos(v.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                        sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                                    until not _G.AutoSaber or v.Humanoid.Health <= 0
                                end
                            end
                        end
                    end
                    wait(.6)
                    TP(CFrame.new(-908.8209838867188, 13.752044677734375, 4078.2666015625))
                    wait(1.2)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                    wait(1.1)
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress")
                    wait(.5)
                    EquipWeapon("Relic")
                    TP(CFrame.new(-1405.82397, 29.8520069, 5.05986547, 0.759286761, 4.36840342e-09, 0.65075618, 9.78191306e-09, 1, -1.81261139e-08, -0.65075618, 2.01285584e-08, 0.759286761))
                    wait(1)
                else
                    if game:GetService("Workspace").Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if v.Name == "Saber Expert [Lv. 200] [Boss]" then
                                if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                    repeat task.wait()
                                        AutoHaki()
                                        EquipWeapon(_G.SelectWeapon)
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        topos(v.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                        sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                                    until not _G.AutoSaber or not v.Parent or v.Humanoid.Health <= 0
                                end
                            end
                        end
                    else
                        if game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
                            topos(game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]").HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                        else
                            if _G.AutoSaber_Hop then
                                Hop()
                            end
                        end
                    end
                end
            end)
        end
    end
end)

Dungeon:AddLine()

local TimeRaid = Dungeon:AddLabel("Wait For Dungeon")

spawn(function()
    pcall(function()
        while wait() do
            if game:GetService("Players").LocalPlayer.PlayerGui.Main.Timer.Visible == true then
                TimeRaid:Set(game:GetService("Players").LocalPlayer.PlayerGui.Main.Timer.Text)
            else
                TimeRaid:Set("Wait For Dungeon")
            end
        end
    end)
end)

Dungeon:AddToggle("Auto Farm Dungeon ",_G.Auto_Dungeon,function(value)
    _G.Auto_Dungeon = value
    StopTween(_G.Auto_Dungeon)
end)

Dungeon:AddToggle("Kill Aura เปิดตอนเข้าดัน ",_G.Kill,function(value)
    _G.Kill = value
end)

Dungeon:AddToggle("Auto Nextland ",_G.Auto_Next,function(value)
    _G.Auto_Next = value
    StopTween(_G.Auto_Next)
end)
spawn(function()
    pcall(function() 
        while wait() do
            if _G.Auto_Dungeon and _G.Kill then
                if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetDescendants()) do
                        if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                            pcall(function()
                                repeat task.wait()                                    
                                    v.Humanoid.Health = 0
                                    v.HumanoidRootPart.CanCollide = false
                                    sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                until not _G.Auto_Dungeon and _G.kill or not v.Parent or v.Humanoid.Health <= 0
                            end)
                        end
                    end
                end
            end
        end
    end)
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.Auto_Dungeon and _G.Auto_Next then
                if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
                    if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
                        topos(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame*CFrame.new(100,70,100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
                        topos(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame*CFrame.new(100,70,100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
                        topos(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame*CFrame.new(100,70,100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
                        topos(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame*CFrame.new(100,70,100))
                    elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
                        topos(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame*CFrame.new(100,70,100))
                    end
                end
            end
        end
    end)
end)

Dungeon:AddToggle("Auto Awakener ",_G.Auto_Awakener,function(value)
    _G.Auto_Awakener = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.Auto_Awakener then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Awakener","Check")
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Awakener","Awaken")
            end
        end
    end)
end)

Dungeon:AddLine()

Dungeon:AddDropdown("Select Chips",{"Flame","Ice","Quake","Light","Dark","String","Rumble","Magma","Human: Buddha","Sand","Bird: Phoenix","Dough"},function(value)
    _G.SelectChip = value
end)

Dungeon:AddToggle("Auto Select Dungeon",_G.AutoSelectDungeon,function(value)
    _G.AutoSelectDungeon = value
end)

spawn(function()
    while wait() do
        if _G.AutoSelectDungeon then
            pcall(function()
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame-Flame") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame-Flame") then
                    _G.SelectChip = "Flame"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice-Ice") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice-Ice") then
                    _G.SelectChip = "Ice"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake-Quake") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake-Quake") then
                    _G.SelectChip = "Quake"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light-Light") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light-Light") then
                    _G.SelectChip = "Light"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark-Dark") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark-Dark") then
                    _G.SelectChip = "Dark"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("String-String") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String-String") then
                    _G.SelectChip = "String"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble-Rumble") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble-Rumble") then
                    _G.SelectChip = "Rumble"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma-Magma") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma-Magma") then
                    _G.SelectChip = "Magma"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
                    _G.SelectChip = "Human: Buddha"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand-Sand") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand-Sand") then
                    _G.SelectChip = "Sand"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird-Bird: Phoenix") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird-Bird: Phoenix") then
                    _G.SelectChip = "Bird: Phoenix"
                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough-Dough") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough-Dough") then
                    _G.SelectChip = "Dough"
                else
                    _G.SelectChip = "Flame"
                end
            end)
        end
    end
end)

Dungeon:AddToggle("Auto Buy Chip ",_G.AutoBuyChip,function(value)
    _G.AutoBuyChip = value
end)

Dungeon:AddToggle("Auto Start Raid ",_G.Auto_StartRaid,function(value)
    _G.Auto_StartRaid = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
                if not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
                    if _G.Auto_StartRaid then
                        if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
                            if World2 then
                                fireclickdetector(game:GetService("Workspace").Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
                            elseif World3 then
                                fireclickdetector(game:GetService("Workspace").Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
                            end
                        end
                    end
                end
            else
                if _G.AutoBuyChip then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", _G.SelectChip)
                end
            end
        end
    end)
end)

Dungeon:AddLine()

Dungeon:AddButton("Next Island",function()
    pcall(function()
        if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
            TP(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame*CFrame.new(0,70,100))
        elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
            TP(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame*CFrame.new(0,70,100))
        elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
            TP(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame*CFrame.new(0,70,100))
        elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
            TP(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame*CFrame.new(0,70,100))
        elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
            TP(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame*CFrame.new(0,70,100))
        end
    end)
end)

if World2 then
    Dungeon:AddButton("Teleport to Lab",function()
        TP(CFrame.new(-6438.73535, 250.645355, -4501.50684))
        end)
elseif World3 then
    Dungeon:AddButton("Teleport to Lab",function()
        TP(CFrame.new(-5017.40869, 314.844055, -2823.0127, -0.925743818, 4.48217499e-08, -0.378151238, 4.55503146e-09, 1, 1.07377559e-07, 0.378151238, 9.7681621e-08, -0.925743818))
    end)
end

if World2 then
    Dungeon:AddButton("Awakening Room ",function()
        TP(CFrame.new(266.227783, 1.39509034, 1857.00732))
    end)
elseif World3 then
    Dungeon:AddButton("Awakening Room ",function()
        TP(CFrame.new(-11571.440429688, 49.172668457031, -7574.7368164062))
    end)
end


 Settings:AddLabel("คนทำ : Mu_LX+ AkinRetention28 ")
 Settings:AddLabel("YT: Mama hub ")
Settings:AddButton("Copy Discord Invite", function()
    setclipboard("https://discord.gg/VkwW6fRM2R")
    UILib:Notification("Notification", "Copied!", "Okay")
end)




local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)

CombatFrameworkR = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework)

y = debug.getupvalues(CombatFrameworkR)[2]

spawn(function()

    game:GetService("RunService").RenderStepped:Connect(function()

        if _G.FastAttack then

            if typeof(y) == "table" then

                pcall(function()

                    CameraShaker:Stop()

                    y.activeController.timeToNextAttack = (math.huge^math.huge^math.huge)

                    y.activeController.timeToNextAttack = 0

                    y.activeController.hitboxMagnitude = 60

                    y.activeController.active = false

                    y.activeController.timeToNextBlock = 0

                    y.activeController.focusStart = 1655503339.0980349

                    y.activeController.increment = 0

                    y.activeController.blocking = false

                    y.activeController.attacking = false

                    y.activeController.humanoid.AutoRotate = true

                end)

            end

        end

    end)

end)

Teleport:AddSeperator("Island")

if W1 then
    Teleport:AddDropdown("Select Island",{
        "WindMill",
        "Marine",
        "Middle Town",
        "Jungle",
        "Pirate Village",
        "Desert",
        "Snow Island",
        "MarineFord",
        "Colosseum",
        "Sky Island 1",
        "Sky Island 2",
        "Sky Island 3",
        "Prison",
        "Magma Village",
        "Under Water Island",
        "Fountain City",
        "Shank Room",
        "Mob Island"
        },function(value)
        _G.SelectIsland = value
    end)
end

if W2 then
    Teleport:AddDropdown("Select Island",{
        "The Cafe",
        "Frist Spot",
        "Dark Area",
        "Flamingo Mansion",
        "Flamingo Room",
        "Green Zone",
        "Factory",
        "Colossuim",
        "Zombie Island",
        "Two Snow Mountain",
        "Punk Hazard",
        "Cursed Ship",
        "Ice Castle",
        "Forgotten Island",
        "Ussop Island",
        "Mini Sky Island"
        },function(value)
        _G.SelectIsland = value
    end)
end

if W3 then
    Teleport:AddDropdown("Select Island",{
        "Mansion",
        "Port Town",
        "Great Tree",
        "Castle On The Sea",
        "MiniSky", 
        "Hydra Island",
        "Floating Turtle",
        "Haunted Castle",
        "Ice Cream Island",
        "Peanut Island",
        "Cake Island"
        },function(value)
        _G.SelectIsland = value
    end)
end

Teleport:AddToggle("Teleport",false,function(value)
    _G.TeleportIsland = value
    if _G.TeleportIsland == true then
        repeat wait()
            if _G.SelectIsland == "WindMill" then
                topos(CFrame.new(979.79895019531, 16.516613006592, 1429.0466308594))
            elseif _G.SelectIsland == "Marine" then
                topos(CFrame.new(-2566.4296875, 6.8556680679321, 2045.2561035156))
            elseif _G.SelectIsland == "Middle Town" then
                topos(CFrame.new(-690.33081054688, 15.09425163269, 1582.2380371094))
            elseif _G.SelectIsland == "Jungle" then
                topos(CFrame.new(-1612.7957763672, 36.852081298828, 149.12843322754))
            elseif _G.SelectIsland == "Pirate Village" then
                topos(CFrame.new(-1181.3093261719, 4.7514905929565, 3803.5456542969))
            elseif _G.SelectIsland == "Desert" then
                topos(CFrame.new(944.15789794922, 20.919729232788, 4373.3002929688))
            elseif _G.SelectIsland == "Snow Island" then
                topos(CFrame.new(1347.8067626953, 104.66806030273, -1319.7370605469))
            elseif _G.SelectIsland == "MarineFord" then
                topos(CFrame.new(-4914.8212890625, 50.963626861572, 4281.0278320313))
            elseif _G.SelectIsland == "Colosseum" then
                topos( CFrame.new(-1427.6203613281, 7.2881078720093, -2792.7722167969))
            elseif _G.SelectIsland == "Sky Island 1" then
                topos(CFrame.new(-4869.1025390625, 733.46051025391, -2667.0180664063))
            elseif _G.SelectIsland == "Sky Island 2" then  
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
            elseif _G.SelectIsland == "Sky Island 3" then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
            elseif _G.SelectIsland == "Prison" then
                topos( CFrame.new(4875.330078125, 5.6519818305969, 734.85021972656))
            elseif _G.SelectIsland == "Magma Village" then
                topos(CFrame.new(-5247.7163085938, 12.883934020996, 8504.96875))
            elseif _G.SelectIsland == "Under Water Island" then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
            elseif _G.SelectIsland == "Fountain City" then
                topos(CFrame.new(5127.1284179688, 59.501365661621, 4105.4458007813))
            elseif _G.SelectIsland == "Shank Room" then
                topos(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
            elseif _G.SelectIsland == "Mob Island" then
                topos(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
            elseif _G.SelectIsland == "The Cafe" then
                topos(CFrame.new(-380.47927856445, 77.220390319824, 255.82550048828))
            elseif _G.SelectIsland == "Frist Spot" then
                topos(CFrame.new(-11.311455726624, 29.276733398438, 2771.5224609375))
            elseif _G.SelectIsland == "Dark Area" then
                topos(CFrame.new(3780.0302734375, 22.652164459229, -3498.5859375))
            elseif _G.SelectIsland == "Flamingo Mansion" then
                topos(CFrame.new(-483.73370361328, 332.0383605957, 595.32708740234))
            elseif _G.SelectIsland == "Flamingo Room" then
                topos(CFrame.new(2284.4140625, 15.152037620544, 875.72534179688))
            elseif _G.SelectIsland == "Green Zone" then
                topos( CFrame.new(-2448.5300292969, 73.016105651855, -3210.6306152344))
            elseif _G.SelectIsland == "Factory" then
                topos(CFrame.new(424.12698364258, 211.16171264648, -427.54049682617))
            elseif _G.SelectIsland == "Colossuim" then
                topos( CFrame.new(-1503.6224365234, 219.7956237793, 1369.3101806641))
            elseif _G.SelectIsland == "Zombie Island" then
                topos(CFrame.new(-5622.033203125, 492.19604492188, -781.78552246094))
            elseif _G.SelectIsland == "Two Snow Mountain" then
                topos(CFrame.new(753.14288330078, 408.23559570313, -5274.6147460938))
            elseif _G.SelectIsland == "Punk Hazard" then
                topos(CFrame.new(-6127.654296875, 15.951762199402, -5040.2861328125))
            elseif _G.SelectIsland == "Cursed Ship" then
                topos(CFrame.new(923.40197753906, 125.05712890625, 32885.875))
            elseif _G.SelectIsland == "Ice Castle" then
                topos(CFrame.new(6148.4116210938, 294.38687133789, -6741.1166992188))
            elseif _G.SelectIsland == "Forgotten Island" then
                topos(CFrame.new(-3032.7641601563, 317.89672851563, -10075.373046875))
            elseif _G.SelectIsland == "Ussop Island" then
                topos(CFrame.new(4816.8618164063, 8.4599885940552, 2863.8195800781))
            elseif _G.SelectIsland == "Mini Sky Island" then
                topos(CFrame.new(-288.74060058594, 49326.31640625, -35248.59375))
            elseif _G.SelectIsland == "Great Tree" then
                topos(CFrame.new(2681.2736816406, 1682.8092041016, -7190.9853515625))
            elseif _G.SelectIsland == "Castle On The Sea" then
                topos(CFrame.new(-5074.45556640625, 314.5155334472656, -2991.054443359375))
            elseif _G.SelectIsland == "MiniSky" then
                topos(CFrame.new(-260.65557861328, 49325.8046875, -35253.5703125))
            elseif _G.SelectIsland == "Port Town" then
                topos(CFrame.new(-290.7376708984375, 6.729952812194824, 5343.5537109375))
            elseif _G.SelectIsland == "Hydra Island" then
                topos(CFrame.new(5228.8842773438, 604.23400878906, 345.0400390625))
            elseif _G.SelectIsland == "Floating Turtle" then
                topos(CFrame.new(-13274.528320313, 531.82073974609, -7579.22265625))
            elseif _G.SelectIsland == "Mansion" then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12471.169921875, 374.94024658203, -7551.677734375))
            elseif _G.SelectIsland == "Haunted Castle" then
                topos(CFrame.new(-9515.3720703125, 164.00624084473, 5786.0610351562))
            elseif _G.SelectIsland == "Ice Cream Island" then
                topos(CFrame.new(-902.56817626953, 79.93204498291, -10988.84765625))
            elseif _G.SelectIsland == "Peanut Island" then
                topos(CFrame.new(-2062.7475585938, 50.473892211914, -10232.568359375))
            elseif _G.SelectIsland == "Cake Island" then
                topos(CFrame.new(-1884.7747802734375, 19.327526092529297, -11666.8974609375))
            end
        until not _G.TeleportIsland
    end
    StopTween(_G.TeleportIsland)
end)


        Main:AddSeperator("Soul Guitar")
        local FM = Main:AddLabel("")
        task.spawn(function()
            while task.wait() do
                pcall(function()
                    if game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149431" then
                        FM:Set("🌑 : Full Moon 100%")
                    elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149052" then
                        FM:Set("🌒 : Full Moon 75%")
                    elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709143733" then
                        FM:Set("🌓 : Full Moon 50%")
                    elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709150401" then
                        FM:Set("🌗 : Full Moon 25%")
                    elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149680" then
                        FM:Set("🌖 : Full Moon 15%")
                    else
                        FM:Set("🌚 : Full Moon 0%")
                    end
                end)
            end
        end)
        
        

Main:AddToggle("Auto Soul Guitar ",_G.Auto_Soul_Guitar,function(value)
    _G.Auto_Soul_Guitar = value
    StopTween(_G.Auto_Soul_Guitar)
end)

task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Settings.Main["Auto Quest Soul Guitar"] then
					if GetWeaponInventory("Soul Guitar") == false then
						if (CFrame.new(-9681.458984375, 6.139880657196045, 6341.3720703125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 5000 then
							if game:GetService("Workspace").NPCs:FindFirstChild("Skeleton Machine") then
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("soulGuitarBuy",true)
							else
								if game:GetService("Workspace").Map["Haunted Castle"].Candle1.Transparency == 0 then
									if game:GetService("Workspace").Map["Haunted Castle"].Placard1.Left.Part.Transparency == 0 then
										Quest2 = true
										repeat wait() toTarget(CFrame.new(-8762.69140625, 176.84783935546875, 6171.3076171875)) until (CFrame.new(-8762.69140625, 176.84783935546875, 6171.3076171875).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.Settings.Main["Auto Quest Soul Guitar"]
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard7.Left.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard6.Left.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard5.Left.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard4.Right.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard3.Left.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard2.Right.ClickDetector)
										wait(1)
										fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"].Placard1.Right.ClickDetector)
										wait(1)
									elseif game:GetService("Workspace").Map["Haunted Castle"].Tablet.Segment1:FindFirstChild("ClickDetector") then
										if game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part1:FindFirstChild("ClickDetector") then
											Quest4 = true
											repeat wait() toTarget(CFrame.new(-9553.5986328125, 65.62338256835938, 6041.58837890625)) until (CFrame.new(-9553.5986328125, 65.62338256835938, 6041.58837890625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.Settings.Main["Auto Quest Soul Guitar"]
											wait(1)
											toTarget(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part3.CFrame)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part3.ClickDetector)
											wait(1)
											toTarget(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part4.CFrame)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part4.ClickDetector)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part4.ClickDetector)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part4.ClickDetector)
											wait(1)
											toTarget(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part6.CFrame)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part6.ClickDetector)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part6.ClickDetector)
											wait(1)
											toTarget(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part8.CFrame)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part8.ClickDetector)
											wait(1)
											toTarget(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part10.CFrame)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part10.ClickDetector)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part10.ClickDetector)
											wait(1)
											fireclickdetector(game:GetService("Workspace").Map["Haunted Castle"]["Lab Puzzle"].ColorFloor.Model.Part10.ClickDetector)
										else
											Quest3 = true
											--Not Work Yet
										end
									else
										if game:GetService("Workspace").NPCs:FindFirstChild("Ghost") then
											local args = {
												[1] = "GuitarPuzzleProgress",
												[2] = "Ghost"
											}

											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										end
										if game.Workspace.Enemies:FindFirstChild("Living Zombie [Lv. 2000]") then
											for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
												if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
													if v.Name == "Living Zombie [Lv. 2000]" then
														EquipWeapon(_G.Settings.Configs["Select Weapon"])
														v.HumanoidRootPart.Size = Vector3.new(60,60,60)
														v.HumanoidRootPart.Transparency = 1
														v.Humanoid.JumpPower = 0
														v.Humanoid.WalkSpeed = 0
														v.HumanoidRootPart.CanCollide = false
														v.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,20,0)
														toTarget(CFrame.new(-10160.787109375, 138.6616973876953, 5955.03076171875))
														game:GetService'VirtualUser':CaptureController()
														game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
													end
												end
											end
										else
											toTarget(CFrame.new(-10160.787109375, 138.6616973876953, 5955.03076171875))
										end
									end
								else    
									if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2), "Error") then
										print("Go to Grave")
										toTarget(CFrame.new(-8653.2060546875, 140.98487854003906, 6160.033203125))
									elseif string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2), "Nothing") then
										print("Wait Next Night")
									else
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2,true)
									end
								end
							end
						else
							toTarget(CFrame.new(-9681.458984375, 6.139880657196045, 6341.3720703125))
						end
					end
				end
			end)
		end
	end)
	
Main:AddToggle("Auto Elite Hunter Hop ",_G.AutoEliteHunterHop,function(value)
    _G.AutoEliteHunterHop = value
end)

Main:AddToggle("Auto Yama ออโต้ดึงดาบ ",_G.Auto_Yama,function(value)
    _G.Auto_Yama = value
    StopTween(_G.Auto_Yama)
end)

spawn(function()
        while wait() do
            if _G.AutoYama then
                if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter","Progress") >= 30 then
                    repeat wait(.1)
                        fireclickdetector(game:GetService("Workspace").Map.Waterfall.SealedKatana.Handle.ClickDetector)
                    until game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Yama") or not _G.AutoYama
                end
            end
        end
    end)


Shop:AddSeperator("Abilities")

Shop:AddButton("Buy Geppo [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Geppo")
end)

Shop:AddButton("Buy Buso Haki [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Buso")
end)

Shop:AddButton("Buy Soru ✅",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Soru")
end)

Shop:AddButton("Buy Observation(Ken) Haki ✅",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Buy")
end)

Shop:AddSeperator("Fighting Style")

Shop:AddButton("Buy Black Leg [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
end)

Shop:AddButton("Buy Electro [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
end)

Shop:AddButton("Buy Fishman Karate [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
end)

Shop:AddButton("Buy Dragon Claw [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
end)

Shop:AddButton("Buy Superhuman [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
end)

Shop:AddButton("Buy Death Step [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
end)

Shop:AddButton("Buy Sharkman Karate [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true)
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
end)

Shop:AddButton("Buy Electric Claw [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
end)

Shop:AddButton("Buy Dragon Talon [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
end)
Shop:AddButton("Buy God Human [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman")
end)

-----Shop----------------
Shop:AddSeperator("Accessory")

Shop:AddButton("Tomoe Ring [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Tomoe Ring")
end)

Shop:AddButton("Black Cape [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Black Cape")
end)

Shop:AddButton("Swordsman Hat [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Swordsman Hat")
end)

Shop:AddSeperator("Sword")

Shop:AddButton("Cutlass [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
end)

Shop:AddButton("Katana [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
end)

Shop:AddButton("Iron Mace [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
end)

Shop:AddButton("Duel Katana [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
end)

Shop:AddButton("Triple Katana [✅]", function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
end)

Shop:AddButton("Pipe [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
end)

Shop:AddButton("Dual Headed Blade [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
end)

Shop:AddButton("Bisento [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
end)

Shop:AddButton("Soul Cane [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
end)

Shop:AddSeperator("Gun")

Shop:AddButton("Slingshot [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
end)

Shop:AddButton("Musket [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
end)

Shop:AddButton("Flintlock [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
end)

Shop:AddButton("Refined Flintlock [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
end)

Shop:AddButton("Cannon [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
end)

Shop:AddButton("Kabucha [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
end)
------------Bone------------------

Shop:AddSeperator("Bones")

Shop:AddButton("Buy Surprise [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
end)

Shop:AddButton("Stat Refund [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,2)
end)
    
Shop:AddButton("Race Reroll [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,3)
end)

Shop:AddSeperator("Fragments 🟣")

Shop:AddButton("Stat Refund [✅]",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
end)

        Combat:AddSeperator("New Aimbot")

Combat:AddToggle("Aimbot Skill Nearest Players ", false, function(vu)

	_G.Aimbot_Skill_Near = vu

end)

spawn(function()
	while wait(.1) do
		pcall(function()
			local MaxDistance = math.huge
			for i,v in pairs(game:GetService("Players"):GetPlayers()) do
				if v.Name ~= game.Players.LocalPlayer.Name then
					local Distance = v:DistanceFromCharacter(game.Players.LocalPlayer.Character.HumanoidRootPart.Position)
					if Distance < MaxDistance then
						MaxDistance = Distance
						TargetPlayerAim = v.Name
					end
				end
			end
		end)
	end
end)

spawn(function()
	pcall(function()
		game:GetService("RunService").RenderStepped:connect(function()
			if _G.Aimbot_Skill_Near and TargetPlayerAim ~= nil and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") and game.Players.LocalPlayer.Character[game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Name]:FindFirstChild("MousePos") then
				local args = {
					[1] = game:GetService("Players"):FindFirstChild(TargetPlayerAim).Character.HumanoidRootPart.Position
				}
				game:GetService("Players").LocalPlayer.Character[game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))
			end
		end)
	end)
end)

Combat:AddSeperator("PvP")

Combat:AddToggle("Enabled PvP ",false,function(value)
    _G.EnabledPvP = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.EnabledPvP then
                if game:GetService("Players").LocalPlayer.PlayerGui.Main.PvpDisabled.Visible == true then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EnablePvp")
                end
            end
        end
    end)
end)

Combat:AddToggle("Safe Mode ",false,function(value)
    _G.Safe_Mode = value
    StopTween(_G.Safe_Mode)
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.Safe_Mode then
                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame
            end
        end
    end)
end)

Combat:AddButton("Respawn",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","") 
    wait()
end)


Combat:AddSeperator("Bounty")

local Current = Combat:AddLabel("Current Bounties :")

local Bounty = tostring(game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value)
local sub = string.sub 
local len = string.len
spawn(function()
    while wait() do
        pcall(function()
            if len(Bounty) == 4 then
                Bounty1 = sub(Bounty,1,1).."."..sub(Bounty,2,3).."K"
            elseif len(Bounty) == 5 then
                Bounty1 = sub(Bounty,1,2).."."..sub(Bounty,3,4).."K"
            elseif len(Bounty) == 6 then
                Bounty1 = sub(Bounty,1,3).."."..sub(Bounty,4,5).."K"
            elseif len(Bounty) == 7 then
                Bounty1 = sub(Bounty,1,1).."."..sub(Bounty,2,3).."M"
            elseif len(Bounty) == 8 then
                Bounty1 = sub(Bounty,1,2).."."..sub(Bounty,3,4).."M"
            elseif len(Bounty) <= 3 then
                Bounty1 = Bounty
            end
            if tonumber(Bounty) == 25000000 then
                Current:Set("Current Bounties : "..Bounty1.." [ Max ]")
            elseif tonumber(Bounty) < 25000000 then
                Current:Set("Current Bounties : "..Bounty1)
            end
        end)
    end
end)

local Earn = Combat:AddLabel("Earned")
local OldBounty = game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value
local Bounty = tostring(game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value)
local Earned = tostring(game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value - OldBounty)
local sub = string.sub 
local len = string.len
spawn(function()
    while wait() do
        pcall(function()
            if len(Earned) == 4 then
                Earned1 = sub(Earned,1,1).."."..sub(Earned,2,3).."K"
            elseif len(Earned) == 5 then
                Earned1 = sub(Earned,1,2).."."..sub(Earned,3,4).."K"
            elseif len(Earned) == 6 then
                Earned1 = sub(Earned,1,3).."."..sub(Earned,4,5).."K"
            elseif len(Earned) == 7 then
                Earned1 = sub(Earned,1,1).."."..sub(Earned,2,3).."M"
            elseif len(Earned) == 8 then
                Earned1 = sub(Earned,1,2).."."..sub(Earned,3,4).."M"
            elseif len(Earned) <= 3 then
                Earned1 = Earned
            end
            Earn:Set("Earned : "..tonumber(Earned1))
        end)
    end
end)

Combat:AddToggle("Auto Farm Bounty",_G.AutoFarmBounty,function(value)
    _G.AutoFarmBounty = value
    StopTween(_G.AutoFarmBounty)
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.AutoFarmBounty then
                for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetChildren()) do
                    if v:IsA("Shirt") then
                        v:Destroy()
                    end
                    if v:IsA("Pants") then
                        v:Destroy()
                    end
                    if v:IsA("Accessory") then
                        v:Destroy()
                    end
                end
            end
        end)
    end
end)

spawn(function()
    pcall(function()
        if _G.AutoFarmBounty then
            while wait() do
                if game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                end
            end
        end
    end)
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.AutoFarmBounty then
                if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
                end
            end
        end)
    end
end)

spawn(function()
    while task.wait() do
        pcall(function()
            if _G.AutoFarmBounty then
                game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].Cooldown.Value = 0
                spawn(function()
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Beli.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.HP.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Energy.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.StatsButton.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ShopButton.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Skills.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Level.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.MenuButton.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Code.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Settings.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Mute.Visible = false
                    game:GetService("Players")["LocalPlayer"].PlayerGui.Main.CrewButton.Visible = false
                    game.Players.LocalPlayer.Character.Animate.Disabled = true
                end)
            end
        end)
    end
end)
CastlePostoMansion = CFrame.new(-5084.8447265625, 316.48101806641, -3145.3752441406)
MansiontoCastlePos = CFrame.new(-12464.596679688, 376.30590820312, -7567.2626953125)
Castletophydra = CFrame.new(-5095.33984375, 316.48101806641, -3168.3134765625)
HydratoCastle = CFrame.new(5741.869140625, 611.94750976562, -282.61154174805)
spawn(function()
    while wait() do
        pcall(function()
            if _G.AutoFarmBounty then
                for i,v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
                    if v.Name ~= game.Players.LocalPlayer.Name then
                        if v:WaitForChild("Humanoid").Health > 0 and (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - v.HumanoidRootPart.Position).Magnitude <= 17000 then
                            plyselecthunthelpold = v.Humanoid.Health
                            repeat task.wait()
                                EquipWeapon(SelectWeaponGun)
                                NameTarget = v.Name
                                if tostring(game.Players.LocalPlayer.Team) == "Pirates" then
                                    topos(v.HumanoidRootPart.CFrame * CFrame.new(0,60,-20))
                                elseif tostring(game.Players.LocalPlayer.Team) == "Marines" then
                                    if game.Players[NameTarget].Team ~= game.Players.LocalPlayer.Team then
                                        topos(v.HumanoidRootPart.CFrame * CFrame.new(0,60,-20))
                                    end
                                end
                                spawn(function()
                                    if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 150 then
                                        StartCheckTarget = true
                                    end
                                end)
                                v.HumanoidRootPart.CanCollide = false
                                spawn(function()
                                    pcall(function()
                                        local args = {
                                            [1] = v.HumanoidRootPart.Position,
                                            [2] = v.HumanoidRootPart
                                        }
                                        game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(unpack(args))
                                    end)
                                end)
                                TargetSelectHunt = v.Humanoid
                            until _G.AutoFarmBounty == false or v.Humanoid.Health == 0 or not v:FindFirstChild("HumanoidRootPart") or not v:FindFirstChild("Humanoid") or not v.Parent or NextplySelect == true
                            NextplySelect = false
                            StartCheckTarget = false
                        end
                    end
                end
            end
        end)
    end
end)

spawn(function()
    pcall(function()
        while task.wait() do
            if _G.AutoFarmBounty then
                game:GetService("Players").LocalPlayer.PlayerGui.Main.InCombat.Visible = false
                game:GetService("Players").LocalPlayer.PlayerGui.Main.SafeZone.Visible = false
            end
        end
    end)
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoFarmBounty then
                if TargetSelectHunt ~= nil then
                    if StartCheckTarget then
                        wait(6.5)
                        if TargetSelectHunt.Health == TargetSelectHunt.MaxHealth or TargetSelectHunt.Health >= plyselecthunthelpold then
                            NextplySelect = true
                            TargetSelectHunt = nil
                        end
                    end
                end
            end
        end
    end)
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoFarmBounty then
                if game:GetService("Players").LocalPlayer.PlayerGui.Main.PvpDisabled.Visible == true then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EnablePvp")
                end
            end
        end
    end)
end)

Combat:AddToggle("Auto Farm Bounty Hop ",_G.AutoFarmBounty_Hop,function(value)
    _G.AutoFarmBounty_Hop = value
end)

spawn(function()
    while wait() do
        if _G.AutoFarmBounty then
            if _G.AutoFarmBounty_Hop then
                pcall(function()
                    wait(120)
                    Hop()
                end)
            end
        end
    end
end)

Combat:AddSeperator("Misc Bounty")

Combat:AddButton("Next Player ",function()
    NextplySelect = true
end)

Combat:AddSlider("Lock Bounty",1,25000000,750000,function(value)
    _G.BountyLock = value
end)

Combat:AddToggle("Start Bounty Lock",false,function(value)
    _G.StartBountyLock = value
end)

spawn(function()
    while wait() do
        if _G.StartBountyLock then
            pcall(function()
                if game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value >= _G.BountyLock then
                    game:GetService("Players").LocalPlayer:Kick("Successfully! Bounty Farm")
                end
            end)
        end
    end
end)


Misc:AddSeperator("Ui")

Misc:AddButton("Open Devil Shop",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Visible = true
end)

Misc:AddButton("Open Inventory",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryWeapons")
    wait(1)
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = true
end)

Misc:AddButton("Open Inventory Fruit",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventoryFruits")
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Visible = true
end)
Misc:AddButton("Kaiton Picture",function()
    __Config = {
      ['Inventory'] = {
         ['Fillter'] = {
            ['Mythical'] = true,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Mythical
            ['Legendary'] = true,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Legendary
            ['Rare'] = false,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Rare
            ['Uncommon'] = false, -- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Uncommon
         },
         ['Enabled'] = true, -- ถ้าเป็น false จะไม่เช็คของในกล่อง
      },
      ['Malee'] = {
         ['Enabled'] = true, -- ถ้าเป็น false จะไม่เช็คหมัด
      },
      ['AwakeningToggler'] = {
         ['Enabled'] = true -- ถ้าเป็น false จะไม่เช็คสกิลผลตื่น
      },
      ['Money'] = {
         ['Enabled'] = true -- ถ้าเป็น false จะไม่เช็คเงิน แและ เงินม่วง
      },
      ['Fruit'] = {
         ['Enabled'] = true, -- ถ้าเป็น false จะไม่เช็คผล
         ['Fillter'] = { 
            ['Cost'] = 1
         },
        ['Permanent'] = true
      },
  ['RTX'] = {
      ['Enabled'] = false, -- ถ้าเป็น false ไม่มี RTX
      ['Mode'] = '' -- Autumn | Summer | 
  }
   }
   
   
   
   
   
   
   
   
   
   
   
if __Config['RTX']['Mode']['Enabled'] then 
      local a = game.Lighting
	a.Ambient = Color3.fromRGB(33, 33, 33)
	a.Brightness = 6.67
	a.ColorShift_Bottom = Color3.fromRGB(0, 0, 0)
	a.ColorShift_Top = Color3.fromRGB(255, 247, 237)
	a.EnvironmentDiffuseScale = 0.105
	a.EnvironmentSpecularScale = 0.522
	a.GlobalShadows = true
	a.OutdoorAmbient = Color3.fromRGB(51, 54, 67)
	a.ShadowSoftness = 0.04
	a.GeographicLatitude = -15.525
	a.ExposureCompensation = 0.75
	local b = Instance.new("BloomEffect", a)
	b.Enabled = true
	b.Intensity = 0.04
	b.Size = 1900
	b.Threshold = 0.915
	local c = Instance.new("ColorCorrectionEffect", a)
	c.Brightness = 0.176
	c.Contrast = 0.39
	c.Enabled = true
	c.Saturation = 0.2
	c.TintColor = Color3.fromRGB(217, 145, 57)
	if __Config['RTX']['Mode']['Enabled'] == "Summer" then
		c.TintColor = Color3.fromRGB(255, 220, 148)
	elseif __Config['RTX']['Mode']['Enabled'] == "Autumn" then
		c.TintColor = Color3.fromRGB(217, 145, 57)
	elseif __Config['RTX']['Mode']['Enabled'] == 'Cold' then 
		c.TintColor = Color3.fromRGB(0, 215, 255)
	else 
		c.TintColor = Color3.fromRGB(217, 145, 57)
	end
	local d = Instance.new("DepthOfFieldEffect", a)
	d.Enabled = true
	d.FarIntensity = 0.077
	d.FocusDistance = 21.54
	d.InFocusRadius = 20.77
	d.NearIntensity = 0.277
	local e = Instance.new("ColorCorrectionEffect", a)
	e.Brightness = 0
	e.Contrast = -0.07
	e.Saturation = 0
	e.Enabled = true
	e.TintColor = Color3.fromRGB(255, 247, 239)
	local e2 = Instance.new("ColorCorrectionEffect", a)
	e2.Brightness = 0.2
	e2.Contrast = 0.45
	e2.Saturation = -0.1
	e2.Enabled = true
	e2.TintColor = Color3.fromRGB(255, 255, 255)
	local s = Instance.new("SunRaysEffect", a)
	s.Enabled = true
	s.Intensity = 0.01
	s.Spread = 0.146
end
local function formatNumber(number)
   local i, k, j = tostring(number):match("(%-?%d?)(%d*)(%.?.*)")
   return i..k:reverse():gsub("(%d%d%d)", "%1,"):reverse()..j
end
local ItemCheckerOld = game.CoreGui:FindFirstChild('ItemChecker')
if ItemCheckerOld then
   ItemCheckerOld:Destroy()
end
local args = {
   [1] = "BuyDragonTalon",
   [2] = true
}
BuyDragonTalon = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyDragonTalon then
   if BuyDragonTalon == 1 then
      HasTalon = true
   end
end
local args = {
   [1] = "BuySuperhuman",
   [2] = true
}
BuySuperhuman = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuySuperhuman then
   if BuySuperhuman == 1 then
      HasSuperhuman = true
   end
end
local args = {
   [1] = "BuySharkmanKarate",
   [2] = true
}
BuySharkmanKarate = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuySharkmanKarate then
   if BuySharkmanKarate == 1 then
      HasKarate = true
   end
end
local args = {
   [1] = "BuyDeathStep",
   [2] = true
}
BuyDeathStep = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyDeathStep then
   if BuyDeathStep == 1 then
      HasDeathStep = true
   end
end
local args = {
   [1] = "BuyElectricClaw",
   [2] = true
}
BuyElectricClaw = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyElectricClaw then
   if BuyElectricClaw == 1 then
      HasElectricClaw = true
   end
end
local args = {
   [1] = "BuyGodhuman",
   [2] = true
}
BuyGodhuman = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyGodhuman then
   if BuyGodhuman == 1 then
      HasGodhuman = true
   end
end
local data = {}
if HasElectricClaw then
   table.insert(data, {
      ['Name'] = 'ElectricClaw',
      ['AssetID'] = '6866994470'
   })
end
if HasTalon then
   table.insert(data, {
      ['Name'] = 'Dragon Talon',
      ['AssetID'] = '7831677967'
   })
end
if HasSuperhuman then
   table.insert(data, {
      ['Name'] = 'Superhuman',
      ['AssetID'] = '4831781711'
   })
end
if HasKarate then
   table.insert(data, {
      ['Name'] = 'Sharkman Karate',
      ['AssetID'] = '6525157144'
   })
end
if HasDeathStep then
   table.insert(data, {
      ['Name'] = 'Death Step',
      ['AssetID'] = '6085350468'
   })
end
if HasGodhuman then
   table.insert(data, {
      ['Name'] = 'Godhuman',
      ['AssetID'] = '11763197600'
   })
end
local ItemChecker = Instance.new("ScreenGui")
local MaleeFrame = Instance.new("Frame")
local InventoryFrame = Instance.new("Frame")
local PostionX = 0


ItemChecker.Name = "ItemChecker"
ItemChecker.Parent = game.CoreGui
ItemChecker.Enabled = true
ItemChecker.ZIndexBehavior = Enum.ZIndexBehavior.Sibling



InventoryFrame.Name = "InventoryFrame"
InventoryFrame.Parent = ItemChecker
InventoryFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
InventoryFrame.BackgroundTransparency = 1.000
InventoryFrame.BorderSizePixel = 0
InventoryFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)



MaleeFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MaleeFrame.BackgroundTransparency = 1.000
MaleeFrame.BorderSizePixel = 0
MaleeFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)

MaleeFrame.Name = "MaleeFrame"
MaleeFrame.Parent = ItemChecker
MaleeFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MaleeFrame.BackgroundTransparency = 1.000
MaleeFrame.BorderSizePixel = 0
MaleeFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)



if __Config['Malee']['Enabled'] then
   for i, v in pairs(data) do
      local Assets = Instance.new("ImageLabel")

      Assets.Name = v.Name
      Assets.Parent = MaleeFrame
      Assets.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
      Assets.BackgroundTransparency = 1
      Assets.BorderSizePixel = 0
      Assets.Size = UDim2.new(1.1, 0, 1.1, 0)
      Assets.Image = 'rbxassetid://' .. v.AssetID
      Assets.Position =  UDim2.new(PostionX, 0, 0, 0)
      PostionX =  PostionX + 1.13
   end
end
if __Config['Inventory']['Enabled'] then
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 1
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = true
   wait(.5)
   local PostionXInv = 0
   local ItemCount = 0
   local PostionYInv = 1.4
   for c, j in pairs(__Config['Inventory']['Fillter']) do
      for i, v in pairs( game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Stored.ScrollingFrame.Frame:GetChildren()) do
         if v:IsA('ImageButton')  then
            if  v.Name == 'Template'   then
            else
               if string.lower(v.Title.TextLabel.Text) == string.lower(c) and j then
                  item = v:Clone()
                  item.Parent = InventoryFrame
                  item.Position = UDim2.new(PostionXInv, 0, PostionYInv, 0)
                  item.Size = UDim2.new(0.9, 0, 0.9, 0)
                  PostionXInv = PostionXInv + 0.92
                  ItemCount = ItemCount + 1
                  if ItemCount >= 11 then
                     PostionYInv = PostionYInv + 0.9
                     ItemCount = 0
                     PostionXInv = 0
                  end
               end
            end
         end
      end
   end
    for c, j in pairs(__Config['Inventory']['Fillter']) do
      for i, v in pairs( game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Current.ScrollingFrame.Frame:GetChildren()) do
         if v:IsA('ImageButton')  then
            if  v.Name == 'Template'   then
            else
               if string.lower(v.Title.TextLabel.Text) == string.lower(c) and j then
                  item = v:Clone()
                  item.Parent = InventoryFrame
                  item.Position = UDim2.new(PostionXInv, 0, PostionYInv, 0)
                  item.Size = UDim2.new(0.9, 0, 0.9, 0)
                  PostionXInv = PostionXInv + 0.92
                  ItemCount = ItemCount + 1
                  if ItemCount >= 11 then
                     PostionYInv = PostionYInv + 0.9
                     ItemCount = 0
                     PostionXInv = 0
                  end
               end
            end
         end
      end
   end
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 0
end

if __Config['AwakeningToggler']['Enabled'] then
   game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler.Visible = true
   for i, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= false
      end
   end
   wait(.5)
   AwakeningToggler = game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:Clone()
   AwakeningToggler.Parent = ItemChecker
   AwakeningToggler.Position = UDim2.new(0.8, 0, 0.11, 0)
   AwakeningToggler.Size =  UDim2.new(0.379635453, 0, 0.275648952, 0)
   game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler.Visible = false
   for i, v in pairs(AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= true
      end
   end
   for i, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= true
      end
   end
end

if __Config['Money']['Enabled'] then

   local Beil = game:GetService("Players").LocalPlayer.PlayerGui.Main.Beli:Clone()
   Beil.Parent = ItemChecker
   Beil.Position = UDim2.new(0.43683219, 0, 0.823238552, 0)
   Beil.Size = UDim2.new(0.125707105, 0, 0.0618046969, 0)
   local Fragments = game:GetService("Players").LocalPlayer.PlayerGui.Main.Fragments:Clone()
   Fragments.Parent = ItemChecker
   Fragments.Position = UDim2.new(0.43683219, 0, 0.783238552, 0)
   Fragments.Size = UDim2.new(0.125707105, 0, 0.0618046969, 0)
   Fragments.Text = 'ƒ' .. formatNumber(game:GetService("Players").LocalPlayer.Data.Fragments.Value)
end
local FruitFrame = Instance.new("Frame")



FruitFrame.Name = "FruitFrame"
FruitFrame.Parent = ItemChecker
FruitFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FruitFrame.BackgroundTransparency = 1.000
FruitFrame.BorderSizePixel = 0
FruitFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)

local TableFruitL = {}
if __Config['Fruit']['Enabled'] then

   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Title.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Container.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Info.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.BackgroundTransparency = 1
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Visible = true
   wait(.5)
   local PostionXInvCuurect = 2.93683219
   local ItemCountCuurect = 0
   local PostionYInvCuurect = 4.683238552
   local args = {
            [1] = "getInventoryFruits"
        }
        
        remote = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        for i, v in pairs(remote) do 
            if v['Price'] >= __Config['Fruit']['Fillter']['Cost'] then 
                   table.insert(TableFruitL, {
                       ['Name'] = v['Name']
                   })
            end
        end
      for i, v in pairs(TableFruitL) do
        
                v = game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Container.Stored.ScrollingFrame.Frame:FindFirstChild(v['Name'])
               item = v:Clone()
               item.Parent = FruitFrame
               item.Position = UDim2.new(PostionXInvCuurect, 0, PostionYInvCuurect, 0)
               item.Size = UDim2.new(0.9, 0, 0.9, 0)
               PostionXInvCuurect = PostionXInvCuurect + 0.92
               ItemCountCuurect = ItemCountCuurect + 1
               if ItemCountCuurect >= 11 then
                  PostionYInvCuurect = PostionYInvCuurect + 0.9
                  ItemCountCuurect = 0
                  PostionXInvCuurect = 2.93683219

               
            
         end
      end
      
      

    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = false
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 0
end
local FruitPermanentFrame = Instance.new("Frame")
FruitPermanentFrame.Parent = ItemChecker
FruitPermanentFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FruitPermanentFrame.BackgroundTransparency = 1.000
FruitPermanentFrame.BorderSizePixel = 0
FruitPermanentFrame.Size = UDim2.new(0, 100, 0, 100)
local TableFruitP = {}
local PostionYInvFruit = 1.97000003
if __Config['Fruit']['Permanent'] then 
    local args = {
        [1] = "GetFruits",
        [2] = false
    }
    remote = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    for i, v in pairs(remote) do
            if v['HasPermanent'] then 
                    table.insert(TableFruitP, {
                        ['Name'] = v['Name']
                    })
            end
    end
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.BackgroundTransparency = 1 
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Visible = false
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Visible = true
     repeat wait() until game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Center.ScrollingFrame.Container:FindFirstChild("Bomb-Bomb")
     if #TableFruitP >= 4 then 
        PostionYSalceF = 0.5     
     end
    
     wait(.5)
     for i, v in pairs(TableFruitP) do 
         Assets = game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Center.ScrollingFrame.Container:FindFirstChild(v['Name']):Clone()
         Assets.Parent = FruitPermanentFrame
         Assets.Position = UDim2.new(11.3400002, 0, PostionYInvFruit, 0)
         Assets.Size = UDim2.new(4.57000017, 0, PostionYSalceF, 0)
         PostionYInvFruit = PostionYInvFruit + 1
     end
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Visible = false
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.BackgroundTransparency = 1 
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Visible = true
end


end)
Misc:AddButton("Delete Picture",function()
    __Config = {
      ['Inventory'] = {
         ['Fillter'] = {
            ['Mythical'] = false,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Mythical
            ['Legendary'] = false,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Legendary
            ['Rare'] = false,-- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Rare
            ['Uncommon'] = false, -- ถ้าเป็น false จะไม่เช็คของในกล่อง ระดับ Uncommon
         },
         ['Enabled'] = false, -- ถ้าเป็น false จะไม่เช็คของในกล่อง
      },
      ['Malee'] = {
         ['Enabled'] = false, -- ถ้าเป็น false จะไม่เช็คหมัด
      },
      ['AwakeningToggler'] = {
         ['Enabled'] = false -- ถ้าเป็น false จะไม่เช็คสกิลผลตื่น
      },
      ['Money'] = {
         ['Enabled'] = false -- ถ้าเป็น false จะไม่เช็คเงิน แและ เงินม่วง
      },
      ['Fruit'] = {
         ['Enabled'] = false, -- ถ้าเป็น false จะไม่เช็คผล
         ['Fillter'] = { 
            ['Cost'] = 1
         },
        ['Permanent'] = false
      },
  ['RTX'] = {
      ['Enabled'] = false, -- ถ้าเป็น false ไม่มี RTX
      ['Mode'] = '' -- Autumn | Summer | 
  }
   }
   
if __Config['RTX']['Mode']['Enabled'] then 
      local a = game.Lighting
	a.Ambient = Color3.fromRGB(33, 33, 33)
	a.Brightness = 6.67
	a.ColorShift_Bottom = Color3.fromRGB(0, 0, 0)
	a.ColorShift_Top = Color3.fromRGB(255, 247, 237)
	a.EnvironmentDiffuseScale = 0.105
	a.EnvironmentSpecularScale = 0.522
	a.GlobalShadows = true
	a.OutdoorAmbient = Color3.fromRGB(51, 54, 67)
	a.ShadowSoftness = 0.04
	a.GeographicLatitude = -15.525
	a.ExposureCompensation = 0.75
	local b = Instance.new("BloomEffect", a)
	b.Enabled = true
	b.Intensity = 0.04
	b.Size = 1900
	b.Threshold = 0.915
	local c = Instance.new("ColorCorrectionEffect", a)
	c.Brightness = 0.176
	c.Contrast = 0.39
	c.Enabled = true
	c.Saturation = 0.2
	c.TintColor = Color3.fromRGB(217, 145, 57)
	if __Config['RTX']['Mode']['Enabled'] == "Summer" then
		c.TintColor = Color3.fromRGB(255, 220, 148)
	elseif __Config['RTX']['Mode']['Enabled'] == "Autumn" then
		c.TintColor = Color3.fromRGB(217, 145, 57)
	elseif __Config['RTX']['Mode']['Enabled'] == 'Cold' then 
		c.TintColor = Color3.fromRGB(0, 215, 255)
	else 
		c.TintColor = Color3.fromRGB(217, 145, 57)
	end
	local d = Instance.new("DepthOfFieldEffect", a)
	d.Enabled = true
	d.FarIntensity = 0.077
	d.FocusDistance = 21.54
	d.InFocusRadius = 20.77
	d.NearIntensity = 0.277
	local e = Instance.new("ColorCorrectionEffect", a)
	e.Brightness = 0
	e.Contrast = -0.07
	e.Saturation = 0
	e.Enabled = true
	e.TintColor = Color3.fromRGB(255, 247, 239)
	local e2 = Instance.new("ColorCorrectionEffect", a)
	e2.Brightness = 0.2
	e2.Contrast = 0.45
	e2.Saturation = -0.1
	e2.Enabled = true
	e2.TintColor = Color3.fromRGB(255, 255, 255)
	local s = Instance.new("SunRaysEffect", a)
	s.Enabled = true
	s.Intensity = 0.01
	s.Spread = 0.146
end
local function formatNumber(number)
   local i, k, j = tostring(number):match("(%-?%d?)(%d*)(%.?.*)")
   return i..k:reverse():gsub("(%d%d%d)", "%1,"):reverse()..j
end
local ItemCheckerOld = game.CoreGui:FindFirstChild('ItemChecker')
if ItemCheckerOld then
   ItemCheckerOld:Destroy()
end
local args = {
   [1] = "BuyDragonTalon",
   [2] = true
}
BuyDragonTalon = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyDragonTalon then
   if BuyDragonTalon == 1 then
      HasTalon = true
   end
end
local args = {
   [1] = "BuySuperhuman",
   [2] = true
}
BuySuperhuman = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuySuperhuman then
   if BuySuperhuman == 1 then
      HasSuperhuman = true
   end
end
local args = {
   [1] = "BuySharkmanKarate",
   [2] = true
}
BuySharkmanKarate = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuySharkmanKarate then
   if BuySharkmanKarate == 1 then
      HasKarate = true
   end
end
local args = {
   [1] = "BuyDeathStep",
   [2] = true
}
BuyDeathStep = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyDeathStep then
   if BuyDeathStep == 1 then
      HasDeathStep = true
   end
end
local args = {
   [1] = "BuyElectricClaw",
   [2] = true
}
BuyElectricClaw = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)))
if BuyElectricClaw then
   if BuyElectricClaw == 1 then
      HasElectricClaw = true
   end
end
local data = {}
if HasElectricClaw then
   table.insert(data, {
      ['Name'] = 'ElectricClaw',
      ['AssetID'] = '6866994470'
   })
end
if HasTalon then
   table.insert(data, {
      ['Name'] = 'Dragon Talon',
      ['AssetID'] = '7831677967'
   })
end
if HasSuperhuman then
   table.insert(data, {
      ['Name'] = 'Superhuman',
      ['AssetID'] = '4831781711'
   })
end
if HasKarate then
   table.insert(data, {
      ['Name'] = 'Sharkman Karate',
      ['AssetID'] = '6525157144'
   })
end
if HasDeathStep then
   table.insert(data, {
      ['Name'] = 'Death Step',
      ['AssetID'] = '6085350468'
   })
end
local ItemChecker = Instance.new("ScreenGui")
local MaleeFrame = Instance.new("Frame")
local InventoryFrame = Instance.new("Frame")
local PostionX = 0


ItemChecker.Name = "ItemChecker"
ItemChecker.Parent = game.CoreGui
ItemChecker.Enabled = true
ItemChecker.ZIndexBehavior = Enum.ZIndexBehavior.Sibling



InventoryFrame.Name = "InventoryFrame"
InventoryFrame.Parent = ItemChecker
InventoryFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
InventoryFrame.BackgroundTransparency = 1.000
InventoryFrame.BorderSizePixel = 0
InventoryFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)



MaleeFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MaleeFrame.BackgroundTransparency = 1.000
MaleeFrame.BorderSizePixel = 0
MaleeFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)

MaleeFrame.Name = "MaleeFrame"
MaleeFrame.Parent = ItemChecker
MaleeFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
MaleeFrame.BackgroundTransparency = 1.000
MaleeFrame.BorderSizePixel = 0
MaleeFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)



if __Config['Malee']['Enabled'] then
   for i, v in pairs(data) do
      local Assets = Instance.new("ImageLabel")

      Assets.Name = v.Name
      Assets.Parent = MaleeFrame
      Assets.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
      Assets.BackgroundTransparency = 1
      Assets.BorderSizePixel = 0
      Assets.Size = UDim2.new(1.1, 0, 1.1, 0)
      Assets.Image = 'rbxassetid://' .. v.AssetID
      Assets.Position =  UDim2.new(PostionX, 0, 0, 0)
      PostionX =  PostionX + 1.13
   end
end
if __Config['Inventory']['Enabled'] then
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 1
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = true
   wait(.5)
   local PostionXInv = 0
   local ItemCount = 0
   local PostionYInv = 1.4
   for c, j in pairs(__Config['Inventory']['Fillter']) do
      for i, v in pairs( game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Stored.ScrollingFrame.Frame:GetChildren()) do
         if v:IsA('ImageButton')  then
            if  v.Name == 'Template'   then
            else
               if string.lower(v.Title.TextLabel.Text) == string.lower(c) and j then
                  item = v:Clone()
                  item.Parent = InventoryFrame
                  item.Position = UDim2.new(PostionXInv, 0, PostionYInv, 0)
                  item.Size = UDim2.new(0.9, 0, 0.9, 0)
                  PostionXInv = PostionXInv + 0.92
                  ItemCount = ItemCount + 1
                  if ItemCount >= 11 then
                     PostionYInv = PostionYInv + 0.9
                     ItemCount = 0
                     PostionXInv = 0
                  end
               end
            end
         end
      end
   end
    for c, j in pairs(__Config['Inventory']['Fillter']) do
      for i, v in pairs( game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Current.ScrollingFrame.Frame:GetChildren()) do
         if v:IsA('ImageButton')  then
            if  v.Name == 'Template'   then
            else
               if string.lower(v.Title.TextLabel.Text) == string.lower(c) and j then
                  item = v:Clone()
                  item.Parent = InventoryFrame
                  item.Position = UDim2.new(PostionXInv, 0, PostionYInv, 0)
                  item.Size = UDim2.new(0.9, 0, 0.9, 0)
                  PostionXInv = PostionXInv + 0.92
                  ItemCount = ItemCount + 1
                  if ItemCount >= 11 then
                     PostionYInv = PostionYInv + 0.9
                     ItemCount = 0
                     PostionXInv = 0
                  end
               end
            end
         end
      end
   end
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = true
   game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 0
end

if __Config['AwakeningToggler']['Enabled'] then
   game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler.Visible = true
   for i, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= false
      end
   end
   wait(.5)
   AwakeningToggler = game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:Clone()
   AwakeningToggler.Parent = ItemChecker
   AwakeningToggler.Position = UDim2.new(0.8, 0, 0.11, 0)
   AwakeningToggler.Size =  UDim2.new(0.379635453, 0, 0.275648952, 0)
   game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler.Visible = false
   for i, v in pairs(AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= true
      end
   end
   for i, v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Main.AwakeningToggler:GetChildren()) do
      if  v:IsA('Frame') or v:IsA('TextLabel') then
         v.Visible= true
      end
   end
end

if __Config['Money']['Enabled'] then

   local Beil = game:GetService("Players").LocalPlayer.PlayerGui.Main.Beli:Clone()
   Beil.Parent = ItemChecker
   Beil.Position = UDim2.new(0.43683219, 0, 0.823238552, 0)
   Beil.Size = UDim2.new(0.125707105, 0, 0.0618046969, 0)
   local Fragments = game:GetService("Players").LocalPlayer.PlayerGui.Main.Fragments:Clone()
   Fragments.Parent = ItemChecker
   Fragments.Position = UDim2.new(0.43683219, 0, 0.783238552, 0)
   Fragments.Size = UDim2.new(0.125707105, 0, 0.0618046969, 0)
   Fragments.Text = 'ƒ' .. formatNumber(game:GetService("Players").LocalPlayer.Data.Fragments.Value)
end
local FruitFrame = Instance.new("Frame")



FruitFrame.Name = "FruitFrame"
FruitFrame.Parent = ItemChecker
FruitFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FruitFrame.BackgroundTransparency = 1.000
FruitFrame.BorderSizePixel = 0
FruitFrame.Size = UDim2.new(0.0628535524, 0, 0.123609394, 0)

local TableFruitL = {}
if __Config['Fruit']['Enabled'] then

   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Title.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Container.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Info.Visible = false
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.BackgroundTransparency = 1
   game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Visible = true
   wait(.5)
   local PostionXInvCuurect = 2.93683219
   local ItemCountCuurect = 0
   local PostionYInvCuurect = 4.683238552
   local args = {
            [1] = "getInventoryFruits"
        }
        
        remote = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        for i, v in pairs(remote) do 
            if v['Price'] >= __Config['Fruit']['Fillter']['Cost'] then 
                   table.insert(TableFruitL, {
                       ['Name'] = v['Name']
                   })
            end
        end
      for i, v in pairs(TableFruitL) do
        
                v = game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitInventory.Container.Stored.ScrollingFrame.Frame:FindFirstChild(v['Name'])
               item = v:Clone()
               item.Parent = FruitFrame
               item.Position = UDim2.new(PostionXInvCuurect, 0, PostionYInvCuurect, 0)
               item.Size = UDim2.new(0.9, 0, 0.9, 0)
               PostionXInvCuurect = PostionXInvCuurect + 0.92
               ItemCountCuurect = ItemCountCuurect + 1
               if ItemCountCuurect >= 11 then
                  PostionYInvCuurect = PostionYInvCuurect + 0.9
                  ItemCountCuurect = 0
                  PostionXInvCuurect = 2.93683219

               
            
         end
      end
      
      

    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Visible = false
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Title.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Container.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.Info.Visible = true
    game:GetService("Players").LocalPlayer.PlayerGui.Main.Inventory.BackgroundTransparency = 0
end
local FruitPermanentFrame = Instance.new("Frame")
FruitPermanentFrame.Parent = ItemChecker
FruitPermanentFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FruitPermanentFrame.BackgroundTransparency = 1.000
FruitPermanentFrame.BorderSizePixel = 0
FruitPermanentFrame.Size = UDim2.new(0, 100, 0, 100)
local TableFruitP = {}
local PostionYInvFruit = 1.97000003
if __Config['Fruit']['Permanent'] then 
    local args = {
        [1] = "GetFruits",
        [2] = false
    }
    remote = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    for i, v in pairs(remote) do
            if v['HasPermanent'] then 
                    table.insert(TableFruitP, {
                        ['Name'] = v['Name']
                    })
            end
    end
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.BackgroundTransparency = 1 
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Visible = false
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Visible = true
     repeat wait() until game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Center.ScrollingFrame.Container:FindFirstChild("Bomb-Bomb")
     if #TableFruitP >= 4 then 
        PostionYSalceF = 0.5     
     end
    
     wait(.5)
     for i, v in pairs(TableFruitP) do 
         Assets = game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Center.ScrollingFrame.Container:FindFirstChild(v['Name']):Clone()
         Assets.Parent = FruitPermanentFrame
         Assets.Position = UDim2.new(11.3400002, 0, PostionYInvFruit, 0)
         Assets.Size = UDim2.new(4.57000017, 0, PostionYSalceF, 0)
         PostionYInvFruit = PostionYInvFruit + 1
     end
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Visible = false
    game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.BackgroundTransparency = 1 
     game:GetService("Players").LocalPlayer.PlayerGui.Main.FruitShop.Left.Visible = true
end


end)

Misc:AddToggle("Highlight Mode ",false,function(value)
    if value == true then
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Beli.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.HP.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Energy.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.StatsButton.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ShopButton.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Skills.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Level.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.MenuButton.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Code.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Settings.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Mute.Visible = false
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.CrewButton.Visible = false
    else
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Beli.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.HP.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Energy.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.StatsButton.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ShopButton.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Skills.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Level.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.MenuButton.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Code.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Settings.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Mute.Visible = true
        game:GetService("Players")["LocalPlayer"].PlayerGui.Main.CrewButton.Visible = true
    end
end)

Misc:AddSeperator("Teams")

Misc:AddButton("Join Pirates Team",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Pirates") 
end)

Misc:AddButton("Join Marines Team",function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Marines") 
end)

Misc:AddSeperator("Boost")

Misc:AddButton("Unlock Portal",function()
    _G.UnlockPortal = true
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.UnlockPortal == true then
                for i,v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Notifications:GetChildren()) do
                    if v.Name == "NotificationTemplate" then
                        if string.find(v.Text,"cannot") then
                            v:Destroy()
                        end
                    end
                end
            end
        end)
    end
end)

spawn(function()
    while wait() do
        pcall(function()
            if _G.UnlockPortal == true then
                CastlePostoMansion = CFrame.new(-5084.8447265625, 316.48101806641, -3145.3752441406)
                MansiontoCastlePos = CFrame.new(-12464.596679688, 376.30590820312, -7567.2626953125)
                Castletophydra = CFrame.new(-5095.33984375, 316.48101806641, -3168.3134765625)
                HydratoCastle = CFrame.new(5741.869140625, 611.94750976562, -282.61154174805)
                if (CastlePostoMansion.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 8 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12471.169921875, 374.94024658203, -7551.677734375))
                end
                if (MansiontoCastlePos.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 8 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-5072.08984375, 314.5412902832, -3151.1098632812))
                end
                if (Castletophydra.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 8 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(5748.7587890625, 610.44982910156, -267.81704711914))
                end
                if (HydratoCastle.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 8 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-5072.08984375, 314.5412902832, -3151.1098632812))
                end
            end
        end)
    end
end)

Misc:AddButton("Invisible",function()
    game:GetService("Players").LocalPlayer.Character.LowerTorso:Destroy()
end)

Misc:AddButton("Click TP Tool",function()
    local plr = game:GetService("Players").LocalPlayer
    local mouse = plr:GetMouse()
    local tool = Instance.new("Tool")
    tool.RequiresHandle = false
    tool.Name = "Teleport Tool"
    tool.Activated:Connect(function()
    local root = plr.Character.HumanoidRootPart
    local pos = mouse.Hit.Position+Vector3.new(0,2.5,0)
    local offset = pos-root.Position
    root.CFrame = root.CFrame+offset
    end)
    tool.Parent = plr.Backpack
end)

Misc:AddButton("Stop All Tween",function()
    topos(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
    _G.Clip = false
end)

Misc:AddSeperator("Codes")

local x2Code = {
    "3BVISITS",
    "UPD16",
    "FUDD10",
    "BIGNEWS",
    "THEGREATACE",
    "SUB2GAMERROBOT_EXP1",
    "StrawHatMaine",
    "Sub2OfficialNoobie",
    "SUB2NOOBMASTER123",
    "Sub2Daigrock",
    "Axiore",
    "TantaiGaming",
    "STRAWHATMAINE",
    "Enyu_is_Pro",
    "Sub2Fer999",
    "Bluxxy",
    "JCWK",
    "Magicbus",
    "Starcodeheo",
    "SUB2UNCLEKIZARU"
}

Misc:AddButton("Redeem All Codes",function()
    function RedeemCode(value)
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(value)
    end
    for i,v in pairs(x2Code) do
        RedeemCode(v)
    end
end)

Misc:AddDropdown("Selected Codes",x2Code,function(value)
    _G.CodeSelect = value
end)

Misc:AddButton("Redeem Code",function()
    game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(_G.CodeSelect)
end)

Misc:AddSeperator("State")

Misc:AddDropdown("Select Haki State",{"State 0","State 1","State 2","State 3","State 4","State 5"},function(value)
    _G.SelectStateHaki = value
end)

Misc:AddButton("Change Buso Haki State",function()
    if _G.SelectStateHaki == "State 0" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",0)
    elseif _G.SelectStateHaki == "State 1" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",1)
    elseif _G.SelectStateHaki == "State 2" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",2)
    elseif _G.SelectStateHaki == "State 3" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",3)
    elseif _G.SelectStateHaki == "State 4" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",4)
    elseif _G.SelectStateHaki == "State 5" then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",5)
    end
end)


Misc:AddSeperator("Abilities")

Misc:AddToggle("Infinite Energy ",false,function(value)
    InfiniteEnergy = value
    originalstam = LocalPlayer.Character.Energy.Value
end)

Misc:AddToggle("Auto Active Race ",_G.AutoAgility,function(value)
    _G.AutoAgility = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoAgility then
                game:GetService("ReplicatedStorage").Remotes.CommE:FireServer("ActivateAbility")
            end
        end
    end)
end)

Misc:AddToggle("Fake Mink Animation ",false,function(value)
loadstring(game:HttpGet("https://pastebin.com/raw/Q0B4FGeg"))()
end)

Misc:AddToggle("Fake Mink V4 Transform [ฃ",false, function(value)
loadstring(game:HttpGet("https://pastebin.com/raw/44SFM0h2"))()
end)

Misc:AddToggle("Infinite Ability",false,function(value)
    InfAbility = value
    if value == false then
        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("Agility"):Destroy()
    end
end)

spawn(function()
    while wait() do
        if InfAbility then
            InfAb()
        end
    end
end)

Misc:AddToggle("Infinite Obversation Range [ฃ",getgenv().InfiniteObRange,function(value)
    getgenv().InfiniteObRange = value
    local VS = game:GetService("Players").LocalPlayer.VisionRadius.Value
    while getgenv().InfiniteObRange do
        wait()
        local player = game:GetService("Players").LocalPlayer
        local char = player.Character
        local VisionRadius = player.VisionRadius
        if player then
            if char.Humanoid.Health <= 0 then 
                wait(5) 
            end
            VisionRadius.Value = math.huge
        elseif getgenv().InfiniteObRange == false and player then
            VisionRadius.Value = VS
        end
    end
end)

Misc:AddToggle("Walk on Water ",_G.WalkWater,function(value)
    _G.WalkWater = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.WalkWater then
                if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.Y <= 1 then
                    if not game:GetService("Workspace"):FindFirstChild("Water") then
                        local Water = Instance.new("Part", game:GetService("Workspace"))
                        Water.Name = "Water"
                        Water.Size = Vector3.new(15,0.5,15)
                        Water.Anchored = true
                        Water.Material = "Neon"
                        Water.Color = _G.Color
                        game:GetService("Workspace").Water.CFrame = CFrame.new(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.X,game:GetService("Workspace").Camera["Water;"].CFrame.Y,game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
                    else
                        game:GetService("Workspace").Water.CFrame = CFrame.new(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.X,game:GetService("Workspace").Camera["Water;"].CFrame.Y,game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
                    end
                elseif game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame.Y >= 1 and game:GetService("Workspace"):FindFirstChild("Water") then
                    game:GetService("Workspace"):FindFirstChild("Water"):Destroy()
                end
            else
                if game:GetService("Workspace"):FindFirstChild("Water") then
                    game:GetService("Workspace"):FindFirstChild("Water"):Destroy()
                end
            end
        end
    end)
end)

Misc:AddToggle("Fly ",false,function(value)
    Fly = value
end)

spawn(function()
    while wait() do
        pcall(function()
            if Fly then
                fly()
            end
        end)
    end
end)

Misc:AddToggle("NoClip ",_G.NOCLIP,function(value)
    _G.NOCLIP = value
end)

Misc:AddSeperator("Level")

Misc:AddTextbox("Level","",true,function(value)
    getgenv().Level = value
end)

Misc:AddToggle("Lock Level ",_G.LockLevel,function(value)
    _G.LockLevel = value
end)

spawn(function()
	while wait() do 
		if _G.LockLevel then
			pcall(function()
				if game.Players.LocalPlayer.Data.Level.Value >= tonumber(getgenv().Level) then
					game.Players.LocalPlayer:Kick("\nSuccessfully Farm!")
				end
			end)
		end
	end
end)

local plyserv = Combat:AddLabel("Players")

spawn(function()
    while wait() do
        pcall(function()
            for i,v in pairs(game:GetService("Players"):GetPlayers()) do
                if i == 12 then
                    plyserv:Set("Players :".." "..i.." ".."/".." ".."12".." ".."(Max)")
                elseif i == 1 then
                    plyserv:Set("Player :".." "..i.." ".."/".." ".."12")
                else
                    plyserv:Set("Players :".." "..i.." ".."/".." ".."12")
                end
            end
        end)
    end
end)

Playerslist = {}

for i,v in pairs(game:GetService("Players"):GetChildren()) do
    table.insert(Playerslist,v.Name)
end

local SelectedPly = Combat:AddDropdown("Select Players",Playerslist,function(value)
    _G.SelectPly = value
end)

Combat:AddButton("Refresh Player",function()
    Playerslist = {}
    SelectedPly:Clear()
    for i,v in pairs(game:GetService("Players"):GetChildren()) do  
        SelectedPly:Add(v.Name)
    end
end)

Combat:AddToggle("Spectate Player ",false,function(value)
    SpectatePlys = value
    local plr1 = game:GetService("Players").LocalPlayer.Character.Humanoid
    local plr2 = game:GetService("Players"):FindFirstChild(_G.SelectPly)
    repeat wait(.1)
        game:GetService("Workspace").Camera.CameraSubject = game:GetService("Players"):FindFirstChild(_G.SelectPly).Character.Humanoid
    until SpectatePlys == false 
    game:GetService("Workspace").Camera.CameraSubject = game:GetService("Players").LocalPlayer.Character.Humanoid
end)

Combat:AddToggle("Teleport",false,function(value)
    _G.TeleportPly = value
    pcall(function()
        if _G.TeleportPly then
            repeat topos(game:GetService("Players")[_G.SelectPly].Character.HumanoidRootPart.CFrame) wait() until _G.TeleportPly == false
        end
        StopTween(_G.TeleportPly)
    end)
end)

Combat:AddToggle("Auto Farm Player ",false,function(value)
    _G.Auto_Kill_Ply = value
    StopTween(_G.Auto_Kill_Ply)
end)

spawn(function()
    while wait() do
        if _G.Auto_Kill_Ply then
            pcall(function()
                if _G.SelectPly ~= nil then 
                    if game.Players:FindFirstChild(_G.SelectPly) then
                        if game.Players:FindFirstChild(_G.SelectPly).Character.Humanoid.Health > 0 then
                            repeat task.wait()
                                EquipWeapon(_G.SelectWeapon)
                                AutoHaki()
                                game.Players:FindFirstChild(_G.SelectPly).Character.HumanoidRootPart.CanCollide = false
                                topos(game.Players:FindFirstChild(_G.SelectPly).Character.HumanoidRootPart.CFrame * CFrame.new(0,35,0))
                                spawn(function()
                                    pcall(function()
                                        if _G.SelectWeapon == SelectWeaponGun then
                                            local args = {
                                                [1] = game.Players:FindFirstChild(_G.SelectPly).Character.HumanoidRootPart.Position,
                                                [2] = game.Players:FindFirstChild(_G.SelectPly).Character.HumanoidRootPart
                                            }
                                            game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(unpack(args))
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                        else
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                        end
                                    end)
                                end)
                            until game.Players:FindFirstChild(_G.SelectPly).Character.Humanoid.Health <= 0 or not game.Players:FindFirstChild(_G.SelectPly) or not _G.Auto_Kill_Ply
                        end
                    end
                end
            end)
        end
    end
end)


Main:AddSeperator("Fighting Style")

Main:AddToggle("Auto Superhuman",_G.AutoSuperhuman,function(value)
    _G.AutoSuperhuman = value
end)

spawn(function()
    pcall(function()
        while wait() do 
            if _G.AutoSuperhuman then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 150000 then
                    UnEquipWeapon("Combat")
                    wait(.1)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
                end   
                if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") then
                	_G.SelectWeapon = "Superhuman"
                end  
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") or game.Players.LocalPlayer.Character:FindFirstChild("Electro") or game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 then
                        _G.SelectWeapon = "Black Leg"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299 then
                    	_G.SelectWeapon = "Electro"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 then
                    	_G.SelectWeapon = "Fishman Karate"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299 then
                    	_G.SelectWeapon = "Dragon Claw"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                    	UnEquipWeapon("Black Leg")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                        UnEquipWeapon("Black Leg")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                        UnEquipWeapon("Electro")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                        UnEquipWeapon("Electro")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                        UnEquipWeapon("Fishman Karate")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                        UnEquipWeapon("Fishman Karate")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                        UnEquipWeapon("Dragon Claw")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                        UnEquipWeapon("Dragon Claw")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                    end 
                end
            end
        end
    end)
end)

Main:AddToggle("Auto DeathStep",_G.AutoDeathStep,function(value)
    _G.AutoDeathStep = value
end)

spawn(function()
    while wait() do wait()
        if _G.AutoDeathStep then
            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Death Step") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Death Step") then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 450 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
                    _G.SelectWeapon = "Death Step"
                end  
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 450 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
                    _G.SelectWeapon = "Death Step"
                end  
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 449 then
                    _G.SelectWeapon = "Black Leg"
                end 
            else 
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
            end
        end
    end
end)

Main:AddToggle("Auto Sharkman Karate",_G.AutoSharkman,function(value)
    _G.AutoSharkman = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoSharkman then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate"), "keys") then  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key") then
                        topos(CFrame.new(-2604.6958, 239.432526, -10315.1982, 0.0425701365, 0, -0.999093413, 0, 1, 0, 0.999093413, 0, 0.0425701365))
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                    elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 400 then
                    else 
                        Ms = "Tide Keeper [Lv. 1475] [Boss]"
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then   
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == Ms then    
                                    OldCFrameShark = v.HumanoidRootPart.CFrame
                                    repeat task.wait()
                                        AutoHaki()
                                        EquipWeapon(_G.SelectWeapon)
                                        v.Head.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        v.HumanoidRootPart.CanCollide = false
                                        v.HumanoidRootPart.CFrame = OldCFrameShark
                                        topos(v.HumanoidRootPart.CFrame*CFrame.new(0,35,0))
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(1280, 670))
                                        sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                    until not v.Parent or v.Humanoid.Health <= 0 or _G.AutoSharkman == false or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key")
                                end
                            end
                        else
                            topos(CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202))
                            wait(3)
                        end
                    end
                else 
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                end
            end
        end
    end)
end)

Main:AddToggle("Auto Electric Claw",_G.AutoElectricClaw,function(value)
    _G.AutoElectricClaw = value
    StopTween(_G.AutoElectricClaw)
end)

spawn(function()
    pcall(function()
        while wait() do 
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electric Claw") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electric Claw") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.SelectWeapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.SelectWeapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 399 then
                        _G.SelectWeapon = "Electro"
                    end 
                else
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                end
            end
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        if _G.AutoFarm == false then
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))           
                            wait(1.1)                
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(.5)
                            TP(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))                            
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))                           
                            wait(1.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        elseif _G.AutoFarm == true then
                            _G.AutoFarm = false
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))           
                            wait(1.1)                
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(.5)
                            TP(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))                            
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))                           
                            wait(1.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                            _G.SelectWeapon = "Electric Claw"
                            _G.AutoFarm = true
                        end
                    end
                end
            end
        end
    end)    
end)


Main:AddSeperator("Fighting Style")

Main:AddToggle("Auto Superhuman ",_G.AutoSuperhuman,function(value)
    _G.AutoSuperhuman = value
end)

spawn(function()
        pcall(function()
            while wait() do 
                if _G.AutoSuperhuman then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 150000 then
                        UnEquipWeapon("Combat")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
                    end   
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
                        _G.SelectWeapon = "Combat"
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") then
                        _G.SelectWeapon = "Superhuman"
                    end  
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") or game.Players.LocalPlayer.Character:FindFirstChild("Electro") or game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 then
                            _G.SelectWeapon = "Black Leg"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299 then
                            _G.SelectWeapon = "Electro"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 then
                            _G.SelectWeapon = "Fishman Karate"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299 then
                            _G.SelectWeapon = "Dragon Claw"
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                            UnEquipWeapon("Black Leg")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                            UnEquipWeapon("Black Leg")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                            UnEquipWeapon("Electro")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                            UnEquipWeapon("Electro")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                            UnEquipWeapon("Fishman Karate")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                            UnEquipWeapon("Fishman Karate")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                        end
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                            UnEquipWeapon("Dragon Claw")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                        end
                        if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                            UnEquipWeapon("Dragon Claw")
                            wait(.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                        end 
                    end
                end
            end
        end)
    end)

Main:AddToggle("Auto DeathStep ",_G.AutoDeathStep,function(value)
    _G.AutoDeathStep = value
end)

spawn(function()
 while wait() do wait()
 if _G.AutoDeathStep then
 if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Death Step") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Death Step") then
 if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 450 then
 game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
 _G.Setting_table.Weapon = "Death Step"
 end
 if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 450 then
 game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
 _G.Setting_table.Weapon = "Death Step"
 end
 if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 449 then
 _G.Setting_table.Weapon = "Black Leg"
 end
 else
  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
 end
 end
 end
 end)

Main:AddToggle("Auto Sharkman Karate ",_G.AutoSharkman,function(value)
    _G.AutoSharkman = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoSharkman then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate"), "keys") then  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key") then
                        topos(CFrame.new(-2604.6958, 239.432526, -10315.1982, 0.0425701365, 0, -0.999093413, 0, 1, 0, 0.999093413, 0, 0.0425701365))
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                    elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 400 then
                    else 
                        Ms = "Tide Keeper [Lv. 1475] [Boss]"
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then   
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == Ms then    
                                    OldCFrameShark = v.HumanoidRootPart.CFrame
                                    repeat task.wait()
                                        AutoHaki()
                                        EquipWeapon(_G.SelectWeapon)
                                        v.Head.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        v.HumanoidRootPart.CanCollide = false
                                        v.HumanoidRootPart.CFrame = OldCFrameShark
                                        topos(v.HumanoidRootPart.CFrame*CFrame.new(0,35,0))
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(1280, 670))
                                        sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                    until not v.Parent or v.Humanoid.Health <= 0 or _G.AutoSharkman == false or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key")
                                end
                            end
                        else
                            topos(CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202))
                            wait(3)
                        end
                    end
                else 
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                end
            end
        end
    end)
end)

Main:AddToggle("Auto Electric Claw ",_G.AutoElectricClaw,function(value)
    _G.AutoElectricClaw = value
    StopTween(_G.AutoElectricClaw)
end)

spawn(function()
    pcall(function()
        while wait() do 
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electric Claw") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electric Claw") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.SelectWeapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.SelectWeapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 399 then
                        _G.SelectWeapon = "Electro"
                    end 
                else
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                end
            end
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        if _G.AutoFarm == false then
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))           
                            wait(1.1)                
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(.5)
                            TP(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))                            
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))                           
                            wait(1.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        elseif _G.AutoFarm == true then
                            _G.AutoFarm = false
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))           
                            wait(1.1)                
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(.5)
                            TP(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))                            
                            wait(.5)
                            TP(CFrame.new(-10371.4717, 330.764496, -10131.4199))                           
                            wait(1.1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                            _G.SelectWeapon = "Electric Claw"
                            _G.AutoFarm = true
                        end
                    end
                end
            end
        end
    end)    
end)

Main:AddToggle("Auto Dragon Talon ",_G.AutoDragonTalon,function(value)
    _G.AutoDragonTalon = value
end)

spawn(function()
    while wait() do
        if _G.AutoDragonTalon then
            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Talon") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Talon") then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 400 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    _G.SelectWeapon = "Dragon Talon"
                end  
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 400 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    _G.SelectWeapon = "Dragon Talon"
                end  
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 399 then
                    _G.SelectWeapon = "Dragon Claw"
                end 
            else 
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
            end
        end
    end
end)

Main:AddToggle("Auto Godhuman หาของเอง ",_G.AutoGodhuman,function(value)
    _G.AutoGodhuman = value
end)

FruitList = {
        "Bomb-Bomb",
        "Spike-Spike",
        "Chop-Chop",
        "Spring-Spring",
        "Kilo-Kilo",
        "Spin-Spin",
        "Bird: Falcon",
        "Smoke-Smoke",
        "Flame-Flame",
        "Ice-Ice",
        "Sand-Sand",
        "Dark-Dark",
        "Revive-Revive",
        "Diamond-Diamond",
        "Light-Light",
        "Love-Love",
        "Rubber-Rubber",
        "Barrier-Barrier",
        "Magma-Magma",
        "Door-Door",
        "Quake-Quake",
        "Human-Human: Buddha",
        "String-String",
        "Bird-Bird: Phoenix",
        "Rumble-Rumble",
        "Paw-Paw",
        "Gravity-Gravity",
        "Dough-Dough",
        "Venom-Venom",
        "Shadow-Shadow",
        "Control-Control",
        "Soul-Soul",
        "Dragon-Dragon"
    }
    
    _G.SelectFruit = ""
    DevilFruit:AddDropdown("Select Fruits Sniper",FruitList,function(value)
        _G.SelectFruit = value
    end)
    
    DevilFruit:AddToggle("Auto Buy Fruit Sniper",_G.AutoBuyFruitSniper,function(value)
        _G.AutoBuyFruitSniper = value
    end)
    
   
    
    DevilFruit:AddDropdown("Select Fruits Eat",FruitList,function(value)
        _G.SelectFruitEat = value
    end)
    
    DevilFruit:AddToggle("Auto Eat Fruit",_G.AutoEatFruit,function(value)
        _G.AutoEatFruit = value
    end)
    
    spawn(function()
        pcall(function()
            while wait(.1) do
                if _G.AutoEatFruit then
                    game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat).EatRemote:InvokeServer()
                end
            end
        end)
    end)
    
    DevilFruit:AddToggle("Auto Eat Fruit Hop",_G.AutoEatFruitHop,function(value)
        _G.AutoEatFruitHop = value
    end)
    
    spawn(function()
        pcall(function()
            while wait(.1) do wait(10)
                if _G.AutoEatFruitHop and _G.SelectFruitEat ~= nil then
                    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat) or not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(_G.SelectFruitEat) then
                        Hop()
                    else
                        game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat).EatRemote:InvokeServer()
                    end
                end
            end
        end)
    end)
    
    spawn(function()
        pcall(function()
            while wait(.1) do
                if _G.AutoBuyFruitSniper then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PurchaseRawFruit",_G.SelectFruit)
                end 
            end
        end)
    end)
    
    DevilFruit:AddToggle("Auto Random Fruit",_G.Random_Auto,function(value)
        _G.Random_Auto = value
    end)
    
    spawn(function()
        pcall(function()
            while wait(.1) do
                if _G.Random_Auto then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
                end 
            end
        end)
    end)
    
    DevilFruit:AddButton("Random Fruit",function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
    end)
    
    
    DevilFruit:AddToggle("Auto Drop Fruit",_G.DropFruit,function(value)
        _G.DropFruit = value
    end)
        
    spawn(function()
        while wait() do
            if _G.DropFruit then
                pcall(function()
                    for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
                        if string.find(v.Name, "Fruit") then
                            EquipWeapon(v.Name)
                            wait(.1)
                            if game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible == true then
                                game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible = false
                            end
                            EquipWeapon(v.Name)
                            game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectFruit).EatRemote:InvokeServer("Drop")
                        end
                    end
                for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetChildren()) do
                        if string.find(v.Name, "Fruit") then
                            EquipWeapon(v.Name)
                            wait(.1)
                            if game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible == true then
                                game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible = false
                            end
                            EquipWeapon(v.Name)
                            game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectFruit).EatRemote:InvokeServer("Drop")
                        end
                    end
                end)
            end
        end
    end)
    
    DevilFruit:AddToggle("Auto Store Fruit",_G.AutoStoreFruit,function(value)
        _G.AutoStoreFruit = value
    end)
    
    spawn(function()
        pcall(function()
            while wait(.1) do
                if _G.AutoStoreFruit then
                    for i,v in pairs(FruitList) do
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit",v)
                    end
                end
            end
        end)
    end)
    
    
    DevilFruit:AddToggle("Grab Fruit",_G.BringFruit,function(value)
        _G.BringFruit = value
        pcall(function()
            while _G.BringFruit do wait(.1)
                for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
                    if v:IsA("Tool") then
                        local OldCFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame				
                        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame * CFrame.new(0,0,8)
                        v.Handle.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame
                        wait(.1)
                        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = OldCFrame
                    end
                end
            end
        end)
    end)

spawn(function()
    while task.wait() do
        pcall(function()
            if _G.AutoGodhuman then
                if game.Players.LocalPlayer.Character:FindFirstChild("Godhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Godhuman") then
                    _G.SWeapon = "Godhuman"
                end  
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step") or game.Players.LocalPlayer.Character:FindFirstChild("Death Step") or game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw") or game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw") or game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate") or game.Players.LocalPlayer.Character:FindFirstChild("Sharkman Karate") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Talon") then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step") and game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step").Level.Value <= 399 then
                        _G.SWeapon = "Death Step"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw").Level.Value <= 399 then
                        _G.SWeapon = "Electric Claw"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate").Level.Value <= 399 then
                        _G.SWeapon = "Sharkman Karate"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon").Level.Value <= 399 then
                        _G.SWeapon = "Dragon Claw"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step") and game.Players.LocalPlayer.Backpack:FindFirstChild("Death Step").Level.Value >= 400 or game.Players.LocalPlayer.Character:FindFirstChild("Death Step") and game.Players.LocalPlayer.Character:FindFirstChild("Death Step").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electric Claw").Level.Value >= 400 or game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Electric Claw").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Sharkman Karate").Level.Value >= 400 or game.Players.LocalPlayer.Character:FindFirstChild("Sharkman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Sharkman Karate").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    end 
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Talon").Level.Value >= 400 or game.Players.LocalPlayer.Backpack:Character("Dragon Talon") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Talon").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman")
                    end
                end
            end
        end)
    end
end)

