# 前端文档

标签 ： 前端
    <div class="fe" style="background-color:red;width:70px;display:inline-block;margin-right:10px">前端文档</div><span>markdow</span>
   
---
## Markdown语法
***
#### 注意：
代表语法的符号最好与内容之间存在空格,比如*（空格）内容 才能表示列表
***
#### 兼容html：
* 直接输入html语句是可以直接编译的
     <div > this is html show </div>
     <a href="www.baidu.com">链接</a> 
* 特殊字符：< &的输入必须使用http://www.baidu.com/images?num=30&amp;q=bird

#### 标题：
    标题格式通过#，##，###分别代表一级标题、二级标题、三级标题……
***
#### 区块元素：
* 引用
    > 引用：通过>(空格)实现
* 列表
    1  * 代表无序列表
    2  数字代表有序列表
      - [ ] 代表方格
      - [x] 代表选择方格
* 公式
  使用两个美元符号包含
  $$E=mc^2$$
* 图片和链接
    1 图片： ![Mou icon](http://mouapp.com/Mou_128.png)                 //![]内为title，即图片不显示时的提示内容。
    2 链接：[Baidu](http://www.baidu.com)
* 粗体和斜体
  *我们是好朋友*   //通过两个*  *包括的是斜体
  **我们是朋友**   //通过四个**  **包含的是粗体
  3个*表示分割线
* 表格

| 项目 | 价格  |  数量 |
| -------- | -----: | :----: |
| 计算机     | \$1600 |   5     |
| 手机        |   \$12   |   12   |
| 管线        |    \$1    |  234  |
***
#### 高亮代码:
```javascript
var getName=function(name){
    this.name=name;
    return this.name;
}
```
***
#### 目录结构
```
bootstrap
  |----src
  |     |---jquery
  |     |---css  
  |----demo
```  


