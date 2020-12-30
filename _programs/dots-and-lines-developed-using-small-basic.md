---
title: "Dots and Lines (Developed using Small Basic)"
category: technet-archive
author:
  name: "Behnam Azizi"
project_url: "https://github.com/alxnull/smallbasic-gallery/tree/master/archive/Dots_and_Lines__Developed_using_Small_Basic_"
download: "https://github.com/alxnull/smallbasic-gallery/raw/master/archive/Dots_and_Lines__Developed_using_Small_Basic_/dots-and-lines (2).zip"
image: dots-and-lines-developed-using-small-basic.png
---

<b>A Dots and Lines Game developed using Microsoft Small Basic. This time I didn't spend much time on the program,. So the program might not be free of bugs. For example a simple bug that it has is that you should click next to each line to draw the line (not exactly on the line),</b>

<DIV id=longDesc>
<P>A Dots and Lines Game developed using Microsoft Small Basic. This time I didn't spend much time on the program,. So the program might not be free of bugs. For example a simple bug that it has is that you should click next to each line to draw the line (not exactly on the line), otherwise it won't draw a new line.&nbsp;</P>
<P>This game can be played with a firend. The program does not automatically declare a winner, and scores can be changed manually by players (so watch out that your opponent doesn't cheat in the game!!!!)</P>
<P>-------------------------------------------------------</P>
<P>Challenges that I had while developing this game:</P>
<P>I had to divide each square into 4 triangular sections. then based on where the user clicks on the screen the program finds out in which of the 4 triangular sections the user has clicked. To accomplish this the program finds the equations for lines that create those 4 triangles, and accordingly decides where to draw each line. Look at the Small Basic code for line equations.</P>
<P>
<P>&nbsp;</P>
<P><SPAN style="COLOR: #ff0000">Like always don't expecpt to get a very amazing game. This was done by an intermediate programmer for learning purposes.</SPAN></P>
<P><SPAN style="COLOR: #000000">Here is the code in Small Basic language:</SPAN></P>
<P><SPAN style="COLOR: #000000">&nbsp;</SPAN></P>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vb</SPAN> <PRE class=hidden>GraphicsWindow.Title = "Dots-And-Lines/Game"
GraphicsWindow.Width = 800
GraphicsWindow.Height = 600
GraphicsWindow.CanResize = "False"
GraphicsWindow.Top = 0
GraphicsWindow.Left = 0
TextWindow.Top = 0
TextWindow.Left = 850
TextWindow.Hide()
'GraphicsWindow.BrushColor = "red"
gh = GraphicsWindow.Height
gw = GraphicsWindow.Width
score1 = 0
score2 = 0
color = 1
lines = 0



  'gw = 200
  'gh = 200


menu()


sub menu
    GraphicsWindow.Clear()
  mainbg = ImageList.LoadImage(Program.Directory + "/pics/mainbg.jpg")
  GraphicsWindow.DrawResizedImage(mainbg, 0, 0, gw, gh)


start = Controls.AddButton("Let's begin", gw/2-150, gh/5+30)
'instr = Controls.AddButton("Instruction", gw/2-150, 2*gh/5+30)
'credit = Controls.AddButton("Credits", gw/2-150, 3*gh/5+30)


exit = Controls.AddButton("Exit", gw/2-150, 4*gh/5-300)

Controls.ButtonClicked = handleButton
EndSub

Sub handleButton
  Controls.Remove(start)
' Controls.Remove(instr)
' Controls.Remove(credit)
  Controls.Remove(exit)
  b = Controls.LastClickedButton

  If(b = exit) Then
    Program.End()
  'ElseIf(b = instr) then
  'elseIf(b = credit) then
  elseif (b = p1dec or b = p1inc or b = p2dec or b = p2inc) then
    changeScore()
  elseif (b = back) then
    menu()
  Else

  main()
 EndIf
EndSub

Sub main
  GraphicsWindow.Clear()
score2Shape = Shapes.AddText("Player 2: "+score2)
Shapes.Move(score2shape, 650, 10)

score1Shape = Shapes.AddText("Player 1: "+score1)
Shapes.Move(score1Shape, 250, 10)


p1inc = Controls.AddButton("&gt;&gt;&gt;", 350, 10)
p1dec = Controls.AddButton("&lt;&lt;&lt;", 200, 10)
p2inc = Controls.AddButton("&gt;&gt;&gt;", 750, 10)
p2dec = Controls.AddButton("&lt;&lt;&lt;", 600, 10)
back = Controls.AddButton("&lt;==", 50, 570)
For i=50 To gw - 10 Step 50
  For j=50 To gh - 10 Step 50
    dot = Shapes.AddEllipse(10, 10)
    Shapes.Move(dot, i, j)

  EndFor
EndFor

startover:
GraphicsWindow.MouseDown = handleMouse
EndSub

Sub handleMouse

  x = GraphicsWindow.MouseX
  y = GraphicsWindow.MouseY

 If  (x &gt; 50 And x&lt; gw-50 and y&gt; 50 And y&lt; gh-50) Then


  areaX = Math.Floor((x)/50)
  x1 = areaX*50 + 5
  X2 = x1 + 50

  areaY = Math.Floor((y)/50)
  y1 = areaY*50 + 5
  y2 = y1 + 50


  If (Math.Remainder(y, 50) = 5) Then
      Shapes.AddLine(x1, y, X2,y)
    EndIf

  If (Math.Remainder(x, 50) = 5) Then
      Shapes.AddLine(x, y1, x,y2)
    EndIf

 ' TextWindow.WriteLine("areaX = " + areaX+ " areaY = "+ areaY)

  'AREA 1
  If ((y-y1 &lt; ((y1 - y2)/(X2 - x1))*(x-x2)) And (y-y1 &lt; ((y1 - y2)/(X1 - x2))*(x-x1))) And (y &gt; y1) Then

Array[areaX+1][areaY+1] = 1
 ' TextWindow.WriteLine("array["+(areaX+1)+"]["+(areaY+1)+"] = 1")

  'TextWindow.WriteLine("upline")
  color = 1 - color
  lines = lines + 1
  Sound.PlayClick()
    If(color = 0) then
    GraphicsWindow.BrushColor = "red"
  Else
    GraphicsWindow.BrushColor = "black"
    EndIf
  Shapes.AddLine(x1, y1, X2,y1)

'AREA 2 
ElseIf (((y-y1 &lt; ((y1 - y2)/(X2 - x1))*(x-x2)) And (y-y1 &gt; ((y1 - y2)/(X1 - x2))*(x-x1))) And (x &gt; x1))  then

Array[areaX-1][areaY+1] = 1
 ' TextWindow.WriteLine("array["+(areaX-1)+"]["+(areaY+1)+"] = 1")
lines = lines + 1
  color = 1 - color
  Sound.PlayClick()
    If(color = 0) then
    GraphicsWindow.BrushColor = "red"
  Else
    GraphicsWindow.BrushColor = "black"
    EndIf
   Shapes.AddLine(x1, y1, X1,y2)

 'AREA 3
ElseIf (((y-y1 &gt; ((y1 - y2)/(X2 - x1))*(x-x2)) And (y-y1 &gt; ((y1 - y2)/(X1 - x2))*(x-x1))) And (y &lt; y2)) then
lines = lines + 1
Array[areaX+1][areaY+2] =  1
 ' TextWindow.WriteLine("array["+(areaX+1)+"]["+(areaY+2)+"] = 1")

  color = 1 - color
  Sound.PlayClick()
    If(color = 0) then
    GraphicsWindow.BrushColor = "red"
  Else
    GraphicsWindow.BrushColor = "black"
    EndIf
   Shapes.AddLine(x1, y2, X2,y2)

'AREA 4
ElseIf (((y-y1 &gt; ((y1 - y2)/(X2 - x1))*(x-x2)) And (y-y1 &lt; ((y1 - y2)/(X1 - x2))*(x-x1))) And (x &lt; x2)) then
lines = lines + 1

Array[areaX][areaY+1] = 1
 ' TextWindow.WriteLine("array["+(areaX)+"]["+(areaY+1)+"] = 1")
  color = 1 - color
  Sound.PlayClick()
  If(color = 0) then
    GraphicsWindow.BrushColor = "red"
  Else
    GraphicsWindow.BrushColor = "black"
    EndIf
   Shapes.AddLine(x2, y1, X2,y2)


EndIf
  EndIf



EndSub

'
Sub changeScore
  GraphicsWindow.BrushColor = "black"

  b = Controls.LastClickedButton
    Sound.PlayClick()
  If (b = p1dec) Then
    score1 = score1 - 1
    Shapes.Remove(score1Shape)
    score1Shape = Shapes.AddText("Player 1: "+score1)
    Shapes.Move(score1Shape, 250, 10)
  ElseIf (b = p1inc) Then
    score1 = score1 + 1
    Shapes.Remove(score1Shape)
    score1Shape = Shapes.AddText("Player 1: "+score1)
    Shapes.Move(score1Shape, 250, 10)
  ElseIf (b = p2dec) Then
    score2 = score2 - 1
    Shapes.Remove(score2Shape)
    score2Shape = Shapes.AddText("Player 2: "+score2)
    Shapes.Move(score2Shape, 650, 10)

Else
    score2 = score2 + 1
    Shapes.Remove(score2Shape)
    score2Shape = Shapes.AddText("Player 2: "+score2)
    Shapes.Move(score2Shape, 650, 10)


  EndIf

EndSub</PRE>
<DIV class=preview><PRE class=vb>GraphicsWindow.Title&nbsp;=&nbsp;<SPAN class=visualBasic__string>"Dots-And-Lines/Game"</SPAN>&nbsp;
GraphicsWindow.Width&nbsp;=&nbsp;<SPAN class=visualBasic__number>800</SPAN>&nbsp;
GraphicsWindow.Height&nbsp;=&nbsp;<SPAN class=visualBasic__number>600</SPAN>&nbsp;
GraphicsWindow.CanResize&nbsp;=&nbsp;<SPAN class=visualBasic__string>"False"</SPAN>&nbsp;
GraphicsWindow.Top&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
GraphicsWindow.Left&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
TextWindow.Top&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
TextWindow.Left&nbsp;=&nbsp;<SPAN class=visualBasic__number>850</SPAN>&nbsp;
TextWindow.Hide()&nbsp;
<SPAN class=visualBasic__com>'GraphicsWindow.BrushColor&nbsp;=&nbsp;"red"</SPAN>&nbsp;
gh&nbsp;=&nbsp;GraphicsWindow.Height&nbsp;
gw&nbsp;=&nbsp;GraphicsWindow.Width&nbsp;
score1&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
score2&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
color&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
lines&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'gw&nbsp;=&nbsp;200</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'gh&nbsp;=&nbsp;200</SPAN>&nbsp;
&nbsp;
&nbsp;
menu()&nbsp;
&nbsp;
&nbsp;
sub&nbsp;menu&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
&nbsp;&nbsp;mainbg&nbsp;=&nbsp;ImageList.LoadImage(Program.Directory&nbsp;+&nbsp;<SPAN class=visualBasic__string>"/pics/mainbg.jpg"</SPAN>)&nbsp;
&nbsp;&nbsp;GraphicsWindow.DrawResizedImage(mainbg,&nbsp;<SPAN class=visualBasic__number>0</SPAN>,&nbsp;<SPAN class=visualBasic__number>0</SPAN>,&nbsp;gw,&nbsp;gh)&nbsp;
&nbsp;
&nbsp;
start&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"Let's&nbsp;begin"</SPAN>,&nbsp;gw/<SPAN class=visualBasic__number>2</SPAN><SPAN class=visualBasic__number>-150</SPAN>,&nbsp;gh/<SPAN class=visualBasic__number>5</SPAN><SPAN class=visualBasic__number>+30</SPAN>)&nbsp;
<SPAN class=visualBasic__com>'instr&nbsp;=&nbsp;Controls.AddButton("Instruction",&nbsp;gw/2-150,&nbsp;2*gh/5+30)</SPAN>&nbsp;
<SPAN class=visualBasic__com>'credit&nbsp;=&nbsp;Controls.AddButton("Credits",&nbsp;gw/2-150,&nbsp;3*gh/5+30)</SPAN>&nbsp;
&nbsp;
&nbsp;
exit&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"Exit"</SPAN>,&nbsp;gw/<SPAN class=visualBasic__number>2</SPAN><SPAN class=visualBasic__number>-150</SPAN>,&nbsp;<SPAN class=visualBasic__number>4</SPAN>*gh/<SPAN class=visualBasic__number>5</SPAN><SPAN class=visualBasic__number>-300</SPAN>)&nbsp;
&nbsp;
Controls.ButtonClicked&nbsp;=&nbsp;handleButton&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=visualBasic__keyword>Sub</SPAN>&nbsp;handleButton&nbsp;
&nbsp;&nbsp;Controls.Remove(start)&nbsp;
<SPAN class=visualBasic__com>'&nbsp;Controls.Remove(instr)</SPAN>&nbsp;
<SPAN class=visualBasic__com>'&nbsp;Controls.Remove(credit)</SPAN>&nbsp;
&nbsp;&nbsp;Controls.Remove(exit)&nbsp;
&nbsp;&nbsp;b&nbsp;=&nbsp;Controls.LastClickedButton&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>(b&nbsp;=&nbsp;exit)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Program.<SPAN class=visualBasic__keyword>End</SPAN>()&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'ElseIf(b&nbsp;=&nbsp;instr)&nbsp;then</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'elseIf(b&nbsp;=&nbsp;credit)&nbsp;then</SPAN>&nbsp;
&nbsp;&nbsp;elseif&nbsp;(b&nbsp;=&nbsp;p1dec&nbsp;or&nbsp;b&nbsp;=&nbsp;p1inc&nbsp;or&nbsp;b&nbsp;=&nbsp;p2dec&nbsp;or&nbsp;b&nbsp;=&nbsp;p2inc)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;changeScore()&nbsp;
&nbsp;&nbsp;elseif&nbsp;(b&nbsp;=&nbsp;back)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;menu()&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;main()&nbsp;
&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=visualBasic__keyword>Sub</SPAN>&nbsp;main&nbsp;
&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
score2Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;2:&nbsp;"</SPAN>+score2)&nbsp;
Shapes.Move(score2shape,&nbsp;<SPAN class=visualBasic__number>650</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;
score1Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;1:&nbsp;"</SPAN>+score1)&nbsp;
Shapes.Move(score1Shape,&nbsp;<SPAN class=visualBasic__number>250</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;
&nbsp;
p1inc&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"&gt;&gt;&gt;"</SPAN>,&nbsp;<SPAN class=visualBasic__number>350</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
p1dec&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"&lt;&lt;&lt;"</SPAN>,&nbsp;<SPAN class=visualBasic__number>200</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
p2inc&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"&gt;&gt;&gt;"</SPAN>,&nbsp;<SPAN class=visualBasic__number>750</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
p2dec&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"&lt;&lt;&lt;"</SPAN>,&nbsp;<SPAN class=visualBasic__number>600</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
back&nbsp;=&nbsp;Controls.AddButton(<SPAN class=visualBasic__string>"&lt;=="</SPAN>,&nbsp;<SPAN class=visualBasic__number>50</SPAN>,&nbsp;<SPAN class=visualBasic__number>570</SPAN>)&nbsp;
<SPAN class=visualBasic__keyword>For</SPAN>&nbsp;i=<SPAN class=visualBasic__number>50</SPAN>&nbsp;<SPAN class=visualBasic__keyword>To</SPAN>&nbsp;gw&nbsp;-&nbsp;<SPAN class=visualBasic__number>10</SPAN>&nbsp;<SPAN class=visualBasic__keyword>Step</SPAN>&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>For</SPAN>&nbsp;j=<SPAN class=visualBasic__number>50</SPAN>&nbsp;<SPAN class=visualBasic__keyword>To</SPAN>&nbsp;gh&nbsp;-&nbsp;<SPAN class=visualBasic__number>10</SPAN>&nbsp;<SPAN class=visualBasic__keyword>Step</SPAN>&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;dot&nbsp;=&nbsp;Shapes.AddEllipse(<SPAN class=visualBasic__number>10</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(dot,&nbsp;i,&nbsp;j)&nbsp;
&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
EndFor&nbsp;
&nbsp;
startover:&nbsp;
GraphicsWindow.MouseDown&nbsp;=&nbsp;handleMouse&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=visualBasic__keyword>Sub</SPAN>&nbsp;handleMouse&nbsp;
&nbsp;
&nbsp;&nbsp;x&nbsp;=&nbsp;GraphicsWindow.MouseX&nbsp;
&nbsp;&nbsp;y&nbsp;=&nbsp;GraphicsWindow.MouseY&nbsp;
&nbsp;
&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>&nbsp;&nbsp;(x&nbsp;&gt;&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;x&lt;&nbsp;gw<SPAN class=visualBasic__number>-50</SPAN>&nbsp;and&nbsp;y&gt;&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;y&lt;&nbsp;gh<SPAN class=visualBasic__number>-50</SPAN>)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;areaX&nbsp;=&nbsp;Math.Floor((x)/<SPAN class=visualBasic__number>50</SPAN>)&nbsp;
&nbsp;&nbsp;x1&nbsp;=&nbsp;areaX*<SPAN class=visualBasic__number>50</SPAN>&nbsp;+&nbsp;<SPAN class=visualBasic__number>5</SPAN>&nbsp;
&nbsp;&nbsp;X2&nbsp;=&nbsp;x1&nbsp;+&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;areaY&nbsp;=&nbsp;Math.Floor((y)/<SPAN class=visualBasic__number>50</SPAN>)&nbsp;
&nbsp;&nbsp;y1&nbsp;=&nbsp;areaY*<SPAN class=visualBasic__number>50</SPAN>&nbsp;+&nbsp;<SPAN class=visualBasic__number>5</SPAN>&nbsp;
&nbsp;&nbsp;y2&nbsp;=&nbsp;y1&nbsp;+&nbsp;<SPAN class=visualBasic__number>50</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>&nbsp;(Math.Remainder(y,&nbsp;<SPAN class=visualBasic__number>50</SPAN>)&nbsp;=&nbsp;<SPAN class=visualBasic__number>5</SPAN>)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.AddLine(x1,&nbsp;y,&nbsp;X2,y)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>&nbsp;(Math.Remainder(x,&nbsp;<SPAN class=visualBasic__number>50</SPAN>)&nbsp;=&nbsp;<SPAN class=visualBasic__number>5</SPAN>)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.AddLine(x,&nbsp;y1,&nbsp;x,y2)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;<SPAN class=visualBasic__com>'&nbsp;TextWindow.WriteLine("areaX&nbsp;=&nbsp;"&nbsp;+&nbsp;areaX+&nbsp;"&nbsp;areaY&nbsp;=&nbsp;"+&nbsp;areaY)</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'AREA&nbsp;1</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>&nbsp;((y-y1&nbsp;&lt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X2&nbsp;-&nbsp;x1))*(x-x2))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y-y1&nbsp;&lt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X1&nbsp;-&nbsp;x2))*(x-x1)))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y&nbsp;&gt;&nbsp;y1)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;
Array[areaX<SPAN class=visualBasic__number>+1</SPAN>][areaY<SPAN class=visualBasic__number>+1</SPAN>]&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;<SPAN class=visualBasic__com>'&nbsp;TextWindow.WriteLine("array["+(areaX+1)+"]["+(areaY+1)+"]&nbsp;=&nbsp;1")</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__com>'TextWindow.WriteLine("upline")</SPAN>&nbsp;
&nbsp;&nbsp;color&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;-&nbsp;color&nbsp;
&nbsp;&nbsp;lines&nbsp;=&nbsp;lines&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>(color&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"red"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"black"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;Shapes.AddLine(x1,&nbsp;y1,&nbsp;X2,y1)&nbsp;
&nbsp;
<SPAN class=visualBasic__com>'AREA&nbsp;2&nbsp;</SPAN>&nbsp;
<SPAN class=visualBasic__keyword>ElseIf</SPAN>&nbsp;(((y-y1&nbsp;&lt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X2&nbsp;-&nbsp;x1))*(x-x2))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y-y1&nbsp;&gt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X1&nbsp;-&nbsp;x2))*(x-x1)))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(x&nbsp;&gt;&nbsp;x1))&nbsp;&nbsp;then&nbsp;
&nbsp;
Array[areaX<SPAN class=visualBasic__number>-1</SPAN>][areaY<SPAN class=visualBasic__number>+1</SPAN>]&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;<SPAN class=visualBasic__com>'&nbsp;TextWindow.WriteLine("array["+(areaX-1)+"]["+(areaY+1)+"]&nbsp;=&nbsp;1")</SPAN>&nbsp;
lines&nbsp;=&nbsp;lines&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;color&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;-&nbsp;color&nbsp;
&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>(color&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"red"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"black"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.AddLine(x1,&nbsp;y1,&nbsp;X1,y2)&nbsp;
&nbsp;
&nbsp;<SPAN class=visualBasic__com>'AREA&nbsp;3</SPAN>&nbsp;
<SPAN class=visualBasic__keyword>ElseIf</SPAN>&nbsp;(((y-y1&nbsp;&gt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X2&nbsp;-&nbsp;x1))*(x-x2))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y-y1&nbsp;&gt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X1&nbsp;-&nbsp;x2))*(x-x1)))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y&nbsp;&lt;&nbsp;y2))&nbsp;then&nbsp;
lines&nbsp;=&nbsp;lines&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
Array[areaX<SPAN class=visualBasic__number>+1</SPAN>][areaY<SPAN class=visualBasic__number>+2</SPAN>]&nbsp;=&nbsp;&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;<SPAN class=visualBasic__com>'&nbsp;TextWindow.WriteLine("array["+(areaX+1)+"]["+(areaY+2)+"]&nbsp;=&nbsp;1")</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;color&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;-&nbsp;color&nbsp;
&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>(color&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"red"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"black"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.AddLine(x1,&nbsp;y2,&nbsp;X2,y2)&nbsp;
&nbsp;
<SPAN class=visualBasic__com>'AREA&nbsp;4</SPAN>&nbsp;
<SPAN class=visualBasic__keyword>ElseIf</SPAN>&nbsp;(((y-y1&nbsp;&gt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X2&nbsp;-&nbsp;x1))*(x-x2))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(y-y1&nbsp;&lt;&nbsp;((y1&nbsp;-&nbsp;y2)/(X1&nbsp;-&nbsp;x2))*(x-x1)))&nbsp;<SPAN class=visualBasic__keyword>And</SPAN>&nbsp;(x&nbsp;&lt;&nbsp;x2))&nbsp;then&nbsp;
lines&nbsp;=&nbsp;lines&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;
Array[areaX][areaY<SPAN class=visualBasic__number>+1</SPAN>]&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;<SPAN class=visualBasic__com>'&nbsp;TextWindow.WriteLine("array["+(areaX)+"]["+(areaY+1)+"]&nbsp;=&nbsp;1")</SPAN>&nbsp;
&nbsp;&nbsp;color&nbsp;=&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;-&nbsp;color&nbsp;
&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>(color&nbsp;=&nbsp;<SPAN class=visualBasic__number>0</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"red"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"black"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.AddLine(x2,&nbsp;y1,&nbsp;X2,y2)&nbsp;
&nbsp;
&nbsp;
<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=visualBasic__com>'</SPAN>&nbsp;
<SPAN class=visualBasic__keyword>Sub</SPAN>&nbsp;changeScore&nbsp;
&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=visualBasic__string>"black"</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;b&nbsp;=&nbsp;Controls.LastClickedButton&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>If</SPAN>&nbsp;(b&nbsp;=&nbsp;p1dec)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score1&nbsp;=&nbsp;score1&nbsp;-&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(score1Shape)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score1Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;1:&nbsp;"</SPAN>+score1)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(score1Shape,&nbsp;<SPAN class=visualBasic__number>250</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>ElseIf</SPAN>&nbsp;(b&nbsp;=&nbsp;p1inc)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score1&nbsp;=&nbsp;score1&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(score1Shape)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score1Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;1:&nbsp;"</SPAN>+score1)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(score1Shape,&nbsp;<SPAN class=visualBasic__number>250</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>ElseIf</SPAN>&nbsp;(b&nbsp;=&nbsp;p2dec)&nbsp;<SPAN class=visualBasic__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score2&nbsp;=&nbsp;score2&nbsp;-&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(score2Shape)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score2Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;2:&nbsp;"</SPAN>+score2)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(score2Shape,&nbsp;<SPAN class=visualBasic__number>650</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;
<SPAN class=visualBasic__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score2&nbsp;=&nbsp;score2&nbsp;+&nbsp;<SPAN class=visualBasic__number>1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(score2Shape)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;score2Shape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=visualBasic__string>"Player&nbsp;2:&nbsp;"</SPAN>+score2)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(score2Shape,&nbsp;<SPAN class=visualBasic__number>650</SPAN>,&nbsp;<SPAN class=visualBasic__number>10</SPAN>)&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;<SPAN class=visualBasic__keyword>EndIf</SPAN>&nbsp;
&nbsp;
EndSub</PRE></DIV></DIV></DIV>
<DIV class=endscriptcode>&nbsp;</DIV></DIV>
