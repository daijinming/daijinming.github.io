
~~~
<script>
    
	var $form = null;
    
	$(function () {
		
		
         $form = $('#fileupload').fileupload({
            dataType: 'json',
			/*xhrFields: {withCredentials: true},*/
			complete: function (e, data) {
			   //code for done uploading callback
			   console.log(e.responseJSON);
			}
        });
		
    });
	
    $('#fileupload').addClass('fileupload-processing');

</script>


<form id="fileupload" method="POST" enctype="multipart/form-data" data-url="http://remote.com/FileUpload/Upload">
    
</form>
//data-url 修改为要提交的跨域网站上传服务地址

~~~

#参考：
https://github.com/blueimp/jQuery-File-Upload
https://github.com/TheKalin/jQuery-File-Upload.MVC5
