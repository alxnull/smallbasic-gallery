---
title: "Tancraft (Developed using Small Basic)"
category: technet-archive
author:
  name: "Behnam Azizi"
project_url: "https://github.com/alxnull/smallbasic-gallery/tree/master/archive/Tancraft__Developed_using_Small_Basic_"
download: "https://github.com/alxnull/smallbasic-gallery/raw/master/archive/Tancraft__Developed_using_Small_Basic_/Tancraft.zip"
image: tancraft-developed-using-small-basic.png
---

<b>Here is another game that I made using small basic. I named it Tancraft. It is a 2-player game you can play with one of you friends.I am so thankful to Litdev for his awesome extensions. I used his extension to use an animated image (the explosion of the tanks) in my game.&nbsp; At th</b>

<DIV id=longDesc>
<P>Here is another game that I made using small basic. I named it Tancraft. It is a 2-player game you can play with one of you friends.</P>
<P>I am so thankful to Litdev for his awesome extensions. I used his extension to use an animated image (the explosion of the tanks) in my game.</P>
<P>&nbsp; At the beginning each player places their tanks anywhere on their own land (lands are seperated with the red line), and then starting from the top player you click somewhere in you own land. Once you click there the corresponding point on the other side of the red line willl be shot. If there is enemy's tank there the tank would explode.</P>
<P>You can download the game from here (at the top of the page)</P>
<P><SPAN style="COLOR: #ff0000">And please don't expect to see a super amazing game! I did all the programming on my own. This was done only for learning purposes.</SPAN></P>
<P>-----------------------------------------------------------</P>
<P><SPAN style="COLOR: #000000">Challenges that I had while developing this game:</SPAN></P>
<P>Compared to my other game projects in Small Basic, this was a simple one. Once one of the players clicks somewhere on the screen the program finds the corresponding point on the opponensts land with respect to the lined breaking between the two lands. Then if there is a tank in approximity it would explode!!!</P>
<P>
<P>&nbsp;</P>
<P>Here is the source code:</P>
<P>&nbsp;</P>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>VB Script</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vbs</SPAN> <PRE class=hidden>GraphicsWindow.Width=500
GraphicsWindow.Height=500

map= ImageList.LoadImage(Program.Directory+"/pics/map.jpg")
GraphicsWindow.DrawResizedImage(map, 0, 0, 510, 510)

'startover:

GraphicsWindow.FontName="Arial"
GraphicsWindow.BrushColor= "Black"
GraphicsWindow.FontSize="12"
GraphicsWindow.DrawText(330, 0, "Developed by behnam Azizi")

vehicle1=ImageList.LoadImage(Program.Directory+"/pics/Tank1.png")
vehicle2=ImageList.LoadImage(Program.Directory+"/pics/Tank2.png")

For i=0 to 10
  shapeA[i]= Shapes.AddImage(vehicle1)
  Shapes.Move(shapeA[i], -50, -50)
endfor

For j=0 to 10
  shapeB[j]= Shapes.AddImage(vehicle2)
  Shapes.Move(shapeB[j], 0, -50)
endfor

j=0
i=0


GraphicsWindow.CanResize="False"
GraphicsWindow.MouseDown=handleMouse
GraphicsWindow.PenColor="brown"
Shapes.AddLine(0,250,510,250)
GraphicsWindow.PenColor="transparent"
GraphicsWindow.KeyDown= handlekey


Sub handleKey
  If GraphicsWindow.LastKey="Q" Then
    GraphicsWindow.PenColor="black"
  ElseIf GraphicsWindow.LastKey="W" then  
    GraphicsWindow.PenColor="transparent"
    EndIf

EndSub

Sub rocket

ammo=Shapes.AddImage(ammo)
Shapes.Animate(ammo, Math.GetRandomNumber(300), Math.GetRandomNumber(300), 1000)
x=Shapes.GetLeft(ammo)
y= Shapes.GetTop(ammo)

If xpos&gt;x And xpos&lt;x+40 And ypos&lt;500-y And ypos&gt;460-y Then
      Shapes.Animate(ammo, math.GetRandomNumber(500), 540, 300)
      

    EndIf   
  

