~~~
/// <summary>
        /// 上传文件
        /// </summary>
        /// <param name="uriStr">服务器网址</param>
        /// <param name="name">http报文头中name</param>
        /// <param name="fileName">文件名</param>
        /// <param name="data">文件数据</param>
        /// <param name="offset">文件数据起始位置</param>
        /// <param name="count">文件数据长度</param>
        /// <returns></returns>
static public string Upload(string uriStr, string name, string fileName, byte[] data, int offset, int count)
        {
            try
            {
                var request = WebRequest.Create(uriStr);
                request.Method = "POST";
                var boundary = $"******{DateTime.Now.Ticks}***";
                request.ContentType = $"multipart/form-data; boundary={boundary}";
                boundary = $"--{boundary}";
                using (var requestStream = request.GetRequestStream())
                {
                    var buffer = Encoding.ASCII.GetBytes(boundary + Environment.NewLine);
                    requestStream.Write(buffer, 0, buffer.Length);
                    buffer = Encoding.ASCII.GetBytes($"Content-Disposition: form-data; name=\"{name}\"; filename=\"{fileName}\"{Environment.NewLine}");
                    requestStream.Write(buffer, 0, buffer.Length);
                    buffer = Encoding.ASCII.GetBytes($"Content-Type: application/octet-stream{Environment.NewLine}{Environment.NewLine}");
                    requestStream.Write(buffer, 0, buffer.Length);
                    requestStream.Write(data, offset, count);
                    buffer = Encoding.ASCII.GetBytes($"{Environment.NewLine}{boundary}--");
                    requestStream.Write(buffer, 0, buffer.Length);
                }
                using (var response = request.GetResponse())
                using (var responseStream = response.GetResponseStream())
                using (var streamReader = new StreamReader(responseStream))
                {
                    return streamReader.ReadToEnd();
                }
            }
            catch
            {
                return null;
            }
        }
        ~~~
