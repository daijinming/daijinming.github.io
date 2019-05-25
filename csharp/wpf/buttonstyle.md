写自己的WPF样式 - 按钮

https://www.cnblogs.com/xinwang/p/4354182.html

~~~
<Application x:Class="WPFCustomerStyleStudy.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <!--自定义颜色-->
        <LinearGradientBrush x:Key="LinearGradientBlueBackground" EndPoint="0.5,1" StartPoint="0.5,0">
            <GradientStop Color="#FF377FED" Offset="0" />
            <GradientStop Color="#FF074CC0" Offset="1" />
        </LinearGradientBrush>
        <Color x:Key="MyBtnBorderColor">#FF2D78F4</Color>
        <!--END-->
        
        <Style x:Key="MyWpfButton" TargetType="{x:Type Button}" >
            <Setter Property="Background" Value="{StaticResource LinearGradientBlueBackground}"></Setter>
            <Setter Property="Foreground" Value="White"></Setter>
            <Setter Property="BorderBrush" Value="{StaticResource MyBtnBorderColor}"></Setter>
        </Style>
    </Application.Resources>
</Application>
~~~
