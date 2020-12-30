---
title: "Hangman"
category: technet-archive
author:
  name: "Jibba Jabba"
project_url: "https://github.com/alxnull/smallbasic-gallery/tree/master/archive/Hangman"
download: "https://github.com/alxnull/smallbasic-gallery/raw/master/archive/Hangman/Hangman v1-0.zip"
image: hangman.png
---

<b>Hangman is a fun and popular word game. To play, download the Zip, unZip it and double click the application file. The Zip includes source code.</b>

<DIV id=longDesc>
<P>Hangman is a fun and popular word game.</P>
<P>To play, download the Zip, unZip it and double click the application file. The Zip includes source code.</P>
<P>
<H1>Version 1.0</H1>
<P>Is a simple solution to the game coded in Small Basic. 133 loc. It's a single session one-player take on the game which includes some retro Small Basic themed graphics, sound FX, scoring and a 900+ word list.</P>
<H2>The Graphics</H2>
<P>Are done for a fixed sized GraphicsWindow. This was done using Paint.Net by creating a fixed sized background graphic then cutting out verious graphic components. This technique requires making the component surroundings transparent and maintaning their position in the fixed sized canvas. By doing this simple graphic FX can be achieved without coding their positions.</P>
<H2>Bugs</H2>
<P>No knowns at the moment.<BR>The last bug was a classic. I was using an uninitialised iterator "i = i + 1" in a While loop. Big no no! The "i" value was storing an earlier value of "i" set by a For loop.</P>
<H2>Future Releases</H2>
<P>v1 releases will maintain a fixed sized canvas and Small Basic theme. Upcoming feature ideas could be:</P>
<UL>
<LI>multi-session play; 
<LI>leaders board (extension required); and 
<LI>dialogue boxes (doable without extensions) </LI></UL>
<P>&nbsp;</P>
<P>v2 releases would be a different UI setup. Probably ditching the fixed size canvas approach.</P></DIV>
