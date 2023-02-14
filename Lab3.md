# Lab Report 3: Command Options: Find
In this lab we look into more complex ways of using some of the commands we've used so far. In particular, we will look at Find, and new ways we are able to use the command in order to make our computer navigation more efficient.

## The -type modifier
The first technique we will look at for Find is the -type modifier. the -type modifier allows us to make the Find command only
output a specific type of path, like a directory vs a file.

### Example 1
```
[cs15lwi23aof@ieng6-203]:written_2:158$ find -type d            
.
./non-fiction
./non-fiction/OUP
./non-fiction/OUP/Abernathy
./non-fiction/OUP/Berk
./non-fiction/OUP/Castro
./non-fiction/OUP/Fletcher
./non-fiction/OUP/Kauffman
./non-fiction/OUP/Rybczynski
./travel_guides
./travel_guides/berlitz1
./travel_guides/berlitz2
```
Here we can see that using -type d specifies that we want to search the current directory only for
directories, and exclude file outputs.

### Example 2
```
[cs15lwi23aof@ieng6-203]:written_2:159$ find -type f
./non-fiction/OUP/Abernathy/ch1.txt
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt
./non-fiction/OUP/Abernathy/ch3.txt
./non-fiction/OUP/Abernathy/ch6.txt
./non-fiction/OUP/Abernathy/ch7.txt
./non-fiction/OUP/Abernathy/ch8.txt
./non-fiction/OUP/Abernathy/ch9.txt
./non-fiction/OUP/Berk/CH4.txt
```
In this case, we use the same modifier, -type, but use f to denote files. In this case the directories are
excluded from the output. 

<br/>

*source:* https://math2001.github.io/article/bashs-find-command/        


## the -name modifier
The second modifier is the -name modifier. We used this in class but I didn't really understand it at the time. Basically it takes 
a "glob" (one of those *thing statements) and then only outputs paths matching to the glob. 

### Example 1
```
[cs15lwi23aof@ieng6-203]:written_2:160$ find -name *History.txt
./travel_guides/berlitz2/Algarve-History.txt
./travel_guides/berlitz2/Amsterdam-History.txt
./travel_guides/berlitz2/Athens-History.txt
./travel_guides/berlitz2/Bahamas-History.txt
./travel_guides/berlitz2/Bali-History.txt
./travel_guides/berlitz2/Barcelona-History.txt
./travel_guides/berlitz2/Beijing-History.txt
./travel_guides/berlitz2/Berlin-History.txt
./travel_guides/berlitz2/Budapest-History.txt
./travel_guides/berlitz2/California-History.txt
```
In this example, we are able to quickly find all paths to text files which end in History.txt.

### Example 2
```
[cs15lwi23aof@ieng6-203]:written_2:165$ find -name *.txt
./non-fiction/OUP/Abernathy/ch1.txt
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt
./non-fiction/OUP/Abernathy/ch3.txt
./non-fiction/OUP/Abernathy/ch6.txt
./non-fiction/OUP/Abernathy/ch7.txt
./non-fiction/OUP/Abernathy/ch8.txt
./non-fiction/OUP/Abernathy/ch9.txt
./non-fiction/OUP/Berk/CH4.txt
```
In this example, we are able to do waht we used to do with a combined find and grep command sequence. 
We filter for only .txt files in the output. How cool!

<br/>

*source:* https://math2001.github.io/article/bashs-find-command/

<br/>

## The -path modifier:
-path is another useful option for Find, and it is heavily related to -name. In this case though, you can use a glob to match with the
end characters of both the name and the path, so files can be found only in paths that have a certain keyword.

### Example 1
```
[cs15lwi23aof@ieng6-203]:written_2:170$ find -path *berlitz2/*.txt
./travel_guides/berlitz2/Algarve-History.txt
./travel_guides/berlitz2/Algarve-Intro.txt
./travel_guides/berlitz2/Algarve-WhatToDo.txt
./travel_guides/berlitz2/Algarve-WhereToGo.txt
./travel_guides/berlitz2/Amsterdam-History.txt
./travel_guides/berlitz2/Amsterdam-Intro.txt
./travel_guides/berlitz2/Amsterdam-WhatToDo.txt
./travel_guides/berlitz2/Amsterdam-WhereToGo.txt
./travel_guides/berlitz2/Athens-History.txt
./travel_guides/berlitz2/Athens-Intro.txt
```
Here we can see that we can use multiple * to find matching patterns in each layer of the path.

### Example 2
```
[cs15lwi23aof@ieng6-203]:written_2:180$ find -path *fiction/*.txt
./non-fiction/OUP/Abernathy/ch1.txt
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt
./non-fiction/OUP/Abernathy/ch3.txt
./non-fiction/OUP/Abernathy/ch6.txt
./non-fiction/OUP/Abernathy/ch7.txt
./non-fiction/OUP/Abernathy/ch8.txt
./non-fiction/OUP/Abernathy/ch9.txt
./non-fiction/OUP/Berk/CH4.txt
```
And in this case, we can see that the directories do not actually have to be adjacent to
be used together.

<br/>

*source:* https://math2001.github.io/article/bashs-find-command/

<br/>

## The boolean modifiers
The fourth option for find allows us to combine all of the previous techniques by adding boolean logic
to the find filters. the -and and -or options allow us to combine modifiers in specified ways, to create an
even more powerful command.

### Example 1
```
[cs15lwi23aof@ieng6-203]:written_2:189$ find -path *California* -or -name *Jamaica.txt
./travel_guides/berlitz1/HandRJamaica.txt
./travel_guides/berlitz1/HistoryJamaica.txt
./travel_guides/berlitz1/IntroJamaica.txt
./travel_guides/berlitz1/WhatToJamaica.txt
./travel_guides/berlitz2/California-History.txt
./travel_guides/berlitz2/California-WhatToDo.txt
./travel_guides/berlitz2/California-WhereToGo.txt
```
In this example, we're finding all of the files or directories with California in the name, and also finding any txt files
ending in Jamaica.

### Example 2
```
[cs15lwi23aof@ieng6-203]:written_2:191$ find -path *California* -and -name *To*.txt
./travel_guides/berlitz2/California-WhatToDo.txt
./travel_guides/berlitz2/California-WhereToGo.txt
```
In this case we're finding all of the files with California in the path *and* have "To" in the name.
<br/>


*source:* https://math2001.github.io/article/bashs-find-command/

<br/>

## References
A list of any references used:

Source of Find modifier knowledge:
https://math2001.github.io/article/bashs-find-command/

ChatGPT created the markdown template for this report.