~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Diagnostics;
 
namespace ConsoleApplication20
{
    class Program
    {
        public delegate void TestDelegate(string name);
        static void Main(string[] args)
        {
            TestDelegate d = Test;
            Console.WriteLine("Beginning : {0:yyyy-MM-dd HH:mm:ss.fff}", DateTime.Now);
            d.BeginInvoke("小明1", null, null);
            d.BeginInvoke("小明2", null, null);
            d.BeginInvoke("小明3", null, null);
            d.BeginInvoke("小明4", null, null);
            d.BeginInvoke("小明5", null, null);
            Console.WriteLine("End       : {0:yyyy-MM-dd HH:mm:ss.fff}", DateTime.Now);
 
            Console.Read();
        }
 
        static void Test(string name) 
        {
            Console.WriteLine("TestMethod: {0:yyyy-MM-dd HH:mm:ss.fff} {1}", DateTime.Now, name);
        }
    }
}

~~~
