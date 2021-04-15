# ue4-canvas-gui

## It's a simple Canvas GUI for Unreal Engine 4 with mouse operation.

Included elements:<br>
Rendering Text (left/center);<br>
Rendering Rects;<br>
Rendering Circles (filled and not);<br>
Button, Slider, Checkbox, Combobox, Hotkeys and ColorPicker.<br>
<br>
Implemented a simple post-render system to draw on top of menu and all.<br>
<br>
## Screenshots with default style:<br>
![EU4 GUI](screenshots/canvas1.jpg "")
 
![EU4 GUI](screenshots/canvas2.jpg "")
 
![EU4 GUI](screenshots/canvas3.jpg "")
 
Ingame render
![EU4 GUI](screenshots/canvas4.jpg "")

## Small "How to use" guide:<br>
First you need get **UCanvas** from game.<br>
After it you can draw like this:<br>

```cpp
//I'll show you with an example Post Render Hook
void PostRenderHook(UGameViewportClient* viewport, UCanvas* canvas)
{
	ZeroGUI::SetupCanvas(canvas);
	Menu::Tick();
}

//Menu.h
void Tick()
{
	ZeroGUI::Input::Handle();
	
	static bool menu_opened = false;
	if (GetAsyncKeyState(VK_F2) & 1) menu_opened = !menu_opened; //Our menu key

	if (ZeroGUI::Window("Superior UE4 GUI", &pos, FVector2D{ 500.0f, 300.0f }, menu_opened))
	{
		//Simple Tabs
		static int tab = 0;
		if (ZeroGUI::ButtonTab("Tab 1", FVector2D{ 110, 25 }, tab == 0)) tab = 0;
		if (ZeroGUI::ButtonTab("Tab 2", FVector2D{ 110, 25 }, tab == 1)) tab = 1;
		if (ZeroGUI::ButtonTab("Tab 3", FVector2D{ 110, 25 }, tab == 2)) tab = 2;
		if (ZeroGUI::ButtonTab("Tab 4", FVector2D{ 110, 25 }, tab == 3)) tab = 3;
		ZeroGUI::NextColumn(130.0f);
		//
		
		//Some Elements
		static bool text_check = false;
		static float text_slider = 15.0f;
		static int test_hotkey = 0;
		static FLinearColor test_color{ 0.0f, 0.0f, 1.0f, 1.0f };
		
		ZeroGUI::Checkbox("Test Checkbox", &text_check);
		ZeroGUI::SliderFloat("Test Slider", &text_slider, 0.0f, 180.0f);
		ZeroGUI::Hotkey("Test Hotkey", FVector2D{ 80, 25 }, &test_hotkey);
		
		//Element with padding
		ZeroGUI::PushNextElementY(Menu::pos.Y + 50.0f);
		ZeroGUI::Combobox("Combobox", FVector2D{ 100, 25 }, &test_number, "None", "First", "Second", "Third", NULL); //NULL at end is required!
		ZeroGUI::SameLine();//inline items
		if (ZeroGUI::Button("It's a Button!", FVector2D{ 100, 25 })) { //clicked! }
		
		//Color Picker
		ZeroGUI::ColorPicker("Color Picker", &test_color);
	}
	ZeroGUI::Render();//Custom Render. I use it for drawing Combobox and ColorPicker over the menu
	ZeroGUI::Draw_Cursor(menu_opened);
}
```
