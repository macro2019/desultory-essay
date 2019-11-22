# 使用等宽字体

(add-to-list 'default-frame-alist
 '(font . "Noto Sans Mono CJK SC-14"))

# 修改一些中文标点符号和unicode字符的错误的列计数。

emacs26.3的Fundamental及text mode中，几个中文标点符号和unicode符号的列计数是错的。
包括：中文的双引号、破折号、省略号以及unicode的×和÷及·符号。
还有其它一些在屏幕上占用的像素宽度是ascii字符两倍宽度的字符，这里并没做修改。
似乎unicode字符库的分类不是很合理，一些双倍宽度的字符和更窄的字符混在了一起。

## 在.emacs文件中加入下列几行：

(let ((l '(#x00B7 #x00D7 #x00F7
           (#x2014 . #x2015)
           (#x201C . #x201D) #x2026)))
  (dolist (elt l)
    (set-char-table-range char-width-table elt 2)))

上面几行文本需要放在textmode启用之后。
如果不确定是哪个模式设置了错误的char-width-table,可将上面几行放在文件的结尾。