EndSub

sub handleMouse

xpos= GraphicsWindow.MouseX 
ypos= GraphicsWindow.MouseY

'If t=20 Then
'    rocket()
'    EndIf



If t&lt;=8 And ypos&lt;250 Then
  
start1()
t=t+1
ElseIf t&lt;=17 and t&gt;=9 and ypos&gt;250 then
  
  start2()
t=t+1
ElseIf t&gt;=18 then
  
  'Shapes.HideShape(tankA[2])
  
  If Math.Remainder(t, 2)=0 And ypos&lt;250 Then
    Player1()
    winner()
  t=t+1
  ElseIf Math.Remainder(t, 2)=1 And ypos&gt;250 Then
    Player2()
    winner()
  t=t+1
  EndIf






EndIf
EndSub

Sub winner

For i=0 To 8
  
    If A[i]= "69" Then
           p=p+1
     EndIf      
     If B[i]="69" then
      
      q=q+1
      
    EndIf
    
EndFor


If p=9 Then
'Sound.play(Program.Directory+"sounds/bomb.mp3")

GraphicsWindow.ShowMessage("Player 2 wins!","Game Over!")

CLS()
  
ElseIf q=9 then


'Sound.play(Program.Directory+"sounds/bomb.mp3")
GraphicsWindow.ShowMessage("Player 1 wins!","Game Over!")

  CLS()
  
  EndIf

  p=0
  q=0
EndSub

Sub Player1
  
  Sound.Stop(Program.Directory+"/sounds/Tick.mp3")
  Sound.Play(Program.Directory+"/sounds/Tick.mp3")
  Shapes.HideShape(lineA)
  Shapes.HideShape(lineB)
  Error="True"
  lineA=Shapes.AddLine(0,ypos,500, ypos)
  lineB=Shapes.AddLine(0,500-ypos,500, 500-ypos)


For j=0 To 8
      x= Shapes.GetLeft(tankB[j])
  y= Shapes.GetTop(tankB[j])

If xpos&gt;x And xpos&lt;x+40 And ypos&lt;500-y And ypos&gt;460-y Then
       Sound.Stop(Program.Directory+"/sounds/Bomb.mp3")
       Sound.Play(Program.Directory+"/sounds/Bomb.mp3")  
       explode = LDShapes.AddAnimatedImage(Program.Directory + "\pics\anim.png", "False",4, 4)
  Shapes.Move(explode, Shapes.GetLeft(tankB[j]), Shapes.GetTop(tankB[j]))
  
     Shapes.Animate(tankB[j], math.GetRandomNumber(500), 540, 300)
     
     
'      Shapes.HideShape(tankB[j])
B[j]="69"
Error="False"

    EndIf  
  
EndFor
Shapes.HideShape(text)
  text=Shapes.AddText("Player 2")
  Shapes.Move(text, 0, 0)
  
  If Error="True" Then
       Sound.Stop(Program.Directory+"/sounds/Error.mp3")
       Sound.Play(Program.Directory+"/sounds/Error.mp3")
       'Shapes.AddImage(gunshot)
'       Shapes.Move(gunshot, xpos, ypos)
  EndIf
EndSub

Sub Player2
  Sound.Stop(Program.Directory+"/sounds/Tick.mp3")
  Sound.Play(Program.Directory+"/sounds/Tick.mp3")
Shapes.HideShape(lineA)
  Shapes.HideShape(lineB)
Error="True"
lineA =Shapes.AddLine(0,ypos,500, ypos)
 lineB=Shapes.AddLine(0,500-ypos,500, 500-ypos)
    
  For i=0 To 8
      x= Shapes.GetLeft(tankA[i])
  y= Shapes.GetTop(tankA[i])
     If xpos&gt;x And xpos&lt;x+40 And ypos&lt;500-y And ypos&gt;460-y Then
             Sound.Stop(Program.Directory + "/sounds/Bomb.mp3")
             Sound.Play(Program.Directory + "/sounds/Bomb.mp3")
                  explode = LDShapes.AddAnimatedImage(Program.Directory + "\pics\anim.png", "False",4, 4)
  Shapes.Move(explode, Shapes.GetLeft(tankA[i]), Shapes.GetTop(tankA[i]))
  
      Shapes.Animate(tankA[i], Math.GetRandomNumber(500), -40, 300)
      A[i]="69"
      Error="False"
    EndIf  
    
