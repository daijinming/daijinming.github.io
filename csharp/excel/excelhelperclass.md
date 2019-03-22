~~~
using System;
using System.Collections.Generic;
using System.Data;
using System.Reflection;
using System.Text.RegularExpressions;

namespace BHOaAPI._base
{
    public class DataTableHelper
    {
        //用于excel表格中列号字转成数字，返回的列号索引从1开始
        public static int ToIndex(string columnName)
        {
            if (!Regex.IsMatch(columnName.ToUpper(), @"[A-Z]+"))
                throw new Exception("Invalid parameter");

            var index = 0;
            var chars = columnName.ToUpper().ToCharArray();
            for (var i = 0; i < chars.Length; i++)
                index += (chars[i] - 'A' + 1) * (int) Math.Pow(26, chars.Length - i - 1);
            return index;
        }

        //用于将数字转成excel表格中列号字母，返回的列号索引从A开始，从A对应1开始
        public static string ToName(int index)
        {
            if (index <= 0)
                throw new Exception("invaild parameter");

            index--;
            var chars = new List<string>();
            do
            {
                if (chars.Count > 0)
                    index--;
                chars.Insert(0, ((char) (index % 26 + 'A')).ToString());
                index = (index - index % 26) / 26;
            } while (index > 0);

            return string.Join(string.Empty, chars.ToArray());
        }

        /// <summary>
        ///     Convert a List{T} to a DataTable.
        /// </summary>
        public static DataTable ToDataTable<T>(T[] items)
        {
            var tb = new DataTable(typeof(T).Name);

            var props = typeof(T).GetFields(BindingFlags.Public | BindingFlags.Instance);

            foreach (var prop in props)
            {
                var t = GetCoreType(prop.FieldType);
                tb.Columns.Add(prop.Name, t);
            }

            foreach (var item in items)
            {
                var values = new object[props.Length];

                for (var i = 0; i < props.Length; i++) values[i] = props[i].GetValue(item);

                tb.Rows.Add(values);
            }

            return tb;
        }

        /// <summary>
        ///     Determine of specified type is nullable
        /// </summary>
        public static bool IsNullable(Type t)
        {
            return !t.IsValueType || t.IsGenericType && t.GetGenericTypeDefinition() == typeof(Nullable<>);
        }

        /// <summary>
        ///     Return underlying type if type is Nullable otherwise return the type
        /// </summary>
        public static Type GetCoreType(Type t)
        {
            if (t != null && IsNullable(t))
            {
                if (!t.IsValueType)
                    return t;
                return Nullable.GetUnderlyingType(t);
            }

            return t;
        }
    }
}
~
