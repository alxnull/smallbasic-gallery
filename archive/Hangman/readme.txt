Hangman is a fun and popular word game.
To play, download the Zip, unZip it and double click the application file. The Zip includes source code.
Version 1.0
Is a simple solution to the game coded in Small Basic. 133 loc. It's a single session one-player take on the game which includes some retro Small Basic themed graphics, sound FX, scoring and a 900+ word list.
The Graphics
Are done for a fixed sized GraphicsWindow. This was done using Paint.Net by creating a fixed sized background graphic then cutting out verious graphic components. This technique requires making the component surroundings transparent and maintaning their position in the fixed sized canvas. By doing this simple graphic FX can be achieved without coding their positions.
Bugs
No knowns at the moment.
The last bug was a classic. I was using an uninitialised iterator "i = i + 1" in a While loop. Big no no! The "i" value was storing an earlier value of "i" set by a For loop.
Future Releases
v1 releases will maintain a fixed sized canvas and Small Basic theme. Upcoming feature ideas could be:
multi-session play; 
leaders board (extension required); and 
dialogue boxes (doable without extensions) 
 
v2 releases would be a different UI setup. Probably ditching the fixed size canvas approach.
