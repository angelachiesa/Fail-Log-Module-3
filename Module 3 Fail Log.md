# Fail Log for Module Three
##### July 24th - July 30th
------------
###### Previous Mistakes
One of last mistakes tasks that I want to improve is creating repositories properly. I didn't set them up correctly if you look at my list, their are so many of them created. I'm hoping with this week, they will be more organized. 

###### Readings
For this week's annotations, I choose _Mining and Mapping the Production of Space A View of the World from Houston_. The beginning talks about urbanism so it caught my attention. Although the first paragraph was a bit misleading to the rest, it did get me thinking a bit more about data. One thing in particular that I do mention in my blog post as well is how the author changed his data in accordance to the information he collected. He states, _"...I shaped the project around the availability of digitized and machine-readable sources. Accessibility can be a major impediment to digital analysis."_ He changed his research to match some of the searchings he found. I found this so strange because it never occured to me that someone would do this. It's really interesting as to what his research would of concluded had the person kept going with their original thought. Even with less data supporting the route that they intended to go in, it would of created an entirely different project in the end.

https://via.hypothes.is/https://web.stanford.edu/group/spatialhistory/cgi-bin/site/pub.php?id=93

# Exercise 1
### Gentle Introduction to Regex
To summarize, the point of the exercise is to ask the computer to search for patterns instead of specific data by matching text. This is known as ‘regular expressions’ or also short for ‘Regex’.
  Notes – How to describe a pattern, and the regular expressions will find it
How to search and replace data.
Option 1
1.	Shift+backslash (dog|cat) means or
2.	If you want to replace every instance of either cat or dog, with the word animals, you open your ‘find-and-replace box’, put dog|cat and put ‘animal’ in the ‘replace’ box, and hit replace all
3.	Note that it messes most things up and will put "certificate" will become "certifianimale”
4.	\<cat\> for only cat or \<cat|dog\> only dog and cat 
Option 2
1.	gray|grey
2.	gr(a|e)y
3.	(that dog)|(that cat)
4.	d.g will search for "dig", "dog", "dug", and so forth.
5.	do+g will search for "dog", "doog", "dooog", and so forth.
6.	(do)+g will search for "dog", "dodog", "dododog", and so forth.
7.	d.+g will search for "dried fruits are g",… because the beginning starts will a d and the end starts with a g
8.	(dogs)( and )(cats) will look for all dogs and cats in the document 

### Regex Exercise
-	Downloaded a file using curl
-	curl http://archive.org/stream/diplomaticcorre33statgoog/diplomaticcorre33statgoog_djvu.txt > texas.txt
-	put > which pushes the result into a file called texas.txt
-	TO DELETE LIST OF THINGS
o	ctrl+shift+6
o	hit down, and ctrl +k to delete


1. sed comman - identifies text that matches a pattern ---- sed 's/old text/new text/g' filename
2. and grep command - print the results to the screen ---- grep 'PATTERN WE WANT' inputfil
3. use > outputfile at the end if you want a new file


#### Step 1

**Notes** 
If you were using a text editor on your own computer like, for instance Notepad++, you would press ctrl-f or search->find to open the find dialogue box. In that box, go to the 'Replace' tab, and check the radio box for 'Regular expression' at the bottom of the search box.


Goal - We wanted to ~ at the beginning of every line that looked like a reference letter.
1. Go into the dhbox and type (grep '\bto\b' texas.txt)
It is to show all the results on the screen, without werid random words.
2. Copy and paste some of the text into RegExr.com
3. type (.+\<to\>)
4. now back to DhBox, we put sed -r -i.bak 's/(.+\bto\b.+)/~\1/g' texas.txt
what this means -
-r means extended regex. this saves us from having to 'escape' certain characters -i.bak means make a backup of the original input file, in case things go wrong. -'s/old-pattern/newpattern/g' is how we find and switch what we're looking for. the final g means 'globally', everywhere in the file texas.txt the filename that we're looking to change.
5. this gives us a new file called, texas.txt.bak
6. when we enter into nano, we can see all the ~ have been created.

#### Step 2
In step 2, we want to remove lines which are not relevant. 

**Notes**
1. If I was using a text ediotr on my computer, the serach string is (\n[^~].+)
2. \n or \r\n means to search for a new line 
3. [] within those, and the ^ this means to search
4. the .+ means to search for all the rest of the characters in the line as well
5. To look at it go, grep '~' texas.txt > index.txt
6. what this does is, it looks for the '~' lines and puts it into a new file called index.txt which you can access with nano.

#### Step 3
Step 3 is to learn how to transform into CSV format.
So basically, how to put this into a spreadsheet.

1. How to change
~Sam Houston to J. Pinckney Henderson, December 31, 1836 51
to
Sam Houston, J. Pinckney Henderson, December 31 1836

Use Regex and type: [0-9]{4}

I guessed that you would use
sed -r -i.bak ‘s/(,)( [0-9]{4})(.+)/~\1/g’ texas.txt
and the correct answer is.
sed -r -i.bak 's/(,)( [0-9]{4})(.+)/\2/g' index.txt

I assume that the file was changed to index for something else, not 100% sure why the 2, however it makes me happy that even though I didn't do it correctly, I was close to getting the command. 

#### Step 4
To delete the tildes, type: sed -r -i.bak 's/~//g' index.txt
#### Step 5
To seperate senders and recivers, sed -r -i.bak 's/(\b to \b)/,/g' index.txt

#### Step 6
Cleaned up the file.

>Reflection
I felt pretty good overall with this exercise. It took me the shortest time out of all of them. I remember I had a lot of trouble but I think because I did them slowely and repeated them to make sure I knew what I was doing, I definatly did this one in a short amount of time. 

# Exercise 2 
Could install Refine okay. Had to install Java first, but things went smoothly. 

I realized that I didn't do the first exercise right. I followed the instructions when it came to adding "Sender, Recipient, Date", However when it was put into Openfile, it didn't show them as separate columns, but as one. I decided to ask in Slack my issue and just go along with the tutorial regardless. It didn’t seem to mess up how to do the tutorial as the instructions are the same for each column.

** Notes**
How to clean up text using Open File.
1. left of "Sender" in OpenRefine and select Facet->Text Facet
2. "Sender" facet box on the left-hand side, click on the button labeled "Cluster"
3. check the box to the right in the 'Merge' column and click the 'Merge Selected & Re-Cluster' button below.
4. click the arrow next to "Sender" and select 'Edit Cells->Common transforms->Trim leading and trailing whitespace'.


**How to Export**
'Export->Custom tabular exporter'. Notice that "source", "target", and "Date" are checked in the content tab; uncheck "Date", as it will not be used in Gephi (networks where the nodes have different dates, ie dynamic networks, are beyond us for the moment). Go to the download tab and change the download option from 'Tab-separated values (TSV)' to 'Comma-separated values (CSV)' and press download. 

>Reflection
Rather than get frustrated, I decided to ask my collegues and contine with the tutorial. The most important part was that I do understand how to use the system, even though the data isn't 100% correct. Until I get a response, I will redo this part to continue with next week exercises. I still feel pretty good because honestly, I think this week's felt like the easiest for me and I was about to go over everything fairly smoothly. I didn't really let the minor error get in the way, and as soon as I redo this, it'll take me less than half hour to correct so I'm feeling pretty good overall. I will attach everything for the fail log as well.