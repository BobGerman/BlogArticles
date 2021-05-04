# What's Up with Markdown?

![Markdown logo and a question mark](./whats-up-with-markdown.png)

Perhaps you've noticed a technology called Markdown that's been showing up in a lot of web sites and apps lately. Markdown is a simple way to format text using ordinary punctuation marks, and it's very useful in Microsoft 365.

For example, [Microsoft Teams supports markdown formatting](https://support.microsoft.com/en-us/office/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772)  in chat messages and SharePoint has a [Markdown web part](https://support.microsoft.com/en-us/office/use-the-markdown-web-part-6d73c06d-2877-4bc9-988b-f2896016c50b). [Adaptive Cards support Markdown](https://docs.microsoft.com/en-us/adaptive-cards/authoring-cards/text-features) as well, as do [Power Automate approvals](https://docs.microsoft.com/en-us/power-automate/approvals-markdown-support). For the bot builders among us, [Bot Composer language generation](https://docs.microsoft.com/en-us/composer/concept-language-generation) and [QnA Maker](https://docs.microsoft.com/en-us/azure/cognitive-services/QnAMaker/reference-markdown-format) both support markdown as well. And what's at the top level of nearly every Github repo? You guessed it, a markdown file called README.md.

This article will explain Markdown and help you get started reading and writing it.

## Designed to be intuitive

Imagine you're texting someone and all you have to work with is letters, numbers, and a few punctuation marks. (OK maybe an emoji or two as well 😁 - Markdown neither helps nor blocks emojis, they're just characters). If you want to get their attention, you might use `**asterisks**`, right? If you've ever done that, then you were already using Markdown! Double asterisks make the text **bold**.

Now imagine you're replying to an email and want to quote what someone said earlier in the thread. Many people use a little greater-than sign like this:

~~~markdown
> Somebody said this
~~~

Guess what, that's Markdown too! When it's displayed, it looks like this:

> Somebody said this

Did you ever make a little table with just text characters, like this?

~~~md
Alpha | Beta | Gamma
------|------|------
  1   |   2  |  3
~~~

If so, you already know how to make a table in Markdown!

Alpha | Beta | Gamma
------|------|------
  1   |   2  |  3

Markdown was designed to be intuitive. Where possible, it uses the formatting clues people type naturally. So you can type something in `_italics_` on the screen and it actually appears _in italics._

In all cases you're starting with plain text - the stuff that comes out of your keyboard and is edited with Notepad or Visual Studio Code - into something richer. (Spoiler alert: it's HTML.)

## Details details

Markdown isn't a formal standard, so unsurprisingly a lot of variations have emerged. It all started at [Daring Fireball](https://daringfireball.net/); most implementations are faithful to the original but many have added their own features. For example, the SharePoint Markdown Web Part uses the ["Marked" syntax](https://marked.js.org/); if you're creating a README.md file for use in Github, you'll want to use [Github Flavored Markdown (GFM)](https://github.github.com/gfm/).

