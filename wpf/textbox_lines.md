WPF中没有textarea的东西，不像在ASP.NET中设置textbox那样设置一个多行属性就可以变成文本域，虽然可以使用ricktextbox实现多行文本输入，但是richtextbox比较复杂，面对简单的多行文本输入的时候太麻烦了点，但是WPF的textbox依然可以通过设置属性实现像textarea一样的多行文本输入。
本示例演示如何使用可扩展应用程序标记语言 (XAML) 定义一个 TextBox 控件，该控件将自动扩展以容纳多行文本。

  示例 
将 TextWrapping 属性设置为 Wrap 会导致输入的文本在到达 TextBox 控件的边缘时换至新行，必要时会自动扩展 TextBox 控件以便为新行留出空间。

将 AcceptsReturn 属性设置为 true 会导致在按 Return 键时插入新行，必要时会再次自动扩展 TextBox 以便为新行留出空间。

VerticalScrollBarVisibility 属性向 TextBox 添加一个滚动条，以便在 TextBox 超出包含它的框架或窗口的大小时，可以滚动 TextBox 的内容。
~~~
<TextBox
  Name="tbMultiLine"
  TextWrapping="Wrap"
  AcceptsReturn="True"
  VerticalScrollBarVisibility="Visible"
>
  This TextBox will allow the user to enter multiple lines of text.  When the RETURN key is pressed, 
  or when typed text reaches the edge of the text box, a new line is automatically inserted.
</TextBox>
~~~