Shapes.HideShape(text)
  text=Shapes.AddText("Player 1")
  Shapes.Move(text, 0, 0)  

EndFor  
If Error="True" Then
       Sound.Stop(Program.Directory+"/sounds/Error.mp3")
       Sound.Play(Program.Directory+"/sounds/Error.mp3")
              'Shapes.Move(gunshot, xpos, ypos)
  EndIf
EndSub

Sub start1
  Sound.Stop(Program.Directory+"/sounds/Tick.mp3")
  Sound.Play(Program.Directory+"/sounds/Tick.mp3")
  
  'R = Math.GetRandomNumber(2)
 
' If R=1 Then
    tankA[i] = shapeA[i]
'    ElseIf R=2 then
'    tankA[i]=Shapes.AddEllipse(40, 70)
    
    
      'EndIf

Shapes.Move(tankA[i], 250, -40)
Shapes.Animate(tankA[i], xpos-20, ypos-20, 500)
    i=i+1
    
  EndSub
  
  Sub start2
    Sound.Stop(Program.Directory+"/sounds/Tick.mp3")
     Sound.Play(Program.Directory+"/sounds/Tick.mp3")
    ' R = Math.GetRandomNumber(2)
 
 'If R=1 Then
    tankB[j] = shapeB[j]
 '   ElseIf R=2 then
 '   tankB[i]=Shapes.AddEllipse(40, 70)
    
    
 '     EndIf

Shapes.Move(tankB[j], 250, -40)
Shapes.Animate(tankB[j], xpos-20, ypos-20, 500)
    j=j+1
    
  EndSub
  
  
  
  Sub CLS
    p=0
    q=0
    GraphicsWindow.Clear()
    For i=0 To 8
      tankA[i]=0
      tankB[i]=0
      
      
      EndFor
    
    'Program.Delay(2000)
    Program.End()
    
    EndSub</PRE>
