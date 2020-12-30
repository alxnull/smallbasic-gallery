---
title: "sb-logger - A Small Basic Logger"
category: technet-archive
author:
  name: "Florian Auer"
project_url: "https://github.com/alxnull/smallbasic-gallery/tree/master/archive/sb-logger_-_A_Small_Basic_Logger"
download: "https://github.com/alxnull/smallbasic-gallery/raw/master/archive/sb-logger_-_A_Small_Basic_Logger/sb-logger.zip"
---

<b>Adds basic logging functionality to Small Basic by using special comments.</b>

<DIV id=longDesc>
<H1><SPAN style="FONT-SIZE: xx-large">sb-logger</SPAN></H1>
<P><SPAN style="FONT-SIZE: medium">Small Basic comes without any logging ability which makes debugging sometimes a painful task. That's why I developed sb-logger. </SPAN></P>
<P>&nbsp;</P>
<P><SPAN style="FONT-SIZE: x-large">Installation</SPAN></P>
<OL>
<LI><SPAN style="FONT-SIZE: medium">Download the <EM>sb-logger.zip</EM> and unpack it.</SPAN> </LI></OL>
<P>&nbsp;</P>
<P><SPAN style="FONT-SIZE: x-large">How it works<BR></SPAN></P>
<OL>
<LI><SPAN style="FONT-SIZE: medium">Add logging statements to your source code (as described below)</SPAN> 
<LI><SPAN style="FONT-SIZE: medium">Drag &amp; Drop the source file into the <EM>sb-logger.exe</EM></SPAN> 
<LI><SPAN style="FONT-SIZE: medium">Run the generated source file (<EM>&lt;source&gt;_with_logging.sb</EM>)</SPAN> </LI></OL>
<P>&nbsp;</P>
<P><SPAN style="FONT-SIZE: x-large">Logging statements</SPAN></P>
<P><SPAN style="FONT-SIZE: medium">Add following statements to your code for logging.</SPAN></P>
<P>&nbsp;</P>
<P><STRONG><SPAN style="FONT-SIZE: medium">'LOGFILE</SPAN></STRONG></P>
<P><SPAN style="FONT-SIZE: medium">It tells the logging system to write (append) all logging messages to the given file. If this statement is not used, the output is written to the TextWindow.</SPAN></P>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN style="FONT-SIZE: medium">Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN style="FONT-SIZE: medium"><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></SPAN></DIV><SPAN class=hidden style="FONT-SIZE: medium">vb </SPAN><PRE class=hidden><SPAN style="FONT-SIZE: medium">'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"</SPAN></PRE>
<DIV class=preview><PRE class=vb><SPAN class=visualBasic__com style="FONT-SIZE: medium">'LOGFILE&nbsp;Clock.ElapsedMilliseconds&nbsp;+&nbsp;"tetris-log.txt"</SPAN></PRE></DIV></DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">Everything after 'LOGFILE is used in the generated source code in the following way.</SPAN></DIV>
<DIV class=endscriptcode>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN style="FONT-SIZE: medium">Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN style="FONT-SIZE: medium"><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></SPAN></DIV><SPAN class=hidden style="FONT-SIZE: medium">vb </SPAN><PRE class=hidden><SPAN style="FONT-SIZE: medium">_LOG_TO_FILE = Program.Directory + "\"+ Clock.ElapsedMilliseconds + "tetris-log.txt"</SPAN></PRE>
<DIV class=preview><PRE class=vb><SPAN style="FONT-SIZE: medium">_LOG_TO_FILE&nbsp;=&nbsp;Program.Directory&nbsp;+&nbsp;<SPAN class=visualBasic__string>"\"+&nbsp;Clock.ElapsedMilliseconds&nbsp;+&nbsp;"</SPAN>tetris-log.txt"</SPAN></PRE></DIV></DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">&nbsp;This allows to generate dynamic log-file names.</SPAN></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium"><BR></SPAN></DIV></DIV>
<P><STRONG><SPAN style="FONT-SIZE: medium">'LOG</SPAN></STRONG></P>
<P><SPAN style="FONT-SIZE: medium">It tells sb-logger a message that should be logged. <EM>&nbsp;</EM></SPAN></P>
<P><SPAN style="FONT-SIZE: medium"><EM>Important</EM>: a whitespace have to be between 'LOG and the message.</SPAN></P>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN style="FONT-SIZE: medium">Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN style="FONT-SIZE: medium"><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></SPAN></DIV><SPAN class=hidden style="FONT-SIZE: medium">vb </SPAN><PRE class=hidden><SPAN style="FONT-SIZE: medium">'LOG "handle key " + GraphicsWindow.LastKey</SPAN></PRE>
<DIV class=preview><PRE class=js><SPAN style="FONT-SIZE: medium">'LOG&nbsp;<SPAN class=js__string>"handle&nbsp;key&nbsp;"</SPAN>&nbsp;+&nbsp;GraphicsWindow.LastKey</SPAN></PRE></DIV></DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">&nbsp;Again everything after 'LOG (and a whitespace) is used to create a message. The output of sb-logger for this statement is:</SPAN></DIV>
<DIV class=endscriptcode>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN style="FONT-SIZE: medium">Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN style="FONT-SIZE: medium"><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></SPAN></DIV><SPAN class=hidden style="FONT-SIZE: medium">vb </SPAN><PRE class=hidden><SPAN style="FONT-SIZE: medium">_LOG_SUB = "HandleKey"
_LOG_LINE = 89
_LOG_MSG = "handle key " + GraphicsWindow.LastKey
_LOG()</SPAN></PRE>
<DIV class=preview><PRE class=js><SPAN style="FONT-SIZE: medium">_LOG_SUB&nbsp;=&nbsp;<SPAN class=js__string>"HandleKey"</SPAN>&nbsp;
_LOG_LINE&nbsp;=&nbsp;<SPAN class=js__num>89</SPAN>&nbsp;
_LOG_MSG&nbsp;=&nbsp;<SPAN class=js__string>"handle&nbsp;key&nbsp;"</SPAN>&nbsp;+&nbsp;GraphicsWindow.LastKey&nbsp;
_LOG()</SPAN></PRE></DIV></DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">&nbsp;It adds the current subroutine ("HandleKey"), the source code line (89) and the message ("handle key " + GraphicsWindow.LastKey). Finally the _LOG() subroutine writes the message. </SPAN></DIV>
<DIV class=endscriptcode></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">To comment a logging statment (so that it is ignored by sb-logger) just add a ' in front of it.<BR></SPAN></DIV>
<DIV class=endscriptcode></DIV>
<DIV class=endscriptcode>
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vb</SPAN> <PRE class=hidden>''LOG "handle key " + GraphicsWindow.LastKey
' also possible
'  'LOG "handle key " + GraphicsWindow.LastKey</PRE>
<DIV class=preview><PRE class=js><SPAN class=js__string>''</SPAN>LOG&nbsp;<SPAN class=js__string>"handle&nbsp;key&nbsp;"</SPAN>&nbsp;+&nbsp;GraphicsWindow.LastKey&nbsp;
'&nbsp;also&nbsp;possible&nbsp;
<SPAN class=js__string>'&nbsp;&nbsp;'</SPAN>LOG&nbsp;<SPAN class=js__string>"handle&nbsp;key&nbsp;"</SPAN>&nbsp;+&nbsp;GraphicsWindow.LastKey</PRE></DIV></DIV></DIV>
<DIV class=endscriptcode>&nbsp;</DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: x-large">Example</SPAN></DIV>
<DIV class=endscriptcode></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">Within the <EM>sb-logger.zip</EM> is <EM>tetris.sb</EM>. It has already some logging statements. <BR></SPAN></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vb</SPAN> <PRE class=hidden>'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"
'LOG "program start"
...</PRE>
<DIV class=preview><PRE class=vb><SPAN class=visualBasic__com>'LOGFILE&nbsp;Clock.ElapsedMilliseconds&nbsp;+&nbsp;"tetris-log.txt"</SPAN><SPAN class=visualBasic__com>'LOG&nbsp;"program&nbsp;start"</SPAN>&nbsp;
...</PRE></DIV></DIV></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">&nbsp;The first line may already look familiar to you. It tells sb-logger to write the logging messages to the file <EM>&lt;EllapsedMilliseconds&gt;tetris-log.txt</EM> (see <EM>Logging Statements</EM> for further explanation). The second line is a logging message.</SPAN></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium"><BR></SPAN></DIV>
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">&nbsp;</SPAN></DIV></SPAN></SPAN><SPAN style="FONT-SIZE: medium">
<DIV class=endscriptcode><STRONG>&nbsp;</STRONG></DIV><STRONG>To run the example (with log-file)</STRONG></SPAN><BR>
<OL>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">Drag&amp;Drop the source file into the <EM>sb-logger.exe</EM>. A new file with the name <EM>tetris_with_logging.sb</EM> is created within the folder. </SPAN></DIV></SPAN></SPAN>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">Now open Small Basic, load </SPAN><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium"><EM>tetris_with_logging.sb</EM> and hit the run button.You will see the familiar Tetris game as without any logging. </SPAN></SPAN></SPAN></DIV></SPAN></SPAN>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium">Play the game for a while :-)</SPAN></SPAN></SPAN></DIV></SPAN></SPAN>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium">Go to the folder of </SPAN></SPAN></SPAN></SPAN></SPAN><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium"><EM>tetris_with_logging.sb</EM>. There is now a new file called <EM>&lt;SomeRandomLookingNumber&gt;tetris-log.txt</EM>. <BR></SPAN></SPAN></SPAN>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium">Open it with your editor of choice and you will see all logging messages.</SPAN></SPAN></SPAN> </LI></OL><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><STRONG><SPAN style="FONT-SIZE: medium"><BR></SPAN></STRONG></DIV></SPAN></SPAN><SPAN style="FONT-SIZE: medium">
<DIV class=endscriptcode><STRONG>&nbsp;</STRONG></DIV><SPAN style="FONT-SIZE: x-large">&nbsp;</SPAN><STRONG>To run the example (with TextWindow output)</STRONG></SPAN><BR>
<OL>
<LI><SPAN style="FONT-SIZE: medium">Remove the first line of tetris.sb</SPAN> 
<DIV class=scriptcode>
<DIV class=pluginEditHolder pluginCommand="mceScriptCode">
<DIV class=title><SPAN>Visual Basic</SPAN></DIV>
<DIV class=pluginLinkHolder><SPAN class=pluginEditHolderLink>Edit</SPAN>|<SPAN class=pluginRemoveHolderLink>Remove</SPAN></DIV><SPAN class=hidden>vb</SPAN> <PRE class=hidden>'LOGFILE Clock.ElapsedMilliseconds + "tetris-log.txt"</PRE>
<DIV class=preview><PRE class=js>'LOGFILE&nbsp;Clock.ElapsedMilliseconds&nbsp;+&nbsp;<SPAN class=js__string>"tetris-log.txt"</SPAN></PRE></DIV></DIV></DIV>
<DIV class=endscriptcode>&nbsp;</DIV>
<LI><SPAN style="FONT-SIZE: medium">Drag&amp;Drop the source file into the <EM>sb-logger.exe</EM>. A new file with the name <EM>tetris_with_logging.sb</EM> is created within the folder.</SPAN> 
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium">Now open Small Basic, load </SPAN><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium"><EM>tetris_with_logging.sb</EM> and hit the run button. You will see the familiar Tetris game and a TextWindow that shows all logging messages.<BR></SPAN></SPAN></SPAN></DIV></SPAN></SPAN>
<LI><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large">
<DIV class=endscriptcode><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><SPAN style="FONT-SIZE: medium">Play the game for a while :-)</SPAN></SPAN></SPAN></DIV></SPAN></SPAN></LI></OL><SPAN style="FONT-SIZE: medium"><SPAN style="FONT-SIZE: x-large"><BR></SPAN></SPAN></DIV>
<DIV class=endscriptcode></DIV>
<DIV class=endscriptcode></DIV></DIV></DIV>
