php的crc32调用方法如下
~~~
echo crc32("ABCD");
//3675725989
~~~
C#的crc32函数实现如下
~~~
using System;
using System.IO;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Security.Cryptography;

namespace ConsoleApplication1
{
    class CRC32Cls
    {
        static protected ulong[] Crc32Table;
        //生成CRC32码表
        static public void GetCRC32Table()
        {
            ulong Crc;
            Crc32Table = new ulong[256];
            int i, j;
            for (i = 0; i < 256; i++)
            {
                Crc = (ulong)i;
                for (j = 8; j > 0; j--)
                {
                    if ((Crc & 1) == 1)
                        Crc = (Crc >> 1) ^ 0xEDB88320;
                    else
                        Crc >>= 1;
                }
                Crc32Table[i] = Crc;
            }
        }
        //获取字符串的CRC32校验值
        static public ulong GetCRC32Str(string sInputString)
        {
            //生成码表
            GetCRC32Table();
            byte[] buffer = System.Text.ASCIIEncoding.ASCII.GetBytes(sInputString); ulong value = 0xffffffff;
            int len = buffer.Length;
            for (int i = 0; i < len; i++)
            {
                value = (value >> 8) ^ Crc32Table[(value & 0xFF) ^ buffer[i]];
            }
            return value ^ 0xffffffff;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(CRC32Cls.GetCRC32Str("ABCD"));
            //print 3675725989
        }
    }
}
~~~


-------------------

~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            var hashid = HashHelper.ComputeMD5(@"E:\QQBrowser_Setup_QB10_10026002.exe");

            Console.WriteLine(hashid);
            Console.Read();

        }
    }
    public sealed class HashHelper
    {
        ///<summary>
        ///  计算指定文件的MD5值
        ///</summary>
        /// <paramname="fileName">指定文件的完全限定名称</param>
        ///<returns>返回值的字符串形式</returns>
        public static String ComputeMD5(String fileName)
        {
            String hashMD5 = String.Empty;

            //检查文件是否存在，如果文件存在则进行计算，否则返回空值
            if (System.IO.File.Exists(fileName))
            {
                byte[] data = System.IO.File.ReadAllBytes(fileName);

                
                //计算文件的MD5值
                System.Security.Cryptography.MD5 calculator = System.Security.Cryptography.MD5.Create();
                Byte[] buffer = calculator.ComputeHash(data);

                
                calculator.Clear();

                //将字节数组转换成十六进制的字符串形式
                StringBuilder stringBuilder = new StringBuilder();


                for (int i = 0; i < buffer.Length; i++)
                {
                    stringBuilder.Append(buffer[i].ToString("x2"));
                }
                //stringBuilder.Append(crc16);

                hashMD5 = stringBuilder.ToString();



                var d = CRC32Cls.GetCRC32Str(hashMD5);


            }

            return hashMD5;
        }

    }



    class CRC32Cls
    {
        static protected ulong[] Crc32Table;
        //生成CRC32码表
        static public void GetCRC32Table()
        {
            ulong Crc;
            Crc32Table = new ulong[256];
            int i, j;
            for (i = 0; i < 256; i++)
            {
                Crc = (ulong)i;
                for (j = 8; j > 0; j--)
                {
                    if ((Crc & 1) == 1)
                        Crc = (Crc >> 1) ^ 0xEDB88320;
                    else
                        Crc >>= 1;
                }
                Crc32Table[i] = Crc;
            }
        }
        //获取字符串的CRC32校验值
        static public ulong GetCRC32Str(string sInputString)
        {
            //生成码表
            GetCRC32Table();
            byte[] buffer = System.Text.ASCIIEncoding.ASCII.GetBytes(sInputString); ulong value = 0xffffffff;
            int len = buffer.Length;
            for (int i = 0; i < len; i++)
            {
                value = (value >> 8) ^ Crc32Table[(value & 0xFF) ^ buffer[i]];
            }
            return value ^ 0xffffffff;
        }

        

    }


}

~~~
