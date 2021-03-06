sb-logger
Small Basic comes without any logging ability which makes debugging sometimes a painful task. That's why I developed sb-logger. 
 
Installation
Download the sb-logger.zip and unpack it. 
 
How it works

Add logging statements to your source code (as described below) 
Drag & Drop the source file into the sb-logger.exe 
Run the generated source file (<source>_with_logging.sb) 
 
Logging statements
Add following statements to your code for logging.
 
'LOGFILE
It tells the logging system to write (append) all logging messages to the given file. If this statement is not used, the output is written to the TextWindow.
Visual Basic
Edit|Remove
vb 
'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"Everything after 'LOGFILE is used in the generated source code in the following way.
Visual Basic
Edit|Remove
vb 
_LOG_TO_FILE = Program.Directory + "\"+ Clock.ElapsedMilliseconds + "tetris-log.txt"_LOG_TO_FILE = Program.Directory + "\"+ Clock.ElapsedMilliseconds + "tetris-log.txt" This allows to generate dynamic log-file names.


'LOG
It tells sb-logger a message that should be logged.  
Important: a whitespace have to be between 'LOG and the message.
Visual Basic
Edit|Remove
vb 
'LOG "handle key " + GraphicsWindow.LastKey'LOG "handle key " + GraphicsWindow.LastKey Again everything after 'LOG (and a whitespace) is used to create a message. The output of sb-logger for this statement is:
Visual Basic
Edit|Remove
vb 
_LOG_SUB = "HandleKey"
_LOG_LINE = 89
_LOG_MSG = "handle key " + GraphicsWindow.LastKey
_LOG()_LOG_SUB = "HandleKey" 
_LOG_LINE = 89 
_LOG_MSG = "handle key " + GraphicsWindow.LastKey 
_LOG() It adds the current subroutine ("HandleKey"), the source code line (89) and the message ("handle key " + GraphicsWindow.LastKey). Finally the _LOG() subroutine writes the message. 
To comment a logging statment (so that it is ignored by sb-logger) just add a ' in front of it.

Visual Basic
Edit|Remove
vb 
''LOG "handle key " + GraphicsWindow.LastKey
' also possible
'  'LOG "handle key " + GraphicsWindow.LastKey''LOG "handle key " + GraphicsWindow.LastKey 
' also possible 
'  'LOG "handle key " + GraphicsWindow.LastKey 
Example
Within the sb-logger.zip is tetris.sb. It has already some logging statements. 

Visual Basic
Edit|Remove
vb 
'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"
'LOG "program start"
...'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"'LOG "program start" 
... The first line may already look familiar to you. It tells sb-logger to write the logging messages to the file <EllapsedMilliseconds>tetris-log.txt (see Logging Statements for further explanation). The second line is a logging message.


 
 
To run the example (with log-file)

Drag&Drop the source file into the sb-logger.exe. A new file with the name tetris_with_logging.sb is created within the folder. 
Now open Small Basic, load tetris_with_logging.sb and hit the run button.You will see the familiar Tetris game as without any logging. 
Play the game for a while :-)
Go to the folder of tetris_with_logging.sb. There is now a new file called <SomeRandomLookingNumber>tetris-log.txt. 

Open it with your editor of choice and you will see all logging messages. 


 
 To run the example (with TextWindow output)

Remove the first line of tetris.sb 
Visual Basic
Edit|Remove
vb 
'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt" 
Drag&Drop the source file into the sb-logger.exe. A new file with the name tetris_with_logging.sb is created within the folder. 
Now open Small Basic, load tetris_with_logging.sb and hit the run button. You will see the familiar Tetris game and a TextWindow that shows all logging messages.

Play the game for a while :-)
