---
title: 我的AutoHotKey配置
date: 2016-05-21 18:09:37
tags:
- AutoHotKey
---

## 摘要：
主要内容：
本文介绍了个人的AutoHotKey配置，包括它的便利性、用法说明等。在文章最后提供配置代码；

<!--more-->

## 简单介绍
当我产生了这样的想法时，我找到了`Autohotkey`:
```
只要是可以编辑的地方，都用同一套规则（例如VIM）控制光标。
```

**使用Autohotkey带来其他便利：**
``` 
* 一次按键，在浏览器中用指定搜索引擎搜索选中的文字（同样可以搜索剪切板的内容）。
* 一次按键，打开指定的某一个软件或同时打开几个软件。
* 一次按键，可以输入自定义的模板：例如输入`/mail`，就能达到输入`example@example.com`的效果。
* 一次按键，快速输入特殊符号（●、★、×、√ 等等）。
```

**软件下载地址**
```
https://autohotkey.com
```

（PS：配置规则源于VIM，如果你也是VIM爱好者，相信你很快就可以上手。）

## 举例说明

**光标控制1**
```
* 光标左移一次：Alt+h
* 光标右移一次：Alt+l
* 光标上移一次：Alt+,
* 光标下移一次：Alt+i
```

**光标控制2**
``` 
* 光标置于行首：Alt+0
* 光标置于行尾：Alt+4
* 选中光标位置到行首的文字：Shift+Alt+0
* 选中光标位置到行尾的文字：Shift+Alt+4
* 删除右侧一个字符（同`Delete`按键）：Alt+'
* 删除当前行内容：Shift+Ctrl+k
* 无论光标在当前行何处，新起一行：Shift+Enter
```

**搜索**
```
* 选中文字，用谷歌搜索：win+alt+g
* 选中文字，用百度搜索：win+alt+b
```

**打开软件或网址**
```
* 在浏览器中打开谷歌日历：win+c
* 同时打开多个软件：win+a
* 锁定电脑并关闭显示器：win+l
* 切换鼠标左右键：win+alt+q
```

**切换导航标签**（例如chrome，Firefox，eclipse等等含有tab的应用）：
```
* 下一个标签：Alt+k
* 上一个标签：Alt+j
```

**控制窗口**
```
* 按住alt键，左键拖拽窗口任意地方可以移动窗口；（非最大化模式）
* 按住alt键，右键拖拽窗口，可以调整窗口的对象；（非最大化模式）
```

