---
title: Day 1 experience with Vim. :)
author: Mohit Jain
layout: post
comments: true
permalink: /2012/11/day-1-experience-with-vim/



categories: General VIM
---

I was free this morning and while checking out few things on Quora, again I got an article where people are debating about Textmate, Vim, Emacs etc. And that what pushed me to learn or try out VIM. I know some basic stuff about Vi or Vim as you need to know while doing things on server.  Anyways I downloaded macvim and checkout few tutorials etc and this is what I learned in couple of hours ie basic movements and editing. So if you are in those unlucky souls who always wants to vim but never try it. Just go for it. Just for fun try out these commands and lets what you feel about it.

##Vim Commands

	h -> Left
	j -> Down
	k -> Up
	l -> Right
(Note -> Tutorials says don’t use arrow keys)

	$ -> Go to End of the line
	(Zero) 0 -> Go to starting of the line

	G -> end of the file
	gg -> beginning of the file

——-\*\*\*|\\*\*\*|\** add number in front to jump example 4w or 4f/ etc \*\*\*|\\*\*\*|\** ———

	w -> Jumps to beginning of next word.. Treats special characters as a different word
	W -. Jumps to beginning of next word. Skips special characters.

	e -> Jumps to end of the word. Treats special characters as a different word
	E ->Jumps to end of next word. Skips special characters.

	b -> Move back. Treats special characters as different word
	B -> Move Back, Skips special characters

	f ( a character) -> Jumps to the character matching in the same line.
	F( a character) -> Moves backwards
	; -> repeats the last f ( character) -> works for both f ( ) and F ( )

	t ( a character) -> Same a f ( a characters) but takes to one previous character i.e. until as in ruby :)
	T ( a character) -> Moves back wards -> works same as t ( )
	; works too in this case

	Control f -> Next page
	Control b -> Previous page

	Control d -> Half page down
	Control u -> half page up

	H -> Head of the current page
	M -> Middle of the current page
	L -> Last of the current page

	u -> undo

	23 G -> will take you to the line number 23
	*-> Hit * and then start pressing n -> It will start search the current word in forward on which you are in the file
	*-> Hit * and then start pressing N -> It will start search the current word in backword on which you are in the file
	g*
	g#
	/typeYourSeach -> Forward searching of specific
	?typeYourSearch -> Backword search of something specific

	dd -> delete the current line (remove enter of that line)
	D -> Delete the current line
	x -> delete the current character
	X -> delete the previous character
	dw -> delete the word
	d$ -> remove from current location to end of the line
	% -> Next matching bracket
	=G -> Code Indentation

	**Basic Editing:**
	i -> Insert Mode:
	a -> Append at the current location
	o -> Insert a new line and start editing
	I -> Insert form beginning of the line
	A -> Append after the line.
	O -> Insert a line above and start editing
	c ->delete and change something
	C -> delete and change entire line
	r -> replace current charter
	R -> start replacing anything u want to..
	cw -> editing the current work and start typing new things…
	or c2w -> editing two words
	. -> repeat the last action

	**Yanking: (Copying)**
	yy / Y — copy the whole line
	yw -> yank the word
	p -> paste the yank
	P -> paste above
	J -> join the next line in the same
	**Visual Mode**
	v -> visual mode -> select character by character using hl
	V -> Visual Model -> select by line using j or k

	**Block Highlighting**
	control v -> select a block
	gv -> previous selected block

 

This is what I learned in 2 hours. Tried these commands and its fun. ;) I loved it. Going for some plugins etc to checkout more stuff. I will say just open your terminal and say vimtutor and invest some time to see what exactly it is.My experience with VIM was awesome :) So I will make one more post soon once I checkout the plugins part –> VIM for Rails :) Once I learn it :)
