---
layout: post
title: SQL Like statement
Tags: code, sql
permalink: sql-like-statement
---

Today I learnt a few new (well to me) SQL commands.  The "Like statement":http://doc.ddart.net/mssql/sql70/la-lz_2.htm can do some basic regex type things.  It supports character specifiers like this:

pre(prettyprint). 
Column Like '%[a-z]Test[a-z]%'

This will find the word test as long as there is a letter at either end of the word in a block of text.  You can also say Not a letter like so:

pre(prettyprint). 
Column Like '%[^a-z]Test[^a-z]%'

This should find any words Test that do not have letters before or after them. Very useful for searching for a complete word in a block of text.  However I could not get this to work (MSSQL Server 2005) so I ended up doing this:

pre(prettyprint). 
Select 	Columns
From	TableName 
Where	BlockOfText Like '%' + @word +'%'
  and	BlockOfText not like '%[a-z]' + @word + '[a-z]%'
  
 Which works well for what I needed and is reasonably quick on a million records or so.