# Do I really need ngrok to build a Microsoft Teams application?

If you've started down the path of developing applications for Microsoft Teams, you may have seen a tool called [ngrok](https://www.ngrok.com) as a prerequisite in various tutorials and lab exercises. This is fine for many or most developers, and I count myself as a big fan of the tool! It gives some people heartburn, however, for a couple reasons:

* ngrok creates a tunnel from the public Internet to your local computer, which may be a security concern. A number of partners and customers I've worked with indicate that ngrok and similar tools have been prohibited in their organization for this reason.

* ngrok's free service provides a new URL every time it's run, or every 8 hours, whichever comes first. This generally means reconfiguring the application in some way when the URL changes. The alternative is to [pay for ngrok](https://ngrok.com/pricing); with the paid service you can reserve a public URL that won't change.

These issues have led quite a number of people to ask, "Do I really need ngrok?"

The consultant's favorite answer applies: "It depends."
My slightly more useful, short answer is, "Probably not, but it's likely the easiest option if you're ok with the issues above."

This article will explain, and help you determine if you need ngrok, or if you can't or would prefer not to use it, what options exist.

## What does ngrok do anyway (hint: it's more than just tunneling!)

Here are the features of ngrok that make it the darling of so many developers:

1. **Tunneling** - Of course the premier feature is tunneling. Typical firewalls or even home routers allow connections one way - that is, your computer behind the firewall can connect to computers on the Internet, but computers on the Internet can't initiate an inbound connection to your computer. 

    The tunnel creates a new IP address and hostname on the public Internet that will relay incoming connections through to your computer, thus bypassing any firewall that may be in place. For example if the Azure Bot Channel Service wants to send a message to a Teams bot you're debugging, it can't call directly, so ngrok saves the day.

1. **HTTPS Support** - Most modern web sites and web services require HTTPS and not HTTP, and for good reason! HTTPS provides privacy by encrypting the data between the client and server computers. Notably, the popular OAuth protocol used for authentication and authorization by Microsoft 365 and many other services isn't encrypted. A bad actor could steal an OAuth token from an HTTP message and use it as if they were the user (a so-called "man in the middle" attack.) To prevent this, HTTPS is considered a requirement for secure operation, and Microsoft 365 insists on it.

    Setting up TLS requires creating and installing a digital certificate which is used in generating the encryption key. You can avoid this by using ngrok, since HTTPS is built into the service. For example can tunnel from https://<something>.ngrok.io to http://localhost and avoid the setup.

1. **Name resolution** - The Domain Name Service (DNS) translates host names into IP addresses. This isn't a problem if your IP address is "127.0.0.1" (the local loopback address) since "localhost" is a widely known name for this address. But if you want to access your program from another computer the "localhost" option won't help. A good example is for testing your app from a mobile device; the device needs a way to access the service you're debugging on your computer.

    Again ngrok provides this with no extra effort. By translating localhost URLs into public ones such as https://<something>.ngrok.io, you can try test your app from a smart phone or tablet with no additional steps.

So while ngrok is clearly very useful, there are alternative approaches to handle each of these cases. The sections that follow will provide details.

> An alternative tunnelling ngrok is not the solution.
> Many people have suggested other tunneling applications such as [Azure Relay](https://blog.botframework.com/2019/04/16/debugging-your-locally-hosted-v4-bot-using-azure-relays/) or [localtunnel](https://localtunnel.github.io/www/). While they may be helpful in some ways, they all open a tunnel from the public Internet to your development computer, and thus the same security concerns usually arise. This article will only consider alternative approaches that do not expose any ports on the local computer to the public Internet.

## Building Teams tabs and task modules

Both tabs and task modules (modal dialogs) in Teams are web pages that appear in IFrames in the Teams user interface. Teams requires https on the URL of these web pages. It's notable that the Teams client accesses these web pages directly, so as long as your Teams client or web browser can access the page with https, it will show up in Microsoft Teams.

This picture shows how ngrok works in the case of a tab or task module. The Teams client (or web browser) opens the web page via the ngrok tunnel, which sends the connection right back to the local computer.

![Picture showing that Teams client access via ngrok is really just a loopback](./ngrok-tab.png)

In this case no tunnel is needed as long as the Teams UI is running on the same computer where you're debugging. 

ngrok is really doing a 


## Building Teams bots and messaging extensions

## Is ngrok secure?

Note that this is only my personal opinion; please consult a security specialist for an authoritative answer.

I think ngrok can be secure if it's used as intended. It opens a single local port to the Internet; this port is the one I'm using for my debug session. If someone started accessing my public ngrok URL, the worst thing that they could do is confuse me as I'm trying to debug my work; there is nothing of value to be had.

However I do understand why IT may object to ngrok and similar tools. An insider could leave it running on a computer under a desk somewhere as the basis of an attack on a corporate network. Once the tunnel is set up, they could log into this relay computer remotely, use ssh commands, or even write a small proxy server to relay the messages from the tunnel to other computers. Any of these methods could be used to gain broad access to the corporate network from from somewhere else. One could argue that a well designed corporate network might mitigate such attacks via IPSec and other policies, but most of the corporate networks I've seen aren't so sophisticated, so "no" is the easy answer.







