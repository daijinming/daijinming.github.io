~~~
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using Nancy.Conventions;
using Nancy;
using Nancy.Responses.Negotiation;
using System.Text;
using System.IO;
using Nancy.Responses;

namespace BeetHead
{
    public class CustomBoostrapper : DefaultNancyBootstrapper
    {

        protected override void ApplicationStartup(Nancy.TinyIoc.TinyIoCContainer container, Nancy.Bootstrapper.IPipelines pipelines)
        {
            base.ApplicationStartup(container, pipelines);


            pipelines.OnError.AddItemToEndOfPipeline(OnErrorWrapInErrorEnvelope);                 
        }
        
        private static dynamic OnErrorWrapInErrorEnvelope(NancyContext context, Exception exception)
        {
            if (context.Response.StatusCode == HttpStatusCode.NotFound)
            {

                return new Response()
               {
                  StatusCode = HttpStatusCode.OK,
                  ContentType = "text/html",
                  Contents = (stream) =>
                  {
                      var errorMessage = Encoding.UTF8.GetBytes("hello 404");
                      stream.Write(errorMessage, 0, errorMessage.Length);
                  }
               };
                
            }
            return null;
        }

        public string[] extentions = new string[] { ".html",".html",".js",".css",".jpg",".gif",".png" };

        protected override void ConfigureConventions(NancyConventions nancyConventions)
        {
            base.ConfigureConventions(nancyConventions);
            
            nancyConventions.StaticContentsConventions.Add(
            StaticContentConventionBuilder.AddDirectory("/", @"wwwroot")
            );

            nancyConventions.StaticContentsConventions.Add((ctx, root) =>
            {
                string fileName;
                string path = ctx.Request.Path.ToLower();

                if (path.Contains("_") && extentions.Where(q=>path.EndsWith(q)).Count() == 0)
                {
                    var localPath = Path.Combine("wwwroot", path.Replace("/","").Replace("\\",""));

                    //return compressed version of vendor.js (as vendor.js.gz)
                    fileName = Path.GetFullPath(Path.Combine(root, localPath,"index.html"));

                    if (File.Exists(fileName) == false)
                        fileName = Path.GetFullPath(Path.Combine(root, localPath, "default.html"));

                    if (File.Exists(fileName))
                    {   
                        var response = new GenericFileResponse(fileName, ctx);
                        //response.Headers.Add("Content-Encoding", "gzip");
                        response.Headers.Add("Content-Type", "text/html");
                        return response;
                    }
                }
                                              
                return null;
            });


        }

    }
}
~
