# ue4-canvas-gui

It's a simple Canvas GUI for Unreal Engine 4 with mouse operation.

Included elements:
Rendering Text (left/center);<br>
Rendering Rects;<br>
Rendering Circles (filled and not);<br>
Button, Slider, Checkbox, Combobox, Hotkeys and ColorPicker.<br>
<br>
Implemented a simple post-render system to draw on top of menu and all.<br>
<br>
Screenshots with default style:<br>
![EU4 GUI](screenshots/canvas1.jpg "")
 
![EU4 GUI](screenshots/canvas2.jpg "")
 
![EU4 GUI](screenshots/canvas3.jpg "")
 
Ingame render
![EU4 GUI](screenshots/canvas4.jpg "")

Small "How to use" guide:<br>
First you need get UCanvas from game.<br>
After it you can draw with him like this:<br>

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
 if (GetAsyncKeyState(VK_F2) & 1) cfg.menu.enabled = !cfg.menu.enabled;
 
 if (ZeroGUI::Window(crypt("Superior UE4 GUI"), &pos, FVector2D{ 500.0f, 300.0f }, cfg.menu.enabled))
 {
  //Tabs
		if (ZeroGUI::ButtonTab(crypt("Visuals"), FVector2D{ 110, 25 }, tab == 0)) tab = 0;
		if (ZeroGUI::ButtonTab(crypt("Aimbot"), FVector2D{ 110, 25 }, tab == 1)) tab = 1;
		if (ZeroGUI::ButtonTab(crypt("Misc"), FVector2D{ 110, 25 }, tab == 2)) tab = 2;
		if (ZeroGUI::ButtonTab(crypt("Settings"), FVector2D{ 110, 25 }, tab == 3)) tab = 3;
		ZeroGUI::NextColumn(130.0f);
 }
}
```
