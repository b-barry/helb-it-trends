---
title: Why We Should Drop CRLF
pubDate: Oct 25, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Formatting
imgUrl: '../../assets/teleprinter.jpg' 
description: When we want to create new lines in text from our programs, we are all used to the classic \n or \r\n. But do we really know how they work and how they behave ? CRLF is one of those, but it seems like it's obsolete. Let's find out why, and what we should use instead.
layout: '../../layouts/BlogPost.astro'
---
# Why We Should Drop CLRF
---
## Definitions

NL, CR, LF... We've all seen those before. But what do they mean ? What do they do ? Here's a recap. Just a quick reminder before we dig in, but as we all know, reading and writing in files both use cursor to go through the the file. Cursors will be at the centre of the matter here, **you've been warned**.
- CR (_Carriage Return_): The cursor gets moved straight to the left margin of the file, but stays on the same row (basically a rollback to the start of the row)
- LF (_Line Feed_): The cursors gets moved down one row, but keeps the same column.
- NL (_New Line_): The cursors gets moved down one row and straight to the left margin of the file, which means that this character offers the functionality of both of the others.

Now we all know what which of those does, we can move on to the core of the matter.

## Observations

From the definitions above, it's pretty clear that both CR and NL are really useful chars. While NL is the most common operation we perform on text, CR has its usage, especillay when it's needed to replace the content on a line. However, LF has literally no real use. It senseless to just stay on the same column to keep writing on the next line.

LF appeared 70 years ago, when we used mechanical teleprinters. At this time, the machines were able to print 5 chars per second. At the end of a line, the print head had to get back at the left of the line before starting a new line, but even though the head moved fast, this operation was quite slow. Add to this that there was no memory in those machines, and you understand that you have to reach the start of the new line **before** the head was ready to print the next character. To facilitate that, it was decided to break down the NL operation into two intermediate operations: the famous CR and LF. The CR char would send the print head all the way to the left, and on its traject, the LF char would make the paper cylinder rotate to make the text scroll up one row. This way, the print head had enough time to traverse the sheet before the arrival of the next character. This marked the beginning of the CRLF usage in new lines insertion.

Today, there's a consensus around the silliness of using CRLF instead of NL, but sending them separately is still a task delegated to hardware drivers, since it's still a work-around for modern teleprinters. As such, computers use only NL characters.

To show the uselessness of LF even more, it must be said that this character shares the same Unicode representation as NL, e.g. U+000a, which most machines interprete as NL **only**, and so do most programming languages nowadays, where the NL char is printable as the famous `\n`. However, this doesn't hold back some machines to keep requiring CRs together with NLs, along with some protocols such as HTML, SMTP and CSV.

This tradition should really cease, as it just adds a needless complexity for programmers and contributes to the waste of bandwidth.

## Call to Action

Here's what we can do to slowly but surely make CRLF move to the historical curiosity it deserves to become :
1. Prioritise using the term _newline_ instead of _line feed_ when referring to the U+000a character
2. Use CRs only in two cases:
    - When you need to overwrite a line of text
    - When you're facing systems which you have no control on and which strictly require CRs before NLs.
3. Never comply to protocols which technically require CRLF to end lines, as NL is supported by most of them
4. If you can, fix softwares which don't accept NL to mark end of lines. Supporting CR before NL for compatibility reasons is acceptable, but avoid building software which only support this.

## Sources

- <https://fossil-scm.org/home/ext/crlf-harmful.md?utm_source=newsletter.programmingdigest.net&utm_medium=newsletter&utm_campaign=how-discord-reduced-websocket-traffic-by-40&_bhlid=4b58348d89172eb3bffd37d95d4a8192e4058d6c>
- <https://fullempty.sh/posts/siemens_100a.html> (Cover Image)