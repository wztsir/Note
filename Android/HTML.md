## HTML



## CSS

### 表格

```CSS
<style>
table.t1{
  table-layout:automatic;
}
<!---->
table.t2{
  table-layout:fixed;
}

</style>

<table class="t1" border="1" width="100%">
    <tr>
        <!--选择器里选择的自动适配，无论第一个格子的width选择多少，都不会挤掉内容，过大的化就会有留白-->
        <td width="10%">abcdefghijklmnopqrstuvwxyz</td>
        <td width="90%">abc</td>
    </tr>
</table>

<table class="t2" border="1" width="100%">
    <tr>
        <td width="50px">abcdefghijklmnopqrstuvwxyz</td>
        <td >abc</td>
    </tr>
</table>
```

### 边框

```CSS
<style>
 div.biankuang{
<!-- width描述字体框的长，height描述字体框的高-->
   width:50px;
   height:50px;
<!--描述边框的宽，其长度默认同字体框一样-->
   border-top-style:solid;
   border-top-color:red;
   border-top-width: 50px;
   background-color:lightgray;
  }
</style>

<div class="biankuang">
    只有上面有边框
</div>
```

### 显示方法

内联是不换行，但是不能指定大小
块级时能指定大小，但是会换行