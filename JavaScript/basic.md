# 导入JavaScript
- 内置
```html
<script type="text/javascript">
    function doDel(id){
        if(confirm("Are you sure to del?")){
            window.location = 'action.php?action=del&id='+id;
        }
    }
</script>
```
- 外部文件
```html
<script type="text/javascript" src="01.js"></script>
```
- 内嵌
```html
<input name="btn" type="button" value="弹出消息框" onclick="javascript:alert('欢迎你');"/>
```
