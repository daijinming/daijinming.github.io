            ~~~
            string cookieStr = webBrowser1.Document.Cookie;


            //MessageBox.Show(cookieStr);


            var body = webBrowser1.Document.Body.InnerHtml;

            Regex reg = new Regex("token: '(.*?)'");
            //例如我想提取记录中的NAME值
            Match match = reg.Match(body);
            string value = match.Groups[1].Value;
            MessageBox.Show(value);

            reg = new Regex("window.gtk = '(.*?)';");
            //例如我想提取记录中的NAME值
             match = reg.Match(body);
             value = match.Groups[1].Value;
            MessageBox.Show(value);
            
            ~~~