## 配置代码
```
;====== Lou BEG ======
;说明
;文中符号说明, 有组合键共同打造不一样
;[!]    等价于按键[Alt]
;[+]    等价于按键[Shift]
;[#]    等价于按键[Windows]
;[^]    等价于按键[Ctrl]
;====== Lou END ======

;====== Lou BEG ======
; 移动窗口
;(alt + 鼠标左键：移动窗口；注意，窗口处于最大化的情况下将不可移动)
;(alt + 鼠标右键：调整窗口大小；注意，窗口处于最大化的情况下将不可改变)
SetWinDelay,2
CoordMode,Mouse

!LButton::
If DoubleAlt
{
    MouseGetPos,,,KDE_id
    PostMessage,0x112,0xf020,,,ahk_id %KDE_id%
    DoubleAlt := false
    return
}
MouseGetPos,KDE_X1,KDE_Y1,KDE_id
WinGet,KDE_Win,MinMax,ahk_id %KDE_id%
If KDE_Win
    return
WinGetPos,KDE_WinX1,KDE_WinY1,,,ahk_id %KDE_id%
WinActivate,ahk_id %KDE_id%
Loop
{
    GetKeyState,KDE_Button,LButton,P ; Break if button has been released.
    If KDE_Button = U
        break
    MouseGetPos,KDE_X2,KDE_Y2 ; Get the current mouse position.
    KDE_X2 -= KDE_X1 ; Obtain an offset from the initial mouse position.
    KDE_Y2 -= KDE_Y1
    KDE_WinX2 := (KDE_WinX1 + KDE_X2) ; Apply this offset to the window position.
    KDE_WinY2 := (KDE_WinY1 + KDE_Y2)
    WinMove,ahk_id %KDE_id%,,%KDE_WinX2%,%KDE_WinY2% ; Move the window to the new position.
}
return

!RButton::
If DoubleAlt
{
    MouseGetPos,,,KDE_id
    ; Toggle between maximized and restored state.
    WinGet,KDE_Win,MinMax,ahk_id %KDE_id%
    If KDE_Win
        WinRestore,ahk_id %KDE_id%
    Else
        WinMaximize,ahk_id %KDE_id%
    DoubleAlt := false
    return
}
; Get the initial mouse position and window id, and
; abort if the window is maximized.
MouseGetPos,KDE_X1,KDE_Y1,KDE_id
WinGet,KDE_Win,MinMax,ahk_id %KDE_id%
If KDE_Win
    return
; Get the initial window position and size.
WinGetPos,KDE_WinX1,KDE_WinY1,KDE_WinW,KDE_WinH,ahk_id %KDE_id%
; Define the window region the mouse is currently in.
; The four regions are Up and Left, Up and Right, Down and Left, Down and Right.
If (KDE_X1 < KDE_WinX1 + KDE_WinW / 2)
   KDE_WinLeft := 1
Else
   KDE_WinLeft := -1
If (KDE_Y1 < KDE_WinY1 + KDE_WinH / 2)
   KDE_WinUp := 1
Else
   KDE_WinUp := -1
Loop
{
    GetKeyState,KDE_Button,RButton,P ; Break if button has been released.
    If KDE_Button = U
        break
    MouseGetPos,KDE_X2,KDE_Y2 ; Get the current mouse position.
    ; Get the current window position and size.
    WinGetPos,KDE_WinX1,KDE_WinY1,KDE_WinW,KDE_WinH,ahk_id %KDE_id%
    KDE_X2 -= KDE_X1 ; Obtain an offset from the initial mouse position.
    KDE_Y2 -= KDE_Y1
    ; Then, act according to the defined region.
    WinMove,ahk_id %KDE_id%,, KDE_WinX1 + (KDE_WinLeft+1)/2*KDE_X2  ; X of resized window
                            , KDE_WinY1 +   (KDE_WinUp+1)/2*KDE_Y2  ; Y of resized window
                            , KDE_WinW  -     KDE_WinLeft  *KDE_X2  ; W of resized window
                            , KDE_WinH  -       KDE_WinUp  *KDE_Y2  ; H of resized window
    KDE_X1 := (KDE_X2 + KDE_X1) ; Reset the initial position for the next iteration.
    KDE_Y1 := (KDE_Y2 + KDE_Y1)
}
return


; "Alt + MButton" may be simpler, but I
; like an extra measure of security for
; an operation like this.
!MButton::
    MouseGetPos,,,KDE_id
    WinClose,ahk_id %KDE_id%
return

; This detects "double-clicks" of the alt key.
~Alt::
DoubleAlt := A_PriorHotKey = "~Alt" AND A_TimeSincePriorHotkey < 400
Sleep 0
KeyWait Alt  ; This prevents the keyboard's auto-repeat feature from interfering.
return
;====== Lou END ======


;====== Lou BEG ======
;取当前鼠标下的屏幕颜色值
!+F9::
MouseGetPos, mouseX, mouseY
PixelGetColor, color, %mouseX%, %mouseY%, RGB
StringRight color,color,6
clipboard = %color%
tooltip, Color: %clipboard%
sleep 2000
tooltip,
return
;====== Lou END ======

#Persistent
#SingleInstance Force
;#NoTrayIcon
#NoEnv


;=============================win系列===================================
; 启动指定的bat文件（可以在bat文件中启动其他程序）

#a::run win_a
#c::run win_c
#n::run win_n
#o::run win_o
#s::run win_s
#v::run win_v
#w::run win_w
#y::run win_y
#z::run win_z
;=============================win系列===================================

;=============================win_alt系列===================================
#!c::run win_alt_c
#!h::run win_alt_h
#!s::run win_alt_s
#!x::run win_alt_x
;=============================win_alt系列===================================




;=============================aa系列===================================

;====== Lou BEG ======
;for android
::aalog::
clipboard = Ulog.i("");
send ^v
send {left}{left}{left}
return

::aaid::
clipboard = android:id="@+id/"
send ^v
send {left}
return

::aatag::
clipboard = public static final String TAG = "";
send ^v
return ;

::aalay::  
d = android:layout_width="match_parent"
clipboard = %d%
Send ^v{enter}
e = android:layout_height="wrap_content"
clipboard = %e%
Send ^v
return



;====== Lou END ======
;=============================aa系列===================================

;=============================jj系列===================================
;====== Lou BEG ======
;输入我的分隔符
::jjl::
d = ====== Lou BEG ======
e = ====== Lou END ======
clipboard = %d%
Send ^v{enter}
clipboard = %e%
Send ^v{up}{enter}
return

::jjs::
d = // --------------------
clipboard = %d%
Send ^v{enter}
e = // ~~~~~~~~~~~~~~~~~~~~
clipboard = %e%
Send ^v{up}{enter}{left}
return

::jjss::
d = // --------------------
clipboard = %d%
Send ^v{enter}
return

::jjse::
e = // ~~~~~~~~~~~~~~~~~~~~
clipboard = %e%
Send ^v{enter}
return

;输入邮箱
::jjm::
clipboard = lyloou@qq.com
Send ^v
return
;====== Lou END ======

;====== Lou BEG ======
;时间输入
;如：14:19:59
::jjt:: 
d = %A_Hour%:%A_Min%:%A_Sec%
clipboard = %d%  
Send ^v  
return
;如：2016.01.16
::jjd::
d = %A_YYYY%.%A_MM%.%A_DD%
clipboard = %d%  
Send ^v  
return
;如：2016-05-08 17:09:10
::jjdt::
d = %A_YYYY%-%A_MM%-%A_DD% %A_Hour%:%A_Min%:%A_Sec%
clipboard = %d%  
Send ^v  
return
;====== Lou END ======


;====== Lou BEG ======
::jj0::
clipboard = ☆☆☆☆☆
send ^v
return
::jj1::
clipboard = ★☆☆☆☆
send ^v
return
::jj2::
clipboard = ★★☆☆☆
send ^v
return
::jj3::
clipboard = ★★★☆☆
send ^v
return
::jj4::
clipboard = ★★★★☆
send ^v
return
::jj5::
clipboard = ★★★★★
send ^v
return
;====== Lou END ======
;=============================jj系列===================================



;====== Lou BEG ======
;搜索功能
;用百度搜索 
#!b:: 
Send ^c 
Run http://www.baidu.com/s?wd=%clipboard% 
return 
;用google搜索 
#!g:: 
Send ^c 
Run http://www.google.com/search?q=%clipboard% 
return 
;====== Lou END ======


;====== Lou BEG ======
;特殊符号
;「
![::
clipboard = 「
send ^v
return

!]::
clipboard = 」
send ^v
return

;★输入
!9::
clipboard = ★
send ^v
return
;·输入
!8::
clipboard = ·
send ^v
return
#!]::
;====== Lou END ======



;====== Lou BEG ======
;方向控制
;光标方向控制
!i::Send {up} ;光标上移
!,::Send {down} ;光标下移
#!i::Send {pgup} ;光标翻页上移
#!,::Send {pgdn} ;光标翻页下移
!h::Send {left} ;光标左移
!l::Send {right} ;光标右移
!4::  ;到行末
Send, {end}
return
!0::  ;到行首
Send, {home}
return

;浏览器及资源管理器中使用
;前进
!=::
send, !{right}
return
;回退
!-::
send, !{left}
return 
;====== Lou END ======


;====== Lou BEG ======
;所有编辑器中的快捷操作
Shift & enter::send {end}{enter} ;下起一行
;+^o::send {home}{enter}{up} ;上起一行
+^!h::send,+^{left} ;选中左移一个单词
+^!l::send,+^{right} ;选中右移一个单词
+!i::send,{shiftdown}{up} ;选中上移
+!,::send,{shiftdown}{down} ;选中下移
+!h::send,{shiftdown}{left} ;选中左移
+!l::send,{shiftdown}{right} ;选中右移
+!4::send,+{end} ;选中当前光标位置到行末
+!0::send,+{home} ;选中当前光标位置到行首
;+^k::send,{end}{shiftdown}{home}{ShiftUp}{backspace}{backspace} ;删除当前行 

;复制当前行到剪切板 
+!v::
send,{home}{shiftdown}{end}{ShiftUp}
Send,^c
Send, {end}
Return 

;复制当前行到剪切板 
+!c::
send,{home}{shiftdown}{end}{ShiftUp}
Send,^c
Send, {end}
Return 

;剪切当前行到剪切板 
+!x::
send,{home}{shiftdown}{end}{ShiftUp}
Send,^x
Send, {backspace}
Return 


;删除光标到行末的内容
+!'::
send,+{end}{delete}
return 
;删除光标到行首的内容
+!;::
send,+{home}{delete}
return 
;====== Lou END ======


;====== Lou BEG ======
;替换按键
;新建
!n::
Send ^n
return
;撤销
!z::
Send ^z
return
;关闭
!w::
Send ^w
return
;粘贴
;+!p::
;Send ^v
;return
;粘贴
!v::
Send ^v
return
;剪切
!x::
Send ^x
return
;复制
!c::
Send ^c
return
;保存
!s::
Send ^s
return
!'::Send {delete} ;删除光标后面的一个字母或汉字
;ThinkPad键盘上的右键:PrintScreen
PrintScreen::Send +{F10}
;====== Lou END ======


;====== Lou BEG ======
;控制autohotyey
;挂起所有autohotkey按键
#!p::suspend
;====== Lou END ======

;====== Lou BEG ======
;切换鼠标左右键
#!q::
run control main.cpl
win_class = #32770
winwait ahk_class %win_class%
WinActivate ahk_class %win_class%
winwaitactive ahk_class %win_class%
if errorlevel = 0
{
  send !s
  sleep 500
  send {enter}
}
return
;====== Lou END ======


;====== Lou BEG ======
;隐藏窗口标题栏
#f11::
WinSet, Style, ^0xC00000, A
WinSet, Style, ^0x40000, A
return
;====== Lou END ======



;====== Lou BEG ======
#l::
; Lock Screen. 模拟Win+L没有成功，执行后Win似乎一直处于按下状态
Run, %A_WinDir%\System32\rundll32.exe user32.dll LockWorkStation 
Sleep, 500
; Power off the screen
SendMessage, 0x112, 0xF170, 2,, Program Manager
;====== Lou END ======


;====== Lou BEG ======
;;音量控制
;静音
#!0::
Send {Volume_Mute}
Return
;增加音量
#!=::
Send {Volume_Up 1} 
Return
;减少音量
#!-::
Send {Volume_Down 1}
Return
;====== Lou END ======



;====== Lou BEG ======
;具体应用
;for 360Chrome
#IfWinActive ahk_class Chrome_WidgetWin_1 
!j::Send ^+{Tab} 
!k::Send ^{Tab} 
!t::Send ^t 
+!t::Send ^+t 
return


;for eclipse
#IfWinActive ahk_class SWT_Window0
!j::Send ^{pgup}
!k::Send ^{pgdn}
!r::Send {F12} ;激活编辑窗
!a::send ^+s ;保存所有文件
!q::send ^+w ;关闭所有文件
return
;====== Lou END ======
```