TabControl
~~~
<Window x:Class="TitleControl.tabItem" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" Title="tabItem" Height="300" Width="300">
	<Grid>
		<TabControl Margin="5" TabStripPlacement="Bottom">
			<TabItem Header="TabItem1" Name="TabItem1">
				<StackPanel Margin="3">
					<CheckBox Content="CheckBox0" Margin="3" />
					<CheckBox aContent="CheckBox1" Margin="3" />
					<Button Content="切换选项卡" Height="100" Width="75" Click="Button_Click" /></StackPanel>
			</TabItem>
			<TabItem Header="TabItem2" Name="TabItem2">
				<Grid Background="#FFE5E5E5">
					<TextBlock Margin="3" Text="选项卡2" VerticalAlignment="Top" /></Grid>
			</TabItem>
		</TabControl>
	</Grid>
</Window>
~~~
TabControl 设置选项卡，TabStripPlacement属性默认为Top，这个属性表示选项的位置，TabItem1和TabItem2的位置。TabItem表示选项卡，里面可进行容器嵌套。 这里我还设置了一个切换选项卡的Button,代码如下供参考。
