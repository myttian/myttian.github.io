# Vim

[vim-tutor.zh_cn.utf-8 ](https://www.cnblogs.com/birtney/p/17303369.html) [ vimtutor ](https://blog.csdn.net/DucklikeJAVA/article/details/79313168)   [vim复制与粘贴 ](https://www.cnblogs.com/lzping/p/11356356.html) [ vim 复制粘贴](https://blog.csdn.net/weixin_50924918/article/details/123920632)  [runoob](https://www.runoob.com/linux/linux-vim.html)   [键位图](https://www.runoob.com/w3cnote/all-vim-cheatsheat.html)   [vim自动补全](https://blog.csdn.net/lanuage/article/details/125554570)  [Vim命令图解](https://www.jianshu.com/p/91496d2dfe7b)  [ 神级程序员都在用什么工具](https://www.zhihu.com/question/465346075/answer/2907673736)  [Vimdoc ](https://vimdoc.sourceforge.net/)   [Vim documentation](https://vimdoc.sourceforge.net/htmldoc/usr_toc.html)  [gvim](https://www.sohu.com/a/488982435_121124018)  [gvim常用配置](https://www.cnblogs.com/oliver2022/p/16609456.html)  [上古神器Gvim](https://zhuanlan.zhihu.com/p/258490825)  [Vim 清空所有内容](https://www.jianshu.com/p/6e281ef206c3)

#### 三种模式

**命令模式**（Command mode一般模式），**输入模式**（Insert mode编辑）和**底线命令模式（Last line mode）** 可视模式

##### 命令模式

~符号表示没有任何东西

```ts
//移动光标：30j 或 30↓ 下移30行 ；  ^f^b一页；^d^u半页； +-光标移动到非空格符的下一行； n<space>右移n个字符；n<Enter>下移n行； 0$^行最前；HML屏幕(上、中央、下)行的第一个字符； G gg第一行；nG文件第n行 ； 全选ggVG; 全删ggdG  w下个单词 e词尾 b词首； >>缩进； zz zb zt移动光标  段落区块：}下一段，%配对括号查找，]}区块尾 ；   mx标记x，`x跳到标记x；   


//搜索替换：/？上下搜； nN重复搜索； *#搜当前单字  fx行内字符查找； gd跳至当前单字定义位置      『 批量注释：< :起始行号,结束行号s/^/注释符/g 找^替换为注释符>， 取消： < :起始行号,结束行号s/^注释符//g >, 从第一行到最后一行1,$或%， /gc替换前确认 』    CTRL-G文件状态

//复制，粘贴删除： x del向后删1字符；nx删n个字符；dd剪切1行（ndd）；p粘贴到下一行；dw ndw删当前字符; d)删到下句开始，d}删到下段开始；d回车删2行  dG删光标到最后行(d1G)； d$ d0删光标到行首；yl复制字符 yh复制光标前1个字符；yw复制1单词； yy复制当前行，nyy复制n行； y1G yG y0 y$；   ^r重做，u撤销, .重复前一个动作； J上下行合并，c重复删除多个数据，例如向下删除10行，[ 10cj ] ； c更改命令：ce改变文本直到一个单词的末尾，cw改变单词,c$改变到行尾；
```

##### 编辑模式

i光标处I；    a光标下一个字符A；    o下一行O；   R一直替换 ； C修改至行末；  C-v即ctrl+v可视块； s删除字符并插入

##### 底线命令

w!强制保存；  q！ ZQ强退；   wq ZZ保存退出；   w 01另存；  ！ls /home执行ls；   h帮助   x跳至x行；  n新文件； e x编辑文件x； 

##### 可视模式

相当于高亮选取文本后的普通模式，可视模式具有子模式；  gv重新选中上一次选中的部分

**以行为单位进行选取**：V sh+v ； 

**块为单位进行选取**： C-v ； 
