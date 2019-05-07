~~~
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Runtime.InteropServices;
using System.Text;
using System.Windows.Forms;

namespace WindowsFormsApplication1
{
    public partial class Form1 : Form
    {
        [DllImport("user32", EntryPoint = "FindWindow")]
        private static extern IntPtr FindWindow(string lpClassName, string lpWindowName);

        [DllImport("user32.dll", EntryPoint = "FindWindowEx")]
        private static extern IntPtr FindWindowEx(IntPtr hwndParent, IntPtr hwndChildAfter, string lpszClass, string lpszWindow);

        [DllImport("User32.dll", EntryPoint = "SendMessage")]
        private static extern void SendMessage(IntPtr hWnd, int Msg, IntPtr wParam, int lParam);

        //根据坐标获取窗口句柄
        [DllImport("user32")]
        public static extern IntPtr WindowFromPoint(
        Point Point  //坐标
        );


        private const int WM_CLOSE = 0x10;//关闭
        private const int BM_CLICK = 0xF5;//点击


        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {

            MessageBox.Show("Hello windows");
        }

        private void Form1_Load(object sender, EventArgs e)
        {

            textBox1.Text = button1.Handle.ToInt64().ToString() + "-" + this.Handle.ToInt64();

        }

        private void button2_Click(object sender, EventArgs e)
        {
            
            /*
            IntPtr childHwnd = FindWindowEx(this.Handle, IntPtr.Zero, null, "button1");
            if (childHwnd != IntPtr.Zero)
            {
                //模拟点击 是(&Y)
                SendMessage(childHwnd, BM_CLICK, IntPtr.Zero, 0);
            }
            */


            IntPtr win = WindowFromPoint(this.PointToScreen(button1.Location));
            
            SendMessage(win, BM_CLICK, IntPtr.Zero, 0);
        }

        


    }
}
~~~
---------------------
根据窗体的Caption和Class获取窗体的句柄  
https://blog.csdn.net/elrphant/article/details/7231754