This article will stick to the most commonly used features that are likely to be widely supported. Each section will show an example of some markdown and then the finished rendering (which, again, may vary depending on what application you're using).

### Emphasizing Text

~~~markdown
You can surround text with *single asterisks* pr _single underscores_ to emphasize it a little bit; this usually formatted using italics.

You can surround text with **double asterisks** or __double underscores__ to emphasize it more strongly; this is usually formatted using bold text.
~~~

You can surround text with *single asterisks* pr _single underscores_ to emphasize it a little bit; this usually formatted using italics.

You can surround text with **double asterisks** or __double underscores__ to emphasize it more strongly; this is usually formatted using bold text.

### Headings

~~~markdown
You can make headings using by putting several = or - signs in the line below.
--------------------------

You can also make headings with one or more hash marks in column 1. The number of hash marks controls the level of the heading.

# First level heading
## Second level heading
### Third level heading
#### etc.
~~~

You can make headings using by putting several = or - signs in the line below.
--------------------------

You can also make headings with one or more hash marks in column 1. The number of hash marks controls the level of the heading.

# First level heading
## Second level heading
### Third level heading
#### etc.

### Hyperlinks

~~~markdown
To make a hyperlink, surround the text in square brackets
immediately followed by the URL in parenthesis (with no space in
between!) For example:
[Microsoft](https://www.microsoft.com).
~~~

To make a hyperlink, surround the text in square brackets
immediately followed by the URL in parenthesis (with no space in
between!) For example:
[Microsoft](https://www.microsoft.com).

### Images

Images use almost the same syntax as hyperlinks except they begin with an exclamation point. In this case the "alt" text is in square brackets and the image URL is in parenthesis, with no spaces in between.

~~~markdown
![Parker the Porcupine](https://pnp.github.io/images/hero-parker-p-800.png)
~~~

![Parker the Porcupine](https://pnp.github.io/images/hero-parker-p-800.png)

In case you were wondering, you can combine this with the hyperlink like this:

~~~markdown
[![Parker the Porcupine](https://pnp.github.io/images/hero-parker-p-800.png)](http://pnp.github.io)
~~~

[![Parker the Porcupine](https://pnp.github.io/images/hero-parker-p-800.png)](http://pnp.github.io)

### Paragraphs and line breaks

~~~markdown
Markdown will
automatically
remove
single line breaks.

Two line breaks start a new paragraph.
~~~

Markdown will
automatically
remove
single line breaks.

Two line breaks start a new paragraph.


### Block quotes

~~~markdown
Use a greater than sign in column 1 to make block quotes like this:

> Line 1
> Line 2
~~~

Use a greater than sign in column 1 to make block quotes like this:

> Line 1
> Line 2

### Bullet lists

~~~markdown
Just put a asterisk or dash in front of a line that should be bulleted.

* Here is an item starting with an asterisk
* Here is another item starting with an asterisk
    * Indent to make sub-bullets
        * Like this
- Here is an item with a dash
    - Changing characters makes a new list.
~~~

Just put a asterisk or dash in front of a line that should be bulleted.

* Here is an item starting with an asterisk
* Here is another item starting with an asterisk
    * Indent to make sub-bullets
        * Like this
- Here is an item with a dash
    - Changing characters makes a new list.

### Numbered lists

~~~markdown
1. Beginning a line with a number makes it a list item.
1. You don't need to put a specific number; Markdown will renumber for you
8. This is handy if you move items around
    1. Don't forget you can indent to get sub-items
        1. Or sub-sub-items
    
1. Skip 2 lines to make a new list and start the numbering from the beginning.
~~~

1. Beginning a line with a number makes it a list item.
1. You don't need to put a specific number; Markdown will renumber for you
8. This is handy if you move items around
    1. Don't forget you can indent to get sub-items
        1. Or sub-sub-items
    
1. Skip 2 lines to make a new list and start the numbering from the beginning.

### Code samples

Many markdown implementations know how to format code by language. (This article was written in Markdown and made extensive use of this feature using "markdown" as the language!) For example to show some HTML:

~~~markdown
    ~~~html
    <button type="button">Do not push this button</button>
    ~~~
~~~

~~~html
<button type="button">Do not push this button</button>
~~~

### Tables

Tables are not universally supported but they're so useful they had to be part of this article.

Column 1 | Column 2 | Column 3
---|---|---
Value 1a | Value 2a |  Value 3a
Value 1b | Value 2b | Value 3b

## HTML and Markdown

Markdown doesn't create any old formatted text - it specifically creates HTML. In fact, it was designed as a shorthand for HTML that is easier for humans to read and write.

Many Markdown implementations allow you to insert HTML directly into the middle of your Markdown; this may be limited to certain HTML tags depending on the application. So if you know HTML and you're not sure how to format something in Markdown, try including the HTML directly!

## Editing Markdown

If you'd like to play with Markdown right now, you might like to try the [Markdown Previewer](https://mdpreviewer.github.io/) where you can type and preview Markdown using any web browser.

For more serious editing, Visual Studio Code does a great job, and has a built-in preview facility. Check the [VS Code Markdown documentation](https://code.visualstudio.com/Docs/languages/markdown) for details.

There's a whole ecosystem of tools around Markdown including converters for Microsoft Word and stand-alone editing apps; these are really too numerous to list but are easy to find by [searching the web](https://www.bing.com/search?q=markdown+tool).

## Legacy

From vinyl records to 8-bit games  and static web sites, there's a trend these days to rediscover simpler technologies from the past. Markdown definitely falls into this category.

Back before "WYSIWYG" (What You See Is What You Get) word processors were cheap and pervasive, there were "runoff" utilities that were very much like Markdown. They turned text files into nicely formatted printed documents (usually Postscript). Markdown harkens back to these legacy tools, but adds HTML compatibility and an intuitive syntax.

## Conclusion

While it may seem unfamiliar at first, Markdown is intended to make it easy for people to read and write HTML. Whether you're a power user, IT admin, or developer, you're bound to run into Markdown sooner or later. Here's hoping this article makes it a little easier to get started!