~~~
static class AppHelper
{
  public static BitmapImage GetBitmapImage(string path)
  {
    BitmapImage bitmap = new BitmapImage();
    bitmap.BeginInit();

    image.CacheOption = BitmapCacheOption.OnLoad;
    bitmap.StreamSource = new MemoryStream(File.ReadAllBytes(path));
    bitmap.EndInit();
    bitmap.Freeze();
    return bitmap;
  }
}
~~~

WPF的BitmapImage的文件无法释放及内存泄露的问题

https://www.cnblogs.com/nio-nio/archive/2011/05/11/2043622.html


