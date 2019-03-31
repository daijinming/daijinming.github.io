方法一：
document.onkeydown = function (e) { // 回车提交表单
// 兼容FF和IE和Opera
    var theEvent = window.event || e;
    var code = theEvent.keyCode || theEvent.which || theEvent.charCode;
    if (code == 13) {
        queryInfo();
    }
}

方法二:
JS监听某个DIV区域
$("#queryTable").bind("keydown",function(e){
　　// 兼容FF和IE和Opera
　　var theEvent = e || window.event;
　　var code = theEvent.keyCode || theEvent.which || theEvent.charCode;
　　 if (code == 13) {
　　//回车执行查询
　　$("#queryButton").click();
　　}
});
JS监听某个输入框
//回车事件绑定
$('#search_input').bind('keyup', function(event) {
　　if (event.keyCode == "13") {
　　　　//回车执行查询
　　　　$('#search_button').click();
　　}
});
