Finally, the ultimate version of the Block Smasher is out! download it from here and play. It has 6 distinct levels and I added the save/load feature. So once tired, you are able to save the game and play the rest anytime you wish. Note that it might take a while for the game to save/load once you press S/L and the loaded game would not resume until you lose the current level once. I also added cheat codes to the game for more fun.  You will get the cheat codes once you finish the game (And please don't cheat to find the cheat codes! Play the game thoroughly!).
One of the special features I added to this game is that the paddle changes direction when hit by the ball depending on the side of the paddle that is hit by the ball. For example if the ball hits the right side of the paddle, the paddle rotates 20 degrees to the right.
Here is just an alternate download link: https://www.dropbox.com/s/1qz78voduciajr1/Breaker%20V%202.0.zip
And please don't expect to see a super amazing game! I did all the programming on my own. This was done only for learning purposes.
------------------------------------------------------
Challenges that I had while developing this game:
At each instance the program checks to see whether there has been a collision between the ball and each of the blocks. To accomplish this I created an array (matrix or whatever they call it!) holding the information about all blocks. And then constantly the program can theck if each of the blocks have been smashed by the ball. Now it doesn`t all end here: once there has been a collision betweent the ball and a block, the program should bounce the ball based on the angle from which the ball hits the square. Look at the code to see how I did this!
 
 
 
 
Also please note that some of the sounds and pictures used in the game are not mine. I downloaded the sound used in the main menu from here:
http://www.newgrounds.com/audio/listen/199965
Here is the source code:
 
 
 
 
VB Script
Edit|Remove
vbs 
GraphicsWindow.CanResize="False"
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

While Controls.LastClickedButton<>play

endwhile

Controls.Remove(play)





RunLoop:
hitBlock()
winner()
x = x + deltaX
y = y - deltaY

Program.Delay(1)
If (x+8 >= gw - 9 or x+8 <= 9) Then
deltaX = -1*deltaX
EndIf

If (y+8 <= 8) Then
deltaY = -1*deltaY
EndIf

paddlehit() 
 
Shapes.Move(ball, x, y)

If (y < gh) Then
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



While Controls.LastClickedButton<>start And Controls.LastClickedButton<>instructions And Controls.LastClickedButton<>Exit

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
  back = Controls.AddButton("<--- Back", 50, 400)
  
  While Controls.LastClickedButton<>back
    
    EndWhile
  
    GraphicsWindow.Clear()
    menu()
  
  
  EndSub

Sub paddlehit
  padX = Shapes.GetLeft (paddle)
  padY= Shapes.GetTop(paddle)
  If (y+8>= padY-8 And y+8<= padY+12 And (x+8 >= padX-8 And x+8 <= padX + 120)) Then
    Sound.Stop(Program.Directory + "/sounds/Hit metal 35.mp3")
Sound.Play(Program.Directory + "/sounds/Hit metal 35.mp3")  
  If x+8 >= padX+80 Then
    Shapes.Rotate(paddle, 15)
  ElseIf x+8 <= padX+40 then
    Shapes.Rotate(paddle, -15)
  Else
    Shapes.Rotate(paddle, 0)
    EndIf
  
  
  
  
    If x+8 >= padX+40 And x+8 <= padX + 80 then
      deltaY = -1*deltaY
    Else
      
       If (deltaX>=0 And x+8<=padX+40) Or (deltaX<=0 And x+8>=padX+80) then
       deltaX= -deltaX
       deltaY=-deltaY
       
       ElseIf (deltaX>=0 And x+8>=padX+80) then
         deltaY=-deltaY
         
       ElseIf (deltaX<=0 And x+8<=padX+40) then
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

While Controls.LastClickedButton<>No And Controls.LastClickedButton <> yes

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
    If cube[i][j]<>0 Then 
      If ((y+8<=Shapes.GetTop(cube[i][j]) And y+8>= Shapes.GetTop(cube[i][j])-8) Or (y+8>=Shapes.GetTop(cube[i][j])+40 And y+8<= Shapes.GetTop(cube[i][j])+48)) And (x+8>=Shapes.GetLeft(cube[i][j]) And x+8<=Shapes.GetLeft(cube[i][j])+40) Then
        z=z+1
        Zvalue()
        Shapes.Remove(cube[i][j])
        cube[i][j]=0
        Sound.PlayClick()
        deltaY=-deltaY   
           nextif="False"
        ElseIf ((x+8<=Shapes.GetLeft(cube[i][j]) And x+8>= Shapes.GetLeft(cube[i][j])-8) Or (x+8>=Shapes.GetLeft(cube[i][j])+40 And x+8<= Shapes.GetLeft(cube[i][j])+48)) And (y+8>=Shapes.GetTop(cube[i][j]) And y+8<=Shapes.GetTop(cube[i][j])+40) And nextif="True" Then
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
    
    If j= gh-48 And x> padX And x< padX+120 Then
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
    If j<>40 Then
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
    
While Controls.LastClickedButton<>start 'And Controls.LastClickedButton<>Exit

EndWhile
Controls.Remove(start)
CLS()
level=1

menu()
    EndSubGraphicsWindow.CanResize="False" 
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
 
While Controls.LastClickedButton<>play 
 
endwhile 
 
Controls.Remove(play) 
 
 
 
 
 
RunLoop: 
hitBlock() 
winner() 
x = x + deltaX 
y = y - deltaY 
 
Program.Delay(1) 
If (x+8 >= gw - 9 or x+8 <= 9) Then 
deltaX = -1*deltaX 
EndIf 
 
If (y+8 <= 8) Then 
deltaY = -1*deltaY 
EndIf 
 
paddlehit()  
  
Shapes.Move(ball, x, y) 
 
If (y < gh) Then 
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
 
 
 
While Controls.LastClickedButton<>start And Controls.LastClickedButton<>instructions And Controls.LastClickedButton<>Exit 
 
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
  back = Controls.AddButton("<--- Back", 50, 400) 
   
  While Controls.LastClickedButton<>back 
     
    EndWhile 
   
    GraphicsWindow.Clear() 
    menu() 
   
   
  EndSub 
 
Sub paddlehit 
  padX = Shapes.GetLeft (paddle) 
  padY= Shapes.GetTop(paddle) 
  If (y+8>= padY-8 And y+8<= padY+12 And (x+8 >= padX-8 And x+8 <= padX + 120)) Then 
    Sound.Stop(Program.Directory + "/sounds/Hit metal 35.mp3") 
Sound.Play(Program.Directory + "/sounds/Hit metal 35.mp3")   
  If x+8 >= padX+80 Then 
    Shapes.Rotate(paddle, 15) 
  ElseIf x+8 <= padX+40 then 
    Shapes.Rotate(paddle, -15) 
  Else 
    Shapes.Rotate(paddle, 0) 
    EndIf 
   
   
   
   
    If x+8 >= padX+40 And x+8 <= padX + 80 then 
      deltaY = -1*deltaY 
    Else 
       
       If (deltaX>=0 And x+8<=padX+40) Or (deltaX<=0 And x+8>=padX+80) then 
       deltaX= -deltaX 
       deltaY=-deltaY 
        
       ElseIf (deltaX>=0 And x+8>=padX+80) then 
         deltaY=-deltaY 
          
       ElseIf (deltaX<=0 And x+8<=padX+40) then 
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
 
While Controls.LastClickedButton<>No And Controls.LastClickedButton <> yes 
 
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
    If cube[i][j]<>0 Then  
      If ((y+8<=Shapes.GetTop(cube[i][j]) And y+8>= Shapes.GetTop(cube[i][j])-8) Or (y+8>=Shapes.GetTop(cube[i][j])+40 And y+8<= Shapes.GetTop(cube[i][j])+48)) And (x+8>=Shapes.GetLeft(cube[i][j]) And x+8<=Shapes.GetLeft(cube[i][j])+40) Then 
        z=z+1 
        Zvalue() 
        Shapes.Remove(cube[i][j]) 
        cube[i][j]=0 
        Sound.PlayClick() 
        deltaY=-deltaY    
           nextif="False" 
        ElseIf ((x+8<=Shapes.GetLeft(cube[i][j]) And x+8>= Shapes.GetLeft(cube[i][j])-8) Or (x+8>=Shapes.GetLeft(cube[i][j])+40 And x+8<= Shapes.GetLeft(cube[i][j])+48)) And (y+8>=Shapes.GetTop(cube[i][j]) And y+8<=Shapes.GetTop(cube[i][j])+40) And nextif="True" Then 
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
     
    If j= gh-48 And x> padX And x< padX+120 Then 
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
    If j<>40 Then 
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
     
While Controls.LastClickedButton<>start 'And Controls.LastClickedButton<>Exit 
 
EndWhile 
Controls.Remove(start) 
CLS() 
level=1 
 
menu() 
    EndSub 
