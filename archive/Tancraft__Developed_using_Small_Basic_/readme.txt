Here is another game that I made using small basic. I named it Tancraft. It is a 2-player game you can play with one of you friends.
I am so thankful to Litdev for his awesome extensions. I used his extension to use an animated image (the explosion of the tanks) in my game.
  At the beginning each player places their tanks anywhere on their own land (lands are seperated with the red line), and then starting from the top player you click somewhere in you own land. Once you click there the corresponding point on the other side of the red line willl be shot. If there is enemy's tank there the tank would explode.
You can download the game from here (at the top of the page)
And please don't expect to see a super amazing game! I did all the programming on my own. This was done only for learning purposes.
-----------------------------------------------------------
Challenges that I had while developing this game:
Compared to my other game projects in Small Basic, this was a simple one. Once one of the players clicks somewhere on the screen the program finds the corresponding point on the opponensts land with respect to the lined breaking between the two lands. Then if there is a tank in approximity it would explode!!!

 
Here is the source code:
 
VB Script
Edit|Remove
vbs 
GraphicsWindow.Width=500
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

If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then
      Shapes.Animate(ammo, math.GetRandomNumber(500), 540, 300)
      

    EndIf   
  

EndSub

sub handleMouse

xpos= GraphicsWindow.MouseX 
ypos= GraphicsWindow.MouseY

'If t=20 Then
'    rocket()
'    EndIf



If t<=8 And ypos<250 Then
  
start1()
t=t+1
ElseIf t<=17 and t>=9 and ypos>250 then
  
  start2()
t=t+1
ElseIf t>=18 then
  
  'Shapes.HideShape(tankA[2])
  
  If Math.Remainder(t, 2)=0 And ypos<250 Then
    Player1()
    winner()
  t=t+1
  ElseIf Math.Remainder(t, 2)=1 And ypos>250 Then
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

If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then
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
     If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then
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
    
    EndSubGraphicsWindow.Width=500 
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
 
If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then 
      Shapes.Animate(ammo, math.GetRandomNumber(500), 540, 300) 
       
 
    EndIf    
   
 
EndSub 
 
sub handleMouse 
 
xpos= GraphicsWindow.MouseX  
ypos= GraphicsWindow.MouseY 
 
'If t=20 Then 
'    rocket() 
'    EndIf 
 
 
 
If t<=8 And ypos<250 Then 
   
start1() 
t=t+1 
ElseIf t<=17 and t>=9 and ypos>250 then 
   
  start2() 
t=t+1 
ElseIf t>=18 then 
   
  'Shapes.HideShape(tankA[2]) 
   
  If Math.Remainder(t, 2)=0 And ypos<250 Then 
    Player1() 
    winner() 
  t=t+1 
  ElseIf Math.Remainder(t, 2)=1 And ypos>250 Then 
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
 
If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then 
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
     If xpos>x And xpos<x+40 And ypos<500-y And ypos>460-y Then 
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
     
    EndSub 
