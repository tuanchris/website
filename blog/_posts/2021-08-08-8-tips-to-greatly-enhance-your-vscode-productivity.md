---
title: 8 Tips to Greatly Enhance Your VSCode Productivity
image: https://cdn-images-1.medium.com/max/11150/0*ZFvO13i-QUrGjX9o
description: My 8 tips for people started using VSCode for the first time or switching from another IDE.
---

# 8 Tips to Greatly Enhance Your VSCode Productivity

Getting your way around an IDE is a vital part, whether you are an engineer or an analyst. Watching a senior developer jumping around in Vim or VSCode can be intimidating for people with less familiarity. However, I assure you that there is no magic here. It is all practice and Googling answers when you got stuck.

Most of the tips I shared in this article will greatly improve your productivity. Once you learn some of these, you will have a hard time imagining life without them.

## 1. The master of all shortcuts

If there is one shortcut you take away from this post, it is this: **⌘ + Shift + P** (you can substitute all ⌘ keys for Ctrl and option for alt on Windows). This shortcut opens the control palette in VSCode, where you can search for commands, actions, and other shortcuts.

![The command palette — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*sDPWfltz31Z6txGNpDp1GA.gif)

*The command palette — GIF by the author*

Try searching for Copy path of active file or Copy relative path of active fileand press enter. No more fumbling around trying to type in exactly the file path to your terminal. Best of all is that you don’t have to remember the actual shortcut to these commands. You only need to remember what they do and search for them in the command palette.

The command palette also remembers some recent items that you opened so you can quickly browse through them.

## 2. Navigate files in your repo

With the command palette opened, you can delete the > character or use the **⌘ + P** command to search for files in the repo. This is especially useful if your project structure is convoluted and it takes time to navigate around. With this command, you will only have to remember the file name.

![Navigating all files in a repo — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*w6fBNfwvU7eBHAK5oMuq7A.gif)

*Navigating all files in a repo — GIF by the author*

The search engine is quite good, so you only need to type in the initials of your file name if it is long. For example, you only need to type ssp into the search bar to search for a file named stg_stripe__payments.sql.

When you have a repo opened on a VSCode window, you can quickly preview files by click on them. Double click a file will open it permanently centered or on the left-hand side. Double-clicking the file will open it on the right-hand side. This is pretty useful when you want to compare the content of two files side by side.

## 3. Multi-cursor editing

This is the part that will **greatly enhance your productivity** when working with a code file. Multi-cursor editing is the ability to have multiple cursors simultaneously and edit from all those cursors instead of one at a time. Let’s use a SQL query and look at some of the use cases for multi-cursor.

There might be several new things to learn here, but if you master them all, you can move around and get things done really fast. I found myself frequently copying snippets from other programs like Word to VSCode to manipulate them.

### Renaming all instances

A common thing to do is select all occurrences and change them all at once. In the example below, our table’s name was changed from orders to order. To do that, you only need to select one instance of the word orders and use **⌘ + shift + L**. This shortcut will create multiple cursors at the word orders so you can edit them.

