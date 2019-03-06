# WPF GridSplitter上下左右拖动
~~~
<Window x:Class="testGridSplitter.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <Grid.RowDefinitions >
            <RowDefinition Height="60" MinHeight="60"/>
            <RowDefinition MinHeight="60"/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="100" MinWidth="60" MaxWidth="400"/>
            <ColumnDefinition MinWidth="60"/>
        </Grid.ColumnDefinitions>
        
　　　　 <GridSplitter Width="5" Grid.Row="0" Grid.RowSpan="2" Grid.Column="0" Background="Gray"  HorizontalAlignment="Right"/>
　　　　 <GridSplitter Height="5" Grid.Row="0" Grid.Column="1" Background="Gray" HorizontalAlignment="Stretch" VerticalAlignment="Bottom"/>

    </Grid>
</Window>
~~~