<DIV class=preview><PRE class=vbs>GraphicsWindow.Width=<SPAN class=vbScript__number>500</SPAN>&nbsp;
GraphicsWindow.Height=<SPAN class=vbScript__number>500</SPAN>&nbsp;
&nbsp;
map=&nbsp;ImageList.LoadImage(Program.Directory+<SPAN class=vbScript__string>"/pics/map.jpg"</SPAN>)&nbsp;
GraphicsWindow.DrawResizedImage(map,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>510</SPAN>,&nbsp;<SPAN class=vbScript__number>510</SPAN>)&nbsp;
&nbsp;
<SPAN class=vbScript__com>'startover:</SPAN>&nbsp;
&nbsp;
GraphicsWindow.FontName=<SPAN class=vbScript__string>"Arial"</SPAN>&nbsp;
GraphicsWindow.BrushColor=&nbsp;<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
GraphicsWindow.FontSize=<SPAN class=vbScript__string>"12"</SPAN>&nbsp;
GraphicsWindow.DrawText(<SPAN class=vbScript__number>330</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__string>"Developed&nbsp;by&nbsp;behnam&nbsp;Azizi"</SPAN>)&nbsp;
&nbsp;
vehicle1=ImageList.LoadImage(Program.Directory+<SPAN class=vbScript__string>"/pics/Tank1.png"</SPAN>)&nbsp;
vehicle2=ImageList.LoadImage(Program.Directory+<SPAN class=vbScript__string>"/pics/Tank2.png"</SPAN>)&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;to&nbsp;<SPAN class=vbScript__number>10</SPAN>&nbsp;
&nbsp;&nbsp;shapeA[i]=&nbsp;Shapes.AddImage(vehicle1)&nbsp;
&nbsp;&nbsp;Shapes.Move(shapeA[i],&nbsp;-<SPAN class=vbScript__number>50</SPAN>,&nbsp;-<SPAN class=vbScript__number>50</SPAN>)&nbsp;
endfor&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;to&nbsp;<SPAN class=vbScript__number>10</SPAN>&nbsp;
&nbsp;&nbsp;shapeB[j]=&nbsp;Shapes.AddImage(vehicle2)&nbsp;
&nbsp;&nbsp;Shapes.Move(shapeB[j],&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;-<SPAN class=vbScript__number>50</SPAN>)&nbsp;
endfor&nbsp;
&nbsp;
j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
i=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;
&nbsp;
GraphicsWindow.CanResize=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
GraphicsWindow.MouseDown=handleMouse&nbsp;
GraphicsWindow.PenColor=<SPAN class=vbScript__string>"brown"</SPAN>&nbsp;
Shapes.AddLine(<SPAN class=vbScript__number>0</SPAN>,<SPAN class=vbScript__number>250</SPAN>,<SPAN class=vbScript__number>510</SPAN>,<SPAN class=vbScript__number>250</SPAN>)&nbsp;
GraphicsWindow.PenColor=<SPAN class=vbScript__string>"transparent"</SPAN>&nbsp;
GraphicsWindow.KeyDown=&nbsp;handlekey&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;handleKey&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;GraphicsWindow.LastKey=<SPAN class=vbScript__string>"Q"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.PenColor=<SPAN class=vbScript__string>"black"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;GraphicsWindow.LastKey=<SPAN class=vbScript__string>"W"</SPAN>&nbsp;then&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.PenColor=<SPAN class=vbScript__string>"transparent"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;rocket&nbsp;
&nbsp;
ammo=Shapes.AddImage(ammo)&nbsp;
Shapes.Animate(ammo,&nbsp;Math.GetRandomNumber(<SPAN class=vbScript__number>300</SPAN>),&nbsp;Math.GetRandomNumber(<SPAN class=vbScript__number>300</SPAN>),&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
x=Shapes.GetLeft(ammo)&nbsp;
y=&nbsp;Shapes.GetTop(ammo)&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;xpos&gt;x&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;xpos&lt;x<SPAN class=vbScript__number>+40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&lt;<SPAN class=vbScript__number>500</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&gt;<SPAN class=vbScript__number>460</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(ammo,&nbsp;math.GetRandomNumber(<SPAN class=vbScript__number>500</SPAN>),&nbsp;<SPAN class=vbScript__number>540</SPAN>,&nbsp;<SPAN class=vbScript__number>300</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;
EndSub&nbsp;
&nbsp;
sub&nbsp;handleMouse&nbsp;
&nbsp;
xpos=&nbsp;GraphicsWindow.MouseX&nbsp;&nbsp;
ypos=&nbsp;GraphicsWindow.MouseY&nbsp;
&nbsp;
<SPAN class=vbScript__com>'If&nbsp;t=20&nbsp;Then</SPAN>&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;rocket()</SPAN>&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;t&lt;=<SPAN class=vbScript__number>8</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&lt;<SPAN class=vbScript__number>250</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
start1()&nbsp;
t=t<SPAN class=vbScript__number>+1</SPAN>&nbsp;
<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;t&lt;=<SPAN class=vbScript__number>17</SPAN>&nbsp;and&nbsp;t&gt;=<SPAN class=vbScript__number>9</SPAN>&nbsp;and&nbsp;ypos&gt;<SPAN class=vbScript__number>250</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;start2()&nbsp;
t=t<SPAN class=vbScript__number>+1</SPAN>&nbsp;
<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;t&gt;=<SPAN class=vbScript__number>18</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__com>'Shapes.HideShape(tankA[2])</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;Math.Remainder(t,&nbsp;<SPAN class=vbScript__number>2</SPAN>)=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&lt;<SPAN class=vbScript__number>250</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Player1()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;winner()&nbsp;
&nbsp;&nbsp;t=t<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;Math.Remainder(t,&nbsp;<SPAN class=vbScript__number>2</SPAN>)=<SPAN class=vbScript__number>1</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&gt;<SPAN class=vbScript__number>250</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Player2()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;winner()&nbsp;
&nbsp;&nbsp;t=t<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;winner&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>8</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;A[i]=&nbsp;<SPAN class=vbScript__string>"69"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;p=p<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;B[i]=<SPAN class=vbScript__string>"69"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;q=q<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
EndFor&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;p=<SPAN class=vbScript__number>9</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
<SPAN class=vbScript__com>'Sound.play(Program.Directory+"sounds/bomb.mp3")</SPAN>&nbsp;
&nbsp;
GraphicsWindow.ShowMessage(<SPAN class=vbScript__string>"Player&nbsp;2&nbsp;wins!"</SPAN>,<SPAN class=vbScript__string>"Game&nbsp;Over!"</SPAN>)&nbsp;
&nbsp;
CLS()&nbsp;
&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;q=<SPAN class=vbScript__number>9</SPAN>&nbsp;then&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__com>'Sound.play(Program.Directory+"sounds/bomb.mp3")</SPAN>&nbsp;
GraphicsWindow.ShowMessage(<SPAN class=vbScript__string>"Player&nbsp;1&nbsp;wins!"</SPAN>,<SPAN class=vbScript__string>"Game&nbsp;Over!"</SPAN>)&nbsp;
&nbsp;
&nbsp;&nbsp;CLS()&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;p=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;q=<SPAN class=vbScript__number>0</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;Player1&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.HideShape(lineA)&nbsp;
&nbsp;&nbsp;Shapes.HideShape(lineB)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;
&nbsp;&nbsp;lineA=Shapes.AddLine(<SPAN class=vbScript__number>0</SPAN>,ypos,<SPAN class=vbScript__number>500</SPAN>,&nbsp;ypos)&nbsp;
&nbsp;&nbsp;lineB=Shapes.AddLine(<SPAN class=vbScript__number>0</SPAN>,<SPAN class=vbScript__number>500</SPAN>-ypos,<SPAN class=vbScript__number>500</SPAN>,&nbsp;<SPAN class=vbScript__number>500</SPAN>-ypos)&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>8</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x=&nbsp;Shapes.GetLeft(tankB[j])&nbsp;
&nbsp;&nbsp;y=&nbsp;Shapes.GetTop(tankB[j])&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;xpos&gt;x&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;xpos&lt;x<SPAN class=vbScript__number>+40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&lt;<SPAN class=vbScript__number>500</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&gt;<SPAN class=vbScript__number>460</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Bomb.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Bomb.mp3"</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;explode&nbsp;=&nbsp;LDShapes.AddAnimatedImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"\pics\anim.png"</SPAN>,&nbsp;<SPAN class=vbScript__string>"False"</SPAN>,<SPAN class=vbScript__number>4</SPAN>,&nbsp;<SPAN class=vbScript__number>4</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(explode,&nbsp;Shapes.GetLeft(tankB[j]),&nbsp;Shapes.GetTop(tankB[j]))&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(tankB[j],&nbsp;math.GetRandomNumber(<SPAN class=vbScript__number>500</SPAN>),&nbsp;<SPAN class=vbScript__number>540</SPAN>,&nbsp;<SPAN class=vbScript__number>300</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.HideShape(tankB[j])</SPAN>&nbsp;
B[j]=<SPAN class=vbScript__string>"69"</SPAN>&nbsp;
<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
EndFor&nbsp;
Shapes.HideShape(text)&nbsp;
&nbsp;&nbsp;text=Shapes.AddText(<SPAN class=vbScript__string>"Player&nbsp;2"</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(text,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Error.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Error.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'Shapes.AddImage(gunshot)</SPAN>&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(gunshot,&nbsp;xpos,&nbsp;ypos)</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;Player2&nbsp;
&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
Shapes.HideShape(lineA)&nbsp;
&nbsp;&nbsp;Shapes.HideShape(lineB)&nbsp;
<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;
lineA&nbsp;=Shapes.AddLine(<SPAN class=vbScript__number>0</SPAN>,ypos,<SPAN class=vbScript__number>500</SPAN>,&nbsp;ypos)&nbsp;
&nbsp;lineB=Shapes.AddLine(<SPAN class=vbScript__number>0</SPAN>,<SPAN class=vbScript__number>500</SPAN>-ypos,<SPAN class=vbScript__number>500</SPAN>,&nbsp;<SPAN class=vbScript__number>500</SPAN>-ypos)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>8</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x=&nbsp;Shapes.GetLeft(tankA[i])&nbsp;
&nbsp;&nbsp;y=&nbsp;Shapes.GetTop(tankA[i])&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;xpos&gt;x&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;xpos&lt;x<SPAN class=vbScript__number>+40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&lt;<SPAN class=vbScript__number>500</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;ypos&gt;<SPAN class=vbScript__number>460</SPAN>-y&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Bomb.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.Play(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Bomb.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;explode&nbsp;=&nbsp;LDShapes.AddAnimatedImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"\pics\anim.png"</SPAN>,&nbsp;<SPAN class=vbScript__string>"False"</SPAN>,<SPAN class=vbScript__number>4</SPAN>,&nbsp;<SPAN class=vbScript__number>4</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(explode,&nbsp;Shapes.GetLeft(tankA[i]),&nbsp;Shapes.GetTop(tankA[i]))&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(tankA[i],&nbsp;Math.GetRandomNumber(<SPAN class=vbScript__number>500</SPAN>),&nbsp;-<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>300</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A[i]=<SPAN class=vbScript__string>"69"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
Shapes.HideShape(text)&nbsp;
&nbsp;&nbsp;text=Shapes.AddText(<SPAN class=vbScript__string>"Player&nbsp;1"</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(text,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;
EndFor&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;<SPAN class=vbScript__keyword>Error</SPAN>=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Error.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Error.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'Shapes.Move(gunshot,&nbsp;xpos,&nbsp;ypos)</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;start1&nbsp;
&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__com>'R&nbsp;=&nbsp;Math.GetRandomNumber(2)</SPAN>&nbsp;
&nbsp;&nbsp;
<SPAN class=vbScript__com>'&nbsp;If&nbsp;R=1&nbsp;Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;tankA[i]&nbsp;=&nbsp;shapeA[i]&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;ElseIf&nbsp;R=2&nbsp;then</SPAN>&nbsp;
<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;tankA[i]=Shapes.AddEllipse(40,&nbsp;70)</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'EndIf</SPAN>&nbsp;
&nbsp;
Shapes.Move(tankA[i],&nbsp;<SPAN class=vbScript__number>250</SPAN>,&nbsp;-<SPAN class=vbScript__number>40</SPAN>)&nbsp;
Shapes.Animate(tankA[i],&nbsp;xpos<SPAN class=vbScript__number>-20</SPAN>,&nbsp;ypos<SPAN class=vbScript__number>-20</SPAN>,&nbsp;<SPAN class=vbScript__number>500</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;i=i<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;start2&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.Play(Program.Directory+<SPAN class=vbScript__string>"/sounds/Tick.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'&nbsp;R&nbsp;=&nbsp;Math.GetRandomNumber(2)</SPAN>&nbsp;
&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__com>'If&nbsp;R=1&nbsp;Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;tankB[j]&nbsp;=&nbsp;shapeB[j]&nbsp;
&nbsp;<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;ElseIf&nbsp;R=2&nbsp;then</SPAN>&nbsp;
&nbsp;<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;tankB[i]=Shapes.AddEllipse(40,&nbsp;70)</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__com>'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndIf</SPAN>&nbsp;
&nbsp;
Shapes.Move(tankB[j],&nbsp;<SPAN class=vbScript__number>250</SPAN>,&nbsp;-<SPAN class=vbScript__number>40</SPAN>)&nbsp;
Shapes.Animate(tankB[j],&nbsp;xpos<SPAN class=vbScript__number>-20</SPAN>,&nbsp;ypos<SPAN class=vbScript__number>-20</SPAN>,&nbsp;<SPAN class=vbScript__number>500</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;CLS&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;p=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;q=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>8</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tankA[i]=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tankB[i]=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'Program.Delay(2000)</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Program.<SPAN class=vbScript__keyword>End</SPAN>()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndSub</PRE></DIV></DIV></DIV>
<DIV class=endscriptcode>&nbsp;</DIV></DIV>