![](https://cdn-images-1.medium.com/max/2000/1*VA2a8VnT4NP60TPNOyyywQ.gif)

This is much like search and replaces with a lot more flexibility.

If we change this query to a different dialect and all column names should be in double-quotes? We can select all instances of the character . and use **Shift + →** to select the next word. With all the column names selected, we can type " to have them all in quotes.

![Quoting all column names — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*omjCx0vYcsNjRDH4k0SVMA.gif)

*Quoting all column names — GIF by the author*

The next example is when we have a long and complicated query and only want to change occurrences within our select statements. You can use ⌘+ F to enable search mode then select the area you want to operate in. Next, press **⌘+ option + L** to search only in the selected area. You can now use **⌘ + shift + L** and change the typos orders to order. Notice that the word order in the from statement is not affected.

![](https://cdn-images-1.medium.com/max/2000/1*Xo7DvRjcntzFQRuNNWRIEQ.gif)

### Turn multiple lines to a Python list

Now let’s try to extract all the column names in this query and turn that into a Python list. For the four first columns, we can use a new shortcut to select them. First, select the space after the . character in the first column. Then hold down **shift + option** and select the same space in the last column. You see that with this, we have created multi-line cursors. To add the last column, you can hold down **option** and select it. Finally, use **option** **+ **→ to select all columns.

![Selecting all columns — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*Ng3Qc7DlWOl9LRM8gGsjJg.gif)

*Selecting all columns — GIF by the author*

With the copied columns, you can paste them down below, select all lines using **shift + option**, quote them, add a comma, delete new line, and put everything in a square bracket.

![Turning copied columns to a Python list — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*wCubXnK_bCM_Kl16CULVMQ.gif)

*Turning copied columns to a Python list — GIF by the author*

## 4. Reordering line

Instead of copy and paste to change the order of lines, you can use** option + cursor** to move any lines up and down. You can select multiple lines at the same time and use this function too.

![Move lines around using cursor — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*GOoFpN50nYz03IGob2nUGw.gif)

*Move lines around using cursor — GIF by the author*

You can also short lines based on their length by selecting the lines, open the command palette, and choose either Sort lines Ascending or Descending.

![Sorting lines using command palette — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*uCW1_MvXEAtjeROBBVS1_g.gif)

*Sorting lines using command palette — GIF by the author*

## 5. Code folding

For complicated codes, sometimes it is hard to know what is going on. If the code is nicely formatted, you can use the Fold All command palette's command to collapse all code. This gives us a high-level overview of what is going on, and we can dive into a specific area that interests us.

![Folding all codes — Image by the author](https://cdn-images-1.medium.com/max/2314/1*9ay6Elr7s_D02qKXXPJ3pw.gif)

*Folding all codes — Image by the author*

You can also use the following commands respectively to fold and unfold a selection: **⌘ + option + [**, **⌘ + option + ]**.

## 6. Formatting

When writing code, having a clearly formatted code is essential to maintain readability. VSCode is popular for having rich extension libraries, and you can find linter to format most programming languages out there.

![Code formatting — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*6eksY_EmOMhlWCVBdaTmKA.gif)

*Code formatting — GIF by the author*

To auto-format a file, you can use the command **option + shift + F**. If the linter for the file extension you are trying to format is not installed, VSCode will prompt you to do so. I use this shortcut a lot when working with Python, SQL, or Terraform files.

## 7. Find instances in the repo

Sometimes you have a value that you have to change across your repo. It can be a function name or a variable. Finding and changing them all manually can be a pain. You can use **⌘ + shift + F** to find all instances of a word or phrase in your repo and replace them with something else.

## 8. Toggle terminal

The terminal is an essential part of any software development workflow. You can open a terminal attached to your coding environment with the shortcut: **control + `**. You can use the command palette to Run current file in a terminal.

If you are developing with Python, I really love selecting a snippet of code and executing it in a Jupyter environment locally. Select the text you want to execute and use **shift + enter**—very much similar to a cell in Jupyter Notebook.

![](https://cdn-images-1.medium.com/max/2908/1*bpG4jErCEjCVxWJPLWUdQA.gif)

## (Bonus) Use a universal clipboard manager

I cannot live without a clipboard manager now. A clipboard manager has the ability to save whatever you copy and keep that for a set period of time (1 to 3 months depends on the tool). You can search for items in there too. For example, if I want to remember a package that I installed using brew recently, I only need to search for brew in my clipboard manager.

![The magic of a clipboard manager — GIF by the author](https://cdn-images-1.medium.com/max/2000/1*Ithr1_ejs-E6l656agB0Pg.gif)

*The magic of a clipboard manager — GIF by the author*

There are many clipboard managers out there. But if you use Mac, I recommend checking out Alfred (paid) and Raycast (free). Both of them are pretty awesome and packed with other functionalities too.

I hope you learned something from this article. Until next time 😁
