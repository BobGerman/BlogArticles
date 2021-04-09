# What's Up with Markdown?

Perhaps you've noticed a technology called Markdown that's been showing up in a lot of web sites and apps lately. Markdown is a simple way to format text using ordinary punctuation marks, and it's very useful in Microsoft 365.

For example, [Microsoft Teams supports markdown formatting](https://support.microsoft.com/en-us/office/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772)  in chat messages and SharePoint has a [Markdown web part](https://support.microsoft.com/en-us/office/use-the-markdown-web-part-6d73c06d-2877-4bc9-988b-f2896016c50b). [Adaptive Cards support Markdown](https://docs.microsoft.com/en-us/adaptive-cards/authoring-cards/text-features) as well, as do [Power Automate approvals](https://docs.microsoft.com/en-us/power-automate/approvals-markdown-support). For the bot builders among us, [Bot Composer language generation](https://docs.microsoft.com/en-us/composer/concept-language-generation) and [QnA Maker](https://docs.microsoft.com/en-us/azure/cognitive-services/QnAMaker/reference-markdown-format) both support markdown as well. And what's at the top level of nearly every Github repo? You guessed it, a markdown file called README.md.

This article will explain Markdown and help you get started reading and writing it.

## Designed to be intuitive

Imagine you're texting someone and all you have to work with is letters, numbers, and a few punctuation marks. (OK maybe an emoji or two as well 😁). If you want to get their attention, you might use `**asterisks**`, right? If you've ever done that, then you were already using Markdown! Double asterisks make the text **bold**.

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

Markdown was designed to be intuitive. It turns the formatting clues people type naturally into rich text that's  formatted on the screen. So you can type something in `_italics_` on the screen and it actually appears _in italics._

In all cases you're starting with plain text - the stuff that comes out of your keyboard and is edited with Notepad or Visual Studio Code - into something richer. (Spoiler alert: it's HTML.)

## It's retro

From vinyl records to 8-bit games  and static web sites, there's a trend these days to rediscover simpler and sometimes better technology from the past. Markdown definitely falls into this category.

Back before "WYSIWYG" (What You See Is What You Get) word processors were cheap and pervasive, there were "runoff" utilities that were very much like Markdown. They turned text files into nicely formatted printed documents (usually Postscript). Markdown harkens back to these legacy tools, but adds HTML compatibility and an intuitive syntax.

