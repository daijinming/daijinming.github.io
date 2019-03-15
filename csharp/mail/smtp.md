~~~
        /// <summary>
        /// 发送邮件
        /// </summary>
        /// <param name="smtpServer">SMTP服务器</param>
        /// <param name="hostemail">主邮箱地址</param>
        /// <param name="hostmailpass">主邮箱密码</param>
        /// <param name="emailaddress">邮件接收者地址</param>
        /// <param name="mailcontent">邮件主体内容</param>
        /// <param name="mailtitle">邮件标题</param>
        /// <param name="mailsubject">邮件主题</param>
        /// <returns></returns>
        private bool SendMailBase(string smtpServer, string hostemail, string hostmailpass, string emailaddress, string mailsubject, string mailcontent, string file)
        {
            try
            {
                WebRequest webreq = WebRequest.Create(file);
                WebResponse webres = webreq.GetResponse();

                using (Stream stream = webres.GetResponseStream())
                {
                    System.Net.Mime.ContentType contentType = new System.Net.Mime.ContentType();
                    contentType.MediaType = "application/pdf";

                    Attachment attachment = new Attachment(stream, contentType);

                    MailMessage onemail = new MailMessage();
                    string myEmail = hostemail; //发送邮件的邮箱地址
                    string myPwd = hostmailpass; //发送邮件的邮箱密码
                    onemail.BodyEncoding = System.Text.Encoding.UTF8;
                    onemail.IsBodyHtml = false;
                    onemail.From = new MailAddress(myEmail);
                    onemail.To.Add(new MailAddress(emailaddress));
                    onemail.Subject = mailsubject;
                    onemail.Body = mailcontent;

                    onemail.Attachments.Add(attachment);

                    SmtpClient clint = new SmtpClient(smtpServer);//发送邮件的服务器
                    clint.UseDefaultCredentials = false;
                    clint.Credentials = new System.Net.NetworkCredential(myEmail, myPwd);
                    clint.DeliveryMethod = SmtpDeliveryMethod.Network;

                    clint.Send(onemail);

                }

                return true;
            }
            catch (Exception Ex)
            {
                LogHelper.WriteLog("发送邮件失败", Ex);

                return false;
            }
        }
  ~~~
