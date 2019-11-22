# 使用等宽字体

## 在.emacs文件中加入以下内容：

    (add-to-list 'default-frame-alist
     '(font . "Noto Sans Mono CJK SC-14"))

# 修改几个字符的错误的列计数。

emacs26.3的Fundamental及text mode中，几个unicode字符的列计数是错的。
包括：中文的双引号、破折号、省略号以及×和÷及·符号。
其它一些在屏幕上占用的像素宽度是ascii字符两倍宽度的字符，这里并没有进行修改。
似乎unicode字符库的分类不是很合理，一些双倍宽度的字符和只占一个英文字母宽度的字符混在了一起。这个问题在终端下也很明显，一些两倍宽度的字符需要稍作调整才能正常显示。

## 在.emacs文件中加入以下几行：

    (let ((l '(#x00B7 #x00D7 #x00F7
               (#x2014 . #x2015)
               (#x201C . #x201D) #x2026)))
      (dolist (elt l)
        (set-char-table-range char-width-table elt 2)))

上面几行文本需要放在textmode启用之后。
如果不确定是哪个模式错误地设置了char-width-table,可将上面几行放在文件的结尾。
