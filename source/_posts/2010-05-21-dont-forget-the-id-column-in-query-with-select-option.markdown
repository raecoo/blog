---
layout: post
title: Don't forget the id column in query with select option
---

<pre><code>>> >> g = Game.find(:all, :select=>'title').first
=> #<Game title: "World of Goo">
>> g.title # Question
=> nil
>> g[:title]
=> "World of Goo"
>> g = Game.find(:all, :select=>'id, title').first
=> #<Game id: 1219, title: "World of Goo">
>> g.title
=> "World of Goo"</code></pre>

Anwser:

Default, the Rails will be select all columns of the table and you can use the Object.attribute_name to reference the column value, otherwise, just load the special columns within :select option value. at this time, if you didn't add the id column in :select option, so that you need to reference the column value as a element of an array.

I guess Rails use the id column to mark the Object in memory, Anyway, let's read the source code to find out the finally reasons.
