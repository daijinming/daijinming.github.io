#[首页](https://booksos.cn)

- WPF悬浮窗口 
https://download.csdn.net/download/ivanleegood1314/3939777

- 关键字 悬浮层

- Using XAML Popup In WPF
https://www.c-sharpcorner.com/UploadFile/mahesh/using-xaml-popup-in-wpf/

- Popup in WPF
https://www.codeproject.com/Tips/718302/Popup-in-WPF

- Understanding WPF popups
https://dzone.com/articles/understanding-wpf-popups


- Drag WPF Popup control
https://stackoverflow.com/questions/222029/drag-wpf-popup-control
>the WPF Popup control is nice, but somewhat limited in my opinion. is there a way to "drag" a popup around when it is opened (like with the DragMove() method of windows)?

>Here's a simple solution using a Thumb.
Subclass Popup in XAML and codebehind
Add a Thumb with width/height set to 0 (this could also be done in XAML)
Listen for MouseDown events on the Popup and raise the same event on the Thumb
Move popup on DragDelta
XAML:
~~~
<Popup x:Class="PopupTest.DraggablePopup" ...>
    <Canvas x:Name="ContentCanvas">

    </Canvas>
</Popup>
~~~
C#:
~~~
public partial class DraggablePopup : Popup 
{
    public DraggablePopup()
    {
        var thumb = new Thumb
        {
            Width = 0,
            Height = 0,
        };
        ContentCanvas.Children.Add(thumb);

        MouseDown += (sender, e) =>
        {
            thumb.RaiseEvent(e);
        };

        thumb.DragDelta += (sender, e) =>
        {
            HorizontalOffset += e.HorizontalChange;
            VerticalOffset += e.VerticalChange;
        };
    }
}
~~~

- Draggable Popup
https://www.codeproject.com/Tips/1162455/Draggable-Popup


- Popup Placement Behavior

https://docs.microsoft.com/en-us/dotnet/framework/wpf/controls/popup-placement-behavior
