---
title: "Block Smasher V2.0 (developed using small basic)"
category: technet-archive
author:
  name: "Behnam Azizi"
project_url: "https://github.com/alxnull/smallbasic-gallery/tree/master/archive/Block_Smasher_V2.0__developed_using_small_basic_"
download: "https://github.com/alxnull/smallbasic-gallery/raw/master/archive/Block_Smasher_V2.0__developed_using_small_basic_/Block Smasher.zip"
image: block-smasher-v20-developed-using-small-basic.png
---

<b>Finally, the ultimate version of the Block Smasher is out! download it from here and play. It has 6 distinct levels and I added the save/load feature. So once tired, you are able to save the game and play the rest anytime you wish. Note that it might take a while for the game t</b>

<DIV id=longDesc>
<P>Finally, the ultimate version of the <SPAN>Block Smasher</SPAN> is out! download it from here and play. It has 6 distinct levels and I added the save/load feature. So once tired, you are able to save the game and play the rest anytime you wish. Note that it might take a while for the game to save/load once you press S/L and the loaded game would not resume until you lose the current level once. I also added cheat codes to the game for more fun. &nbsp;You will get the cheat codes once you finish the game (And please don't cheat to find the cheat codes! Play the game thoroughly!).</P>
<P>One of the special features I added to this game is that the paddle changes direction when hit by the ball depending on the side of the paddle that is hit by the ball. For example if the ball hits the right side of the paddle, the paddle rotates 20 degrees to the right.</P>
<P>Here is just an alternate download link: https://www.dropbox.com/s/1qz78voduciajr1/Breaker%20V%202.0.zip</P>
<P><SPAN style="COLOR: #ff0000">And please don't expect to see a super amazing game! I did all the programming on my own. This was done only for learning purposes.</SPAN></P>
<P>------------------------------------------------------</P>
<P>Challenges that I had while developing this game:</P>
<P>At each instance the program checks to see whether there has been a collision between the ball and each of the blocks. To accomplish this I created an array (matrix or whatever they call it!) holding the information about all blocks. And then constantly the program can theck if each of the blocks have been smashed by the ball. Now it doesn`t all end here: once there has been a collision betweent the ball and a block, the program should bounce the ball based on the angle from which the ball hits the square. Look at the code to see how I did this!</P>
<P>&nbsp;</P>
<P>&nbsp;
<P>&nbsp;</P>
<P>&nbsp;</P>
<P>Also please note that some of the sounds and pictures used in the game are not mine. I downloaded the sound used in the main menu from here:</P>
<P><EM>http://www.newgrounds.com/audio/listen/199965</EM></P>
<P><EM>Here is the source code:</EM></P>
<P><EM>&nbsp;</EM></P>
<P><EM>&nbsp;</EM></P>
<P><EM>&nbsp;</EM></P>
<P><EM>&nbsp;</EM></P>
<P><EM></P>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>VB Script</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vbs</SPAN> <PRE class=hidden>GraphicsWindow.CanResize="False"
level=1
menu()

'startover:
main()

'------------------------------------------------   SUBS ---------------------------------------
sub main
deltaX = 1
deltaY = 1
height= 40
GraphicsWindow.KeyDown = processkey

  win="True"
  If level=1 Then
    level1()
  ElseIf level=2 then
    level2()
    ElseIf level=3 then
      level3()
    elseif level=4 then
      level4()
    elseif level=5 then
      level5()
    elseif level=6 then
      level6()
    Else
      gameend()
      GraphicsWindow.DrawRectangle(gw/2, gh/2, 200, 200)
      GraphicsWindow.DrawBoundText(gw/2, gh/2, 198, "Congratulations! You won all levels!")
  EndIf
 
GraphicsWindow.BrushColor= "Black"
  Shapes.Remove(Slevel)
  Slevel = Shapes.AddText("Level: "+ level)
Shapes.Move(Slevel, 550, 10)
GraphicsWindow.CanResize="False"
'GraphicsWindow.BackgroundColor = "lightBlue"


paddle = Shapes.AddRectangle(120, 12)
ball = Shapes.AddEllipse(16, 16)
Shapes.Move(ball, -16, -16)

gw = GraphicsWindow.Width
gh = GraphicsWindow.Height
bkg = ImageList.LoadImage(Program.Directory + "/pics/metal.jpg")
GraphicsWindow.DrawResizedImage(bkg, 0, 0, gw, gh)

GraphicsWindow.BrushColor="Black"
GraphicsWindow.DrawText(10, 10,"Developed by Behnam Azizi")
GraphicsWindow.BrushColor= GraphicsWindow.GetRandomColor()
GraphicsWindow.MouseMove = OnMouseMove




x = 2
y = gh-48
'Timer.Interval= 1000

GraphicsWindow.BrushColor="Black"
play=Controls.AddButton("Press to Play!",gw/2-50, gh/2)

While Controls.LastClickedButton&lt;&gt;play

endwhile

Controls.Remove(play)





RunLoop:
hitBlock()
winner()
x = x + deltaX
y = y - deltaY

Program.Delay(1)
If (x+8 &gt;= gw - 9 or x+8 &lt;= 9) Then
deltaX = -1*deltaX
EndIf

If (y+8 &lt;= 8) Then
deltaY = -1*deltaY
EndIf

paddlehit() 
 
Shapes.Move(ball, x, y)

If (y &lt; gh) Then
Goto RunLoop
EndIf

Sound.Play(Program.Directory + "/sounds/Error.mp3")
GraphicsWindow.ShowMessage("You Lose", "Paddle")
win="False"
PlayAgain()
deltaY=-1
EndSub

'----------------------------------------------   SUBROUTINES ------------------------------------


Sub menu
  Sound.Play(Program.Directory + "/sounds/Menu music.mp3")
  menubkg = ImageList.LoadImage(Program.Directory + "/pics/menu.jpg")
GraphicsWindow.DrawResizedImage(menubkg, 0, 0, GraphicsWindow.Width, GraphicsWindow.Height)
  start=Controls.AddButton("Start", 260, 160)
  instructions= Controls.AddButton("Instructions", 260, 200)
  Exit = Controls.AddButton("Exit", 260, 240)



While Controls.LastClickedButton&lt;&gt;start And Controls.LastClickedButton&lt;&gt;instructions And Controls.LastClickedButton&lt;&gt;Exit

EndWhile

If Controls.LastClickedButton=Exit Then
  Program.End()
ElseIf Controls.LastClickedButton=instructions then
  instructionspage()
  EndIf



GraphicsWindow.Clear()
Sound.Stop(Program.Directory + "/sounds/Menu music.mp3")
EndSub

Sub instructionspage
  GraphicsWindow.Clear()
 instr= ImageList.LoadImage(Program.Directory + "/pics/instructions.jpg")
  GraphicsWindow.DrawResizedImage(instr, 0, 0,GraphicsWindow.Width, GraphicsWindow.Height)
  back = Controls.AddButton("&lt;--- Back", 50, 400)
  
  While Controls.LastClickedButton&lt;&gt;back
    
    EndWhile
  
    GraphicsWindow.Clear()
    menu()
  
  
  EndSub

Sub paddlehit
  padX = Shapes.GetLeft (paddle)
  padY= Shapes.GetTop(paddle)
  If (y+8&gt;= padY-8 And y+8&lt;= padY+12 And (x+8 &gt;= padX-8 And x+8 &lt;= padX + 120)) Then
    Sound.Stop(Program.Directory + "/sounds/Hit metal 35.mp3")
Sound.Play(Program.Directory + "/sounds/Hit metal 35.mp3")  
  If x+8 &gt;= padX+80 Then
    Shapes.Rotate(paddle, 15)
  ElseIf x+8 &lt;= padX+40 then
    Shapes.Rotate(paddle, -15)
  Else
    Shapes.Rotate(paddle, 0)
    EndIf
  
  
  
  
    If x+8 &gt;= padX+40 And x+8 &lt;= padX + 80 then
      deltaY = -1*deltaY
    Else
      
       If (deltaX&gt;=0 And x+8&lt;=padX+40) Or (deltaX&lt;=0 And x+8&gt;=padX+80) then
       deltaX= -deltaX
       deltaY=-deltaY
       
       ElseIf (deltaX&gt;=0 And x+8&gt;=padX+80) then
         deltaY=-deltaY
         
       ElseIf (deltaX&lt;=0 And x+8&lt;=padX+40) then
         deltaY=-deltaY
       EndIf
       
        
    EndIf
EndIf 

EndSub

Sub savegame
  GraphicsWindow.BrushColor="Red"
  
    
     save = File.WriteContents(Program.Directory +"/BreakerV2.txt", level)
     
     If save="SUCCESS" Then
  Shapes.Remove(saveshape)
  saveshape = Shapes.AddText("GAme successfully saved! ")

Shapes.Move(saveshape, 200, 10)
Else
  Shapes.Remove(saveshape)
  saveshape = Shapes.AddText("There is an error! file cannot be saved ")  
  Shapes.Move(saveshape, 200, 10)  
   EndIf

 
  EndSub
  
  Sub loadgame
    
  GraphicsWindow.BrushColor="Red"
  
    
     level = File.ReadContents(Program.Directory +"/BreakerV2.txt")
     
     If save="SUCCESS" Or save="" Then
  Shapes.Remove(saveshape)
  saveshape = Shapes.AddText("GAme successfully loaded! ")
  Shapes.Move(saveshape, 200, 10)


  
  
ElseIf save="FAILED" then
  Shapes.Remove(saveshape)
  saveshape = Shapes.AddText("There is an error! game cannot be loaded ")  
  Shapes.Move(saveshape, 200, 10)
  
   EndIf

     
    EndSub
  
  
Sub Zvalue
          GraphicsWindow.BrushColor="Black"
   Shapes.Remove(zvalue)
   zvalue=Shapes.AddText("Z= "+z)
   Shapes.Move(zvalue, 400, 10)

EndSub
Sub OnMouseMove
paddleX = GraphicsWindow.MouseX
Shapes.Move(paddle, paddleX - 60, GraphicsWindow.Height - height)
EndSub

Sub PlayAgain

If win="False" Then  
  play=Shapes.AddText(" Do you want to play again?")
  Shapes.Move(play, gw/3+30,gh/2-40)
  GraphicsWindow.BrushColor = "Black"
yes = Controls.AddButton("Yes",gw/3,gh/2)
No = Controls.AddButton("No",gw*2/3,gh/2)

While Controls.LastClickedButton&lt;&gt;No And Controls.LastClickedButton &lt;&gt; yes

endwhile
EndIf

if Controls.LastClickedButton = yes Or win="True" then

CLS()
main()
Else
  Program.End()
endif
  
  
EndSub

Sub level2
  For i=0 To GraphicsWindow.Width Step 40
    For j=80 To 200  Step 40
       GraphicsWindow.BrushColor= GraphicsWindow.GetRandomColor()
     cube[i][j]=Shapes.AddRectangle(40, 40)
      
    Shapes.Animate(cube[i][j], i, j, 1000)
    EndFor
    EndFor
  EndSub
  
  Sub hitBlock
  For i=0 To 16*40 Step 40
    For j=0 To 280 Step 40
      nextif="True"
    If cube[i][j]&lt;&gt;0 Then 
      If ((y+8&lt;=Shapes.GetTop(cube[i][j]) And y+8&gt;= Shapes.GetTop(cube[i][j])-8) Or (y+8&gt;=Shapes.GetTop(cube[i][j])+40 And y+8&lt;= Shapes.GetTop(cube[i][j])+48)) And (x+8&gt;=Shapes.GetLeft(cube[i][j]) And x+8&lt;=Shapes.GetLeft(cube[i][j])+40) Then
        z=z+1
        Zvalue()
        Shapes.Remove(cube[i][j])
        cube[i][j]=0
        Sound.PlayClick()
        deltaY=-deltaY   
           nextif="False"
        ElseIf ((x+8&lt;=Shapes.GetLeft(cube[i][j]) And x+8&gt;= Shapes.GetLeft(cube[i][j])-8) Or (x+8&gt;=Shapes.GetLeft(cube[i][j])+40 And x+8&lt;= Shapes.GetLeft(cube[i][j])+48)) And (y+8&gt;=Shapes.GetTop(cube[i][j]) And y+8&lt;=Shapes.GetTop(cube[i][j])+40) And nextif="True" Then
        z=z+1
        Zvalue()
        Shapes.Remove(cube[i][j])
        cube[i][j]=0
        Sound.PlayClick()
        deltaX=-deltaX              
        
        

      EndIf
EndIf 



     EndFor
   EndFor

 EndSub
 
 Sub bonus
   gift = ImageList.LoadImage(Program.Directory+"pics/gift.jpg")
   Shapes.AddImage(gift)
   bonusX= Math.GetRandomNumber(gw)
   
  For j=-30 To gh Step (gh-78)/100
    Shapes.Move(gift, bonusX, j)
    
    If j= gh-48 And x&gt; padX And x&lt; padX+120 Then
      Sound.PlayChimes()
      
      EndIf
   EndFor
   
 EndSub
 
 
 Sub winner

If  (level=4 And (z= 23 Or z=136)) Or (level=5 And (z=39 Or z=136)) Or (level=2 And (z=64 Or z=144)) Or (level=3 And (z=36 Or z=135) ) Or (level=6 And  (z=136 Or z=135 Or z=58)) Or (level=1 And (z=120 Or z=136 Or z=40)) Then

            Sound.PlayBellRing()
     GraphicsWindow.ShowMessage("You won!","Congratulations!")
level=level+1     
     PlayAgain()
       EndIf
   
 EndSub
 
 Sub processkey
   If GraphicsWindow.LastKey="Oem3" Then
     TextWindow.WriteLine("Enter  your cheat code: ")
     cheatcode = TextWindow.Read()
      ElseIf GraphicsWindow.LastKey = "S" then
    savegame()
  ElseIf GraphicsWindow.LastKey= "L" then
    loadgame()
    EndIf
     
      If cheatcode = "nima" Then
          TextWindow.WriteLine("Enter your desired level: ")
          
          level=TextWindow.ReadNumber()
          TextWindow.WriteLine("Level select successful!")

         Elseif cheatcode="behnam" then
           TextWindow.WriteLine("Enter the Y-coordinate of speed to be adjusted: ")
           deltaY = TextWindow.ReadNumber()
           TextWindow.WriteLine("Enter the x-coordinate of ball speed to be adjusted: ")
           deltaX= TextWindow.ReadNumber()
           TextWindow.WriteLine("Ball speed adjusted!")
         elseif cheatcode = "shahab" then
           TextWindow.WriteLine("Enter the height of the paddle to be adjusted: ")
           height=TextWindow.ReadNumber()
           TextWindow.WriteLine("Paddle height adjusted!")
         elseif cheatcode = "sina" then
           TextWindow.WriteLine("Wow! you can go to the next level even if you lose?")
         level=level+1
    EndIf
    Program.Delay(5000)
    TextWindow.Hide()
    cheatcode=""
    GraphicsWindow.Show()

    
       
    
'
EndSub

 sub CLS
   z=0
   Shapes.Remove(saveshape)
     Shapes.Remove(paddle)
  Shapes.Remove(play)
  Controls.Remove(yes)
  Controls.Remove(No)
  Shapes.Remove(ball)
  For i=0 To 16*40 Step 40
    For j=0 To 280 Step 40
      
    Shapes.Remove(cube[i][j])
    EndFor
    EndFor
  EndSub
  
  Sub level1
    For i=0 To GraphicsWindow.Width Step 80
    For j=40 To 200 Step 40
GraphicsWindow.BrushColor= GraphicsWindow.GetColorFromRGB(j, j, j)  
  cube[i][j]=Shapes.AddRectangle(20, 20)
      
    Shapes.Animate(cube[i][j], i, j, 1000)
    EndFor
    EndFor
    
    
    
    
  EndSub
  
  
  Sub level3
    j=0
' GraphicsWindow.BrushColor="Green"   
          'For j=0 To GraphicsWindow.Height/2 Step 40
    For i=0 To 240 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      j=j+40
    EndFor
    
    
    
    i=0
        For j=120 To 260 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      i=i+40
       
      
      
    EndFor

    
        j=0

    For i=120 To 360 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      j=j+40
    EndFor


        j=0

    For i=240 To 480 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      j=j+40
    EndFor

 j=0
    For i=360 To 600 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      j=j+40
    EndFor

 j=0
    For i=480 To 600 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(225,100,i*20)
cube[i][j]=Shapes.AddEllipse(40, 40)
      
      Shapes.Animate(cube[i][j], i, j, 1000)
      j=j+40
    EndFor



  EndSub    
  
  
  Sub level4
    GraphicsWindow.BrushColor="Yellow"    
    
    For j=40 To 120 Step 40
      For i=0 To 160 Step 160
            cube[i][j]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[i][j], i, j, 1000)
    
    
      EndFor
    EndFor     
    
     j=40
      For i=40 To 120 Step 40
            cube[i][j]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[i][j], i, j, 1000)
    
    j=j+40
  EndFor
  
  i=240
  For j=0 To 120 Step 40
    If j&lt;&gt;40 Then
            cube[i][j]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[i][j], i, j, 1000)
    EndIf
   
      EndFor      
        
    For j=80 To 120 Step 40
      For i=320 To 480 Step 160
            cube[i][j]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[i][j], i, j, 1000)
    
    
      EndFor
    EndFor       

           cube[400][120]=Shapes.AddRectangle(40, 40)
           Shapes.Animate(cube[400][120], 400, 120, 1000)

           cube[440][80]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[440][80], 440, 80, 1000)

           cube[360][80]=Shapes.AddRectangle(40, 40)
            Shapes.Animate(cube[360][80], 360, 80, 1000)
            
            
            i=560
For j=80 To 120 Step 40
  
       cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)  
  EndFor
  
              i=600
For j=120 To 160 Step 40
  
       cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)  
  EndFor
            
  EndSub
  
  
  
  Sub level5

    For j=40 To 200 Step 80
    For i=40 To 540 Step 40
GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(i*20,j*20,0)
cube[i][j]=Shapes.AddRectangle(40, 40)
      
    Shapes.Animate(cube[i][j], i, j, 1000)      
      
  EndFor
  EndFor
    
    
  EndSub
  
  
  Sub level6
    
 For j=40 To 280 Step 200
    For i=40 To 540 Step 40
     GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(i*20,j*20,0)
     cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)      
      
  EndFor
EndFor

 For j=80 To 200 Step 120
    For i=120 To 460 Step 40
     GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(i*20,j*20,0)
     cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)      
      
  EndFor
EndFor

 For j=120 To 160 Step 40
    For i=120 To 440 Step 320
     GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(i*20,j*20,0)
     cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)      
      
  EndFor
EndFor

 For j=80 To 200 Step 40
    For i=40 To 520 Step 480
     GraphicsWindow.BrushColor = GraphicsWindow.GetColorFromRGB(i*20,j*20,0)
     cube[i][j]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[i][j], i, j, 1000)      
      
  EndFor
  EndFor    
    
    cube[280][120]=Shapes.AddRectangle(40, 40) 
    Shapes.Animate(cube[280][120], 280, 120, 1000)      
    
cube[280][160]=Shapes.AddRectangle(40, 40) 
Shapes.Animate(cube[280][160], 280, 160, 1000)   



    
  EndSub
  
  
  Sub gameend
   ' Controls.Remove(paddle)
    
    'TextWindow.WriteLine("IN the end")
   GraphicsWindow.Clear()
   congrats = ImageList.LoadImage(Program.Directory + "/pics/lastlevel.png")
    
    GraphicsWindow.DrawResizedImage(congrats,0, 0, GraphicsWindow.Width, GraphicsWindow.Height)
   
    start = Controls.AddButton("Start Over", 260, 420)
    
While Controls.LastClickedButton&lt;&gt;start 'And Controls.LastClickedButton&lt;&gt;Exit

EndWhile
Controls.Remove(start)
CLS()
level=1

menu()
    EndSub</PRE>
<DIV class=preview><PRE class=vbs>GraphicsWindow.CanResize=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
level=<SPAN class=vbScript__number>1</SPAN>&nbsp;
menu()&nbsp;
&nbsp;
<SPAN class=vbScript__com>'startover:</SPAN>&nbsp;
main()&nbsp;
&nbsp;
<SPAN class=vbScript__com>'------------------------------------------------&nbsp;&nbsp;&nbsp;SUBS&nbsp;---------------------------------------</SPAN>&nbsp;
sub&nbsp;main&nbsp;
deltaX&nbsp;=&nbsp;<SPAN class=vbScript__number>1</SPAN>&nbsp;
deltaY&nbsp;=&nbsp;<SPAN class=vbScript__number>1</SPAN>&nbsp;
height=&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.KeyDown&nbsp;=&nbsp;processkey&nbsp;
&nbsp;
&nbsp;&nbsp;win=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;level=<SPAN class=vbScript__number>1</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;level1()&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;level=<SPAN class=vbScript__number>2</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;level2()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;level=<SPAN class=vbScript__number>3</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level3()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;elseif&nbsp;level=<SPAN class=vbScript__number>4</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level4()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;elseif&nbsp;level=<SPAN class=vbScript__number>5</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level5()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;elseif&nbsp;level=<SPAN class=vbScript__number>6</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level6()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;gameend()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.DrawRectangle(gw/<SPAN class=vbScript__number>2</SPAN>,&nbsp;gh/<SPAN class=vbScript__number>2</SPAN>,&nbsp;<SPAN class=vbScript__number>200</SPAN>,&nbsp;<SPAN class=vbScript__number>200</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.DrawBoundText(gw/<SPAN class=vbScript__number>2</SPAN>,&nbsp;gh/<SPAN class=vbScript__number>2</SPAN>,&nbsp;<SPAN class=vbScript__number>198</SPAN>,&nbsp;<SPAN class=vbScript__string>"Congratulations!&nbsp;You&nbsp;won&nbsp;all&nbsp;levels!"</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;
GraphicsWindow.BrushColor=&nbsp;<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
&nbsp;&nbsp;Shapes.Remove(Slevel)&nbsp;
&nbsp;&nbsp;Slevel&nbsp;=&nbsp;Shapes.AddText(<SPAN class=vbScript__string>"Level:&nbsp;"</SPAN>+&nbsp;level)&nbsp;
Shapes.Move(Slevel,&nbsp;<SPAN class=vbScript__number>550</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;
GraphicsWindow.CanResize=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
<SPAN class=vbScript__com>'GraphicsWindow.BackgroundColor&nbsp;=&nbsp;"lightBlue"</SPAN>&nbsp;
&nbsp;
&nbsp;
paddle&nbsp;=&nbsp;Shapes.AddRectangle(<SPAN class=vbScript__number>120</SPAN>,&nbsp;<SPAN class=vbScript__number>12</SPAN>)&nbsp;
ball&nbsp;=&nbsp;Shapes.AddEllipse(<SPAN class=vbScript__number>16</SPAN>,&nbsp;<SPAN class=vbScript__number>16</SPAN>)&nbsp;
Shapes.Move(ball,&nbsp;-<SPAN class=vbScript__number>16</SPAN>,&nbsp;-<SPAN class=vbScript__number>16</SPAN>)&nbsp;
&nbsp;
gw&nbsp;=&nbsp;GraphicsWindow.Width&nbsp;
gh&nbsp;=&nbsp;GraphicsWindow.Height&nbsp;
bkg&nbsp;=&nbsp;ImageList.LoadImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/pics/metal.jpg"</SPAN>)&nbsp;
GraphicsWindow.DrawResizedImage(bkg,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;gw,&nbsp;gh)&nbsp;
&nbsp;
GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
GraphicsWindow.DrawText(<SPAN class=vbScript__number>10</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>,<SPAN class=vbScript__string>"Developed&nbsp;by&nbsp;Behnam&nbsp;Azizi"</SPAN>)&nbsp;
GraphicsWindow.BrushColor=&nbsp;GraphicsWindow.GetRandomColor()&nbsp;
GraphicsWindow.MouseMove&nbsp;=&nbsp;OnMouseMove&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
x&nbsp;=&nbsp;<SPAN class=vbScript__number>2</SPAN>&nbsp;
y&nbsp;=&nbsp;gh<SPAN class=vbScript__number>-48</SPAN>&nbsp;
<SPAN class=vbScript__com>'Timer.Interval=&nbsp;1000</SPAN>&nbsp;
&nbsp;
GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
play=Controls.AddButton(<SPAN class=vbScript__string>"Press&nbsp;to&nbsp;Play!"</SPAN>,gw/<SPAN class=vbScript__number>2</SPAN><SPAN class=vbScript__number>-50</SPAN>,&nbsp;gh/<SPAN class=vbScript__number>2</SPAN>)&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>While</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;play&nbsp;
&nbsp;
endwhile&nbsp;
&nbsp;
Controls.Remove(play)&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
RunLoop:&nbsp;
hitBlock()&nbsp;
winner()&nbsp;
x&nbsp;=&nbsp;x&nbsp;+&nbsp;deltaX&nbsp;
y&nbsp;=&nbsp;y&nbsp;-&nbsp;deltaY&nbsp;
&nbsp;
Program.Delay(<SPAN class=vbScript__number>1</SPAN>)&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;(x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&gt;=&nbsp;gw&nbsp;-&nbsp;<SPAN class=vbScript__number>9</SPAN>&nbsp;or&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&lt;=&nbsp;<SPAN class=vbScript__number>9</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
deltaX&nbsp;=&nbsp;-<SPAN class=vbScript__number>1</SPAN>*deltaX&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;(y<SPAN class=vbScript__number>+8</SPAN>&nbsp;&lt;=&nbsp;<SPAN class=vbScript__number>8</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
deltaY&nbsp;=&nbsp;-<SPAN class=vbScript__number>1</SPAN>*deltaY&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
paddlehit()&nbsp;&nbsp;
&nbsp;&nbsp;
Shapes.Move(ball,&nbsp;x,&nbsp;y)&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;(y&nbsp;&lt;&nbsp;gh)&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
Goto&nbsp;RunLoop&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
Sound.Play(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Error.mp3"</SPAN>)&nbsp;
GraphicsWindow.ShowMessage(<SPAN class=vbScript__string>"You&nbsp;Lose"</SPAN>,&nbsp;<SPAN class=vbScript__string>"Paddle"</SPAN>)&nbsp;
win=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
PlayAgain()&nbsp;
deltaY=-<SPAN class=vbScript__number>1</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__com>'----------------------------------------------&nbsp;&nbsp;&nbsp;SUBROUTINES&nbsp;------------------------------------</SPAN>&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;menu&nbsp;
&nbsp;&nbsp;Sound.Play(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Menu&nbsp;music.mp3"</SPAN>)&nbsp;
&nbsp;&nbsp;menubkg&nbsp;=&nbsp;ImageList.LoadImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/pics/menu.jpg"</SPAN>)&nbsp;
GraphicsWindow.DrawResizedImage(menubkg,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;GraphicsWindow.Width,&nbsp;GraphicsWindow.Height)&nbsp;
&nbsp;&nbsp;start=Controls.AddButton(<SPAN class=vbScript__string>"Start"</SPAN>,&nbsp;<SPAN class=vbScript__number>260</SPAN>,&nbsp;<SPAN class=vbScript__number>160</SPAN>)&nbsp;
&nbsp;&nbsp;instructions=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"Instructions"</SPAN>,&nbsp;<SPAN class=vbScript__number>260</SPAN>,&nbsp;<SPAN class=vbScript__number>200</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Exit</SPAN>&nbsp;=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"Exit"</SPAN>,&nbsp;<SPAN class=vbScript__number>260</SPAN>,&nbsp;<SPAN class=vbScript__number>240</SPAN>)&nbsp;
&nbsp;
&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>While</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;start&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;instructions&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;<SPAN class=vbScript__keyword>Exit</SPAN>&nbsp;
&nbsp;
EndWhile&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;Controls.LastClickedButton=<SPAN class=vbScript__keyword>Exit</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;Program.<SPAN class=vbScript__keyword>End</SPAN>()&nbsp;
<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;Controls.LastClickedButton=instructions&nbsp;then&nbsp;
&nbsp;&nbsp;instructionspage()&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;
&nbsp;
GraphicsWindow.Clear()&nbsp;
Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Menu&nbsp;music.mp3"</SPAN>)&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;instructionspage&nbsp;
&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
&nbsp;instr=&nbsp;ImageList.LoadImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/pics/instructions.jpg"</SPAN>)&nbsp;
&nbsp;&nbsp;GraphicsWindow.DrawResizedImage(instr,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,GraphicsWindow.Width,&nbsp;GraphicsWindow.Height)&nbsp;
&nbsp;&nbsp;back&nbsp;=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"&lt;---&nbsp;Back"</SPAN>,&nbsp;<SPAN class=vbScript__number>50</SPAN>,&nbsp;<SPAN class=vbScript__number>400</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>While</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;back&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndWhile&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;menu()&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;paddlehit&nbsp;
&nbsp;&nbsp;padX&nbsp;=&nbsp;Shapes.GetLeft&nbsp;(paddle)&nbsp;
&nbsp;&nbsp;padY=&nbsp;Shapes.GetTop(paddle)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;(y<SPAN class=vbScript__number>+8</SPAN>&gt;=&nbsp;padY<SPAN class=vbScript__number>-8</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;y<SPAN class=vbScript__number>+8</SPAN>&lt;=&nbsp;padY<SPAN class=vbScript__number>+12</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&gt;=&nbsp;padX<SPAN class=vbScript__number>-8</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&lt;=&nbsp;padX&nbsp;+&nbsp;<SPAN class=vbScript__number>120</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Sound.<SPAN class=vbScript__keyword>Stop</SPAN>(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Hit&nbsp;metal&nbsp;35.mp3"</SPAN>)&nbsp;
Sound.Play(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/sounds/Hit&nbsp;metal&nbsp;35.mp3"</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&gt;=&nbsp;padX<SPAN class=vbScript__number>+80</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Rotate(paddle,&nbsp;<SPAN class=vbScript__number>15</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&lt;=&nbsp;padX<SPAN class=vbScript__number>+40</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Rotate(paddle,&nbsp;-<SPAN class=vbScript__number>15</SPAN>)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Rotate(paddle,&nbsp;<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&gt;=&nbsp;padX<SPAN class=vbScript__number>+40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&nbsp;&lt;=&nbsp;padX&nbsp;+&nbsp;<SPAN class=vbScript__number>80</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY&nbsp;=&nbsp;-<SPAN class=vbScript__number>1</SPAN>*deltaY&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;(deltaX&gt;=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&lt;=padX<SPAN class=vbScript__number>+40</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(deltaX&lt;=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&gt;=padX<SPAN class=vbScript__number>+80</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaX=&nbsp;-deltaX&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY=-deltaY&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;(deltaX&gt;=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&gt;=padX<SPAN class=vbScript__number>+80</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY=-deltaY&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;(deltaX&lt;=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&lt;=padX<SPAN class=vbScript__number>+40</SPAN>)&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY=-deltaY&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;
&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;savegame&nbsp;
&nbsp;&nbsp;GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Red"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;save&nbsp;=&nbsp;File.WriteContents(Program.Directory&nbsp;+<SPAN class=vbScript__string>"/BreakerV2.txt"</SPAN>,&nbsp;level)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;save=<SPAN class=vbScript__string>"SUCCESS"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;Shapes.Remove(saveshape)&nbsp;
&nbsp;&nbsp;saveshape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=vbScript__string>"GAme&nbsp;successfully&nbsp;saved!&nbsp;"</SPAN>)&nbsp;
&nbsp;
Shapes.Move(saveshape,&nbsp;<SPAN class=vbScript__number>200</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;
<SPAN class=vbScript__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;Shapes.Remove(saveshape)&nbsp;
&nbsp;&nbsp;saveshape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=vbScript__string>"There&nbsp;is&nbsp;an&nbsp;error!&nbsp;file&nbsp;cannot&nbsp;be&nbsp;saved&nbsp;"</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;Shapes.Move(saveshape,&nbsp;<SPAN class=vbScript__number>200</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;loadgame&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Red"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level&nbsp;=&nbsp;File.ReadContents(Program.Directory&nbsp;+<SPAN class=vbScript__string>"/BreakerV2.txt"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;save=<SPAN class=vbScript__string>"SUCCESS"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;save=<SPAN class=vbScript__string>""</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;Shapes.Remove(saveshape)&nbsp;
&nbsp;&nbsp;saveshape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=vbScript__string>"GAme&nbsp;successfully&nbsp;loaded!&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(saveshape,&nbsp;<SPAN class=vbScript__number>200</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;save=<SPAN class=vbScript__string>"FAILED"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;Shapes.Remove(saveshape)&nbsp;
&nbsp;&nbsp;saveshape&nbsp;=&nbsp;Shapes.AddText(<SPAN class=vbScript__string>"There&nbsp;is&nbsp;an&nbsp;error!&nbsp;game&nbsp;cannot&nbsp;be&nbsp;loaded&nbsp;"</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;Shapes.Move(saveshape,&nbsp;<SPAN class=vbScript__number>200</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;Zvalue&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.Remove(zvalue)&nbsp;
&nbsp;&nbsp;&nbsp;zvalue=Shapes.AddText(<SPAN class=vbScript__string>"Z=&nbsp;"</SPAN>+z)&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.Move(zvalue,&nbsp;<SPAN class=vbScript__number>400</SPAN>,&nbsp;<SPAN class=vbScript__number>10</SPAN>)&nbsp;
&nbsp;
EndSub&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;OnMouseMove&nbsp;
paddleX&nbsp;=&nbsp;GraphicsWindow.MouseX&nbsp;
Shapes.Move(paddle,&nbsp;paddleX&nbsp;-&nbsp;<SPAN class=vbScript__number>60</SPAN>,&nbsp;GraphicsWindow.Height&nbsp;-&nbsp;height)&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;PlayAgain&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;win=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;play=Shapes.AddText(<SPAN class=vbScript__string>"&nbsp;Do&nbsp;you&nbsp;want&nbsp;to&nbsp;play&nbsp;again?"</SPAN>)&nbsp;
&nbsp;&nbsp;Shapes.Move(play,&nbsp;gw/<SPAN class=vbScript__number>3</SPAN><SPAN class=vbScript__number>+30</SPAN>,gh/<SPAN class=vbScript__number>2</SPAN><SPAN class=vbScript__number>-40</SPAN>)&nbsp;
&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;<SPAN class=vbScript__string>"Black"</SPAN>&nbsp;
yes&nbsp;=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"Yes"</SPAN>,gw/<SPAN class=vbScript__number>3</SPAN>,gh/<SPAN class=vbScript__number>2</SPAN>)&nbsp;
No&nbsp;=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"No"</SPAN>,gw*<SPAN class=vbScript__number>2</SPAN>/<SPAN class=vbScript__number>3</SPAN>,gh/<SPAN class=vbScript__number>2</SPAN>)&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>While</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;No&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;Controls.LastClickedButton&nbsp;&lt;&gt;&nbsp;yes&nbsp;
&nbsp;
endwhile&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;
if&nbsp;Controls.LastClickedButton&nbsp;=&nbsp;yes&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;win=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;then&nbsp;
&nbsp;
CLS()&nbsp;
main()&nbsp;
<SPAN class=vbScript__keyword>Else</SPAN>&nbsp;
&nbsp;&nbsp;Program.<SPAN class=vbScript__keyword>End</SPAN>()&nbsp;
endif&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
EndSub&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level2&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;GraphicsWindow.Width&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>80</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor=&nbsp;GraphicsWindow.GetRandomColor()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;hitBlock&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>16</SPAN>*<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>280</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nextif=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;cube[i][j]&lt;&gt;<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;((y<SPAN class=vbScript__number>+8</SPAN>&lt;=Shapes.GetTop(cube[i][j])&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;y<SPAN class=vbScript__number>+8</SPAN>&gt;=&nbsp;Shapes.GetTop(cube[i][j])-<SPAN class=vbScript__number>8</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(y<SPAN class=vbScript__number>+8</SPAN>&gt;=Shapes.GetTop(cube[i][j])+<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;y<SPAN class=vbScript__number>+8</SPAN>&lt;=&nbsp;Shapes.GetTop(cube[i][j])+<SPAN class=vbScript__number>48</SPAN>))&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(x<SPAN class=vbScript__number>+8</SPAN>&gt;=Shapes.GetLeft(cube[i][j])&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&lt;=Shapes.GetLeft(cube[i][j])+<SPAN class=vbScript__number>40</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z=z<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zvalue()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(cube[i][j])&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY=-deltaY&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nextif=<SPAN class=vbScript__string>"False"</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;((x<SPAN class=vbScript__number>+8</SPAN>&lt;=Shapes.GetLeft(cube[i][j])&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&gt;=&nbsp;Shapes.GetLeft(cube[i][j])-<SPAN class=vbScript__number>8</SPAN>)&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(x<SPAN class=vbScript__number>+8</SPAN>&gt;=Shapes.GetLeft(cube[i][j])+<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x<SPAN class=vbScript__number>+8</SPAN>&lt;=&nbsp;Shapes.GetLeft(cube[i][j])+<SPAN class=vbScript__number>48</SPAN>))&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(y<SPAN class=vbScript__number>+8</SPAN>&gt;=Shapes.GetTop(cube[i][j])&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;y<SPAN class=vbScript__number>+8</SPAN>&lt;=Shapes.GetTop(cube[i][j])+<SPAN class=vbScript__number>40</SPAN>)&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;nextif=<SPAN class=vbScript__string>"True"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z=z<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zvalue()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(cube[i][j])&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.PlayClick()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaX=-deltaX&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;EndSub&nbsp;
&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;bonus&nbsp;
&nbsp;&nbsp;&nbsp;gift&nbsp;=&nbsp;ImageList.LoadImage(Program.Directory+<SPAN class=vbScript__string>"pics/gift.jpg"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.AddImage(gift)&nbsp;
&nbsp;&nbsp;&nbsp;bonusX=&nbsp;Math.GetRandomNumber(gw)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=-<SPAN class=vbScript__number>30</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;gh&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;(gh<SPAN class=vbScript__number>-78</SPAN>)/<SPAN class=vbScript__number>100</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Move(gift,&nbsp;bonusX,&nbsp;j)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;j=&nbsp;gh<SPAN class=vbScript__number>-48</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x&gt;&nbsp;padX&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;x&lt;&nbsp;padX<SPAN class=vbScript__number>+120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.PlayChimes()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;EndSub&nbsp;
&nbsp;&nbsp;
&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;winner&nbsp;
&nbsp;
<SPAN class=vbScript__keyword>If</SPAN>&nbsp;&nbsp;(level=<SPAN class=vbScript__number>4</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(z=&nbsp;<SPAN class=vbScript__number>23</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>136</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(level=<SPAN class=vbScript__number>5</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(z=<SPAN class=vbScript__number>39</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>136</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(level=<SPAN class=vbScript__number>2</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(z=<SPAN class=vbScript__number>64</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>144</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(level=<SPAN class=vbScript__number>3</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(z=<SPAN class=vbScript__number>36</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>135</SPAN>)&nbsp;)&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(level=<SPAN class=vbScript__number>6</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;&nbsp;(z=<SPAN class=vbScript__number>136</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>135</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>58</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;(level=<SPAN class=vbScript__number>1</SPAN>&nbsp;<SPAN class=vbScript__keyword>And</SPAN>&nbsp;(z=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>136</SPAN>&nbsp;<SPAN class=vbScript__keyword>Or</SPAN>&nbsp;z=<SPAN class=vbScript__number>40</SPAN>))&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sound.PlayBellRing()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.ShowMessage(<SPAN class=vbScript__string>"You&nbsp;won!"</SPAN>,<SPAN class=vbScript__string>"Congratulations!"</SPAN>)&nbsp;
level=level<SPAN class=vbScript__number>+1</SPAN>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PlayAgain()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;EndSub&nbsp;
&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;processkey&nbsp;
&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;GraphicsWindow.LastKey=<SPAN class=vbScript__string>"Oem3"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Enter&nbsp;&nbsp;your&nbsp;cheat&nbsp;code:&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cheatcode&nbsp;=&nbsp;TextWindow.Read()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;GraphicsWindow.LastKey&nbsp;=&nbsp;<SPAN class=vbScript__string>"S"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;savegame()&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>ElseIf</SPAN>&nbsp;GraphicsWindow.LastKey=&nbsp;<SPAN class=vbScript__string>"L"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;loadgame()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;cheatcode&nbsp;=&nbsp;<SPAN class=vbScript__string>"nima"</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Enter&nbsp;your&nbsp;desired&nbsp;level:&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level=TextWindow.ReadNumber()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Level&nbsp;select&nbsp;successful!"</SPAN>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Elseif&nbsp;cheatcode=<SPAN class=vbScript__string>"behnam"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Enter&nbsp;the&nbsp;Y-coordinate&nbsp;of&nbsp;speed&nbsp;to&nbsp;be&nbsp;adjusted:&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaY&nbsp;=&nbsp;TextWindow.ReadNumber()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Enter&nbsp;the&nbsp;x-coordinate&nbsp;of&nbsp;ball&nbsp;speed&nbsp;to&nbsp;be&nbsp;adjusted:&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deltaX=&nbsp;TextWindow.ReadNumber()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Ball&nbsp;speed&nbsp;adjusted!"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;elseif&nbsp;cheatcode&nbsp;=&nbsp;<SPAN class=vbScript__string>"shahab"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Enter&nbsp;the&nbsp;height&nbsp;of&nbsp;the&nbsp;paddle&nbsp;to&nbsp;be&nbsp;adjusted:&nbsp;"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;height=TextWindow.ReadNumber()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Paddle&nbsp;height&nbsp;adjusted!"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;elseif&nbsp;cheatcode&nbsp;=&nbsp;<SPAN class=vbScript__string>"sina"</SPAN>&nbsp;then&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.WriteLine(<SPAN class=vbScript__string>"Wow!&nbsp;you&nbsp;can&nbsp;go&nbsp;to&nbsp;the&nbsp;next&nbsp;level&nbsp;even&nbsp;if&nbsp;you&nbsp;lose?"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;level=level<SPAN class=vbScript__number>+1</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Program.Delay(<SPAN class=vbScript__number>5000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;TextWindow.Hide()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;cheatcode=<SPAN class=vbScript__string>""</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.Show()&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__com>'</SPAN>&nbsp;
EndSub&nbsp;
&nbsp;
&nbsp;sub&nbsp;CLS&nbsp;
&nbsp;&nbsp;&nbsp;z=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;Shapes.Remove(saveshape)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(paddle)&nbsp;
&nbsp;&nbsp;Shapes.Remove(play)&nbsp;
&nbsp;&nbsp;Controls.Remove(yes)&nbsp;
&nbsp;&nbsp;Controls.Remove(No)&nbsp;
&nbsp;&nbsp;Shapes.Remove(ball)&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>16</SPAN>*<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>280</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Remove(cube[i][j])&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level1&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;GraphicsWindow.Width&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>80</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor=&nbsp;GraphicsWindow.GetColorFromRGB(j,&nbsp;j,&nbsp;j)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>20</SPAN>,&nbsp;<SPAN class=vbScript__number>20</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level3&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
<SPAN class=vbScript__com>'&nbsp;GraphicsWindow.BrushColor="Green"&nbsp;&nbsp;&nbsp;</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'For&nbsp;j=0&nbsp;To&nbsp;GraphicsWindow.Height/2&nbsp;Step&nbsp;40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>240</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>260</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i=i<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>360</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>240</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>480</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>360</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>600</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>480</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>600</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(<SPAN class=vbScript__number>225</SPAN>,<SPAN class=vbScript__number>100</SPAN>,i*<SPAN class=vbScript__number>20</SPAN>)&nbsp;
cube[i][j]=Shapes.AddEllipse(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;EndSub&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level4&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor=<SPAN class=vbScript__string>"Yellow"</SPAN>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>160</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>160</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;j=<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;j=j<SPAN class=vbScript__number>+40</SPAN>&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;i=<SPAN class=vbScript__number>240</SPAN>&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>0</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>If</SPAN>&nbsp;j&lt;&gt;<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>Then</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>EndIf</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>80</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>320</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>480</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>160</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndFor&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[<SPAN class=vbScript__number>400</SPAN>][<SPAN class=vbScript__number>120</SPAN>]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[<SPAN class=vbScript__number>400</SPAN>][<SPAN class=vbScript__number>120</SPAN>],&nbsp;<SPAN class=vbScript__number>400</SPAN>,&nbsp;<SPAN class=vbScript__number>120</SPAN>,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[<SPAN class=vbScript__number>440</SPAN>][<SPAN class=vbScript__number>80</SPAN>]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[<SPAN class=vbScript__number>440</SPAN>][<SPAN class=vbScript__number>80</SPAN>],&nbsp;<SPAN class=vbScript__number>440</SPAN>,&nbsp;<SPAN class=vbScript__number>80</SPAN>,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[<SPAN class=vbScript__number>360</SPAN>][<SPAN class=vbScript__number>80</SPAN>]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[<SPAN class=vbScript__number>360</SPAN>][<SPAN class=vbScript__number>80</SPAN>],&nbsp;<SPAN class=vbScript__number>360</SPAN>,&nbsp;<SPAN class=vbScript__number>80</SPAN>,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i=<SPAN class=vbScript__number>560</SPAN>&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>80</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i=<SPAN class=vbScript__number>600</SPAN>&nbsp;
<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>160</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level5&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>80</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>540</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(i*<SPAN class=vbScript__number>20</SPAN>,j*<SPAN class=vbScript__number>20</SPAN>,<SPAN class=vbScript__number>0</SPAN>)&nbsp;
cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;level6&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>280</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>540</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(i*<SPAN class=vbScript__number>20</SPAN>,j*<SPAN class=vbScript__number>20</SPAN>,<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
EndFor&nbsp;
&nbsp;
&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>80</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>120</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>460</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(i*<SPAN class=vbScript__number>20</SPAN>,j*<SPAN class=vbScript__number>20</SPAN>,<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
EndFor&nbsp;
&nbsp;
&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>160</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>120</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>440</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>320</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(i*<SPAN class=vbScript__number>20</SPAN>,j*<SPAN class=vbScript__number>20</SPAN>,<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
EndFor&nbsp;
&nbsp;
&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;j=<SPAN class=vbScript__number>80</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>200</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>40</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__keyword>For</SPAN>&nbsp;i=<SPAN class=vbScript__number>40</SPAN>&nbsp;<SPAN class=vbScript__keyword>To</SPAN>&nbsp;<SPAN class=vbScript__number>520</SPAN>&nbsp;<SPAN class=vbScript__keyword>Step</SPAN>&nbsp;<SPAN class=vbScript__number>480</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.BrushColor&nbsp;=&nbsp;GraphicsWindow.GetColorFromRGB(i*<SPAN class=vbScript__number>20</SPAN>,j*<SPAN class=vbScript__number>20</SPAN>,<SPAN class=vbScript__number>0</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cube[i][j]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[i][j],&nbsp;i,&nbsp;j,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndFor&nbsp;
&nbsp;&nbsp;EndFor&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;cube[<SPAN class=vbScript__number>280</SPAN>][<SPAN class=vbScript__number>120</SPAN>]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Shapes.Animate(cube[<SPAN class=vbScript__number>280</SPAN>][<SPAN class=vbScript__number>120</SPAN>],&nbsp;<SPAN class=vbScript__number>280</SPAN>,&nbsp;<SPAN class=vbScript__number>120</SPAN>,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cube[<SPAN class=vbScript__number>280</SPAN>][<SPAN class=vbScript__number>160</SPAN>]=Shapes.AddRectangle(<SPAN class=vbScript__number>40</SPAN>,&nbsp;<SPAN class=vbScript__number>40</SPAN>)&nbsp;&nbsp;
Shapes.Animate(cube[<SPAN class=vbScript__number>280</SPAN>][<SPAN class=vbScript__number>160</SPAN>],&nbsp;<SPAN class=vbScript__number>280</SPAN>,&nbsp;<SPAN class=vbScript__number>160</SPAN>,&nbsp;<SPAN class=vbScript__number>1000</SPAN>)&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;EndSub&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;<SPAN class=vbScript__keyword>Sub</SPAN>&nbsp;gameend&nbsp;
&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'&nbsp;Controls.Remove(paddle)</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<SPAN class=vbScript__com>'TextWindow.WriteLine("IN&nbsp;the&nbsp;end")</SPAN>&nbsp;
&nbsp;&nbsp;&nbsp;GraphicsWindow.Clear()&nbsp;
&nbsp;&nbsp;&nbsp;congrats&nbsp;=&nbsp;ImageList.LoadImage(Program.Directory&nbsp;+&nbsp;<SPAN class=vbScript__string>"/pics/lastlevel.png"</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;GraphicsWindow.DrawResizedImage(congrats,<SPAN class=vbScript__number>0</SPAN>,&nbsp;<SPAN class=vbScript__number>0</SPAN>,&nbsp;GraphicsWindow.Width,&nbsp;GraphicsWindow.Height)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;start&nbsp;=&nbsp;Controls.AddButton(<SPAN class=vbScript__string>"Start&nbsp;Over"</SPAN>,&nbsp;<SPAN class=vbScript__number>260</SPAN>,&nbsp;<SPAN class=vbScript__number>420</SPAN>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<SPAN class=vbScript__keyword>While</SPAN>&nbsp;Controls.LastClickedButton&lt;&gt;start&nbsp;<SPAN class=vbScript__com>'And&nbsp;Controls.LastClickedButton&lt;&gt;Exit</SPAN>&nbsp;
&nbsp;
EndWhile&nbsp;
Controls.Remove(start)&nbsp;
CLS()&nbsp;
level=<SPAN class=vbScript__number>1</SPAN>&nbsp;
&nbsp;
menu()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;EndSub</PRE></DIV></DIV></DIV>
<DIV class=endscriptcode>&nbsp;</DIV><BR></EM>
<P></P></DIV>
