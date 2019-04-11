 - c# 获得一个程序的窗口句柄，并且修改它的标题
 
https://zhidao.baidu.com/question/1704056559628380220.html
 
~~~
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Text;
using System.Runtime.InteropServices; 

namespace WindowsFormsApplication2
{
    static class Program
    {
        [DllImport("user32.dll", EntryPoint = "FindWindowA", CharSet = CharSet.Ansi)]
        public static extern int FindWindow(string lpClassName, string lpWindowName);

        [DllImport("user32.dll", EntryPoint = "SetWindowText", CharSet = CharSet.Ansi)]
        public static extern int SetWindowText(int hwnd, string lpString);

        [DllImport("user32.dll")]
        public static extern bool SetForegroundWindow(int hWnd);
        static Int32 Run()
        {
            Process myProcess = new Process();
            myProcess.StartInfo.UseShellExecute = false;
            myProcess.StartInfo.FileName = "calc.exe";
            myProcess.StartInfo.CreateNoWindow = true;
            myProcess.Start();
            myProcess.WaitForExit(2000);

            return myProcess.Id;
        }

        /// <summary>
        /// 应用程序的主入口点。
        /// </summary>
        [STAThread]
        static void Main()
        {
            Run();
            int lHwnd = FindWindow(null, "计算器");

            SetWindowText(lHwnd, "我的计算器");

            SetForegroundWindow(lHwnd);
        }
    }
}

~~~
