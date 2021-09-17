# HTML

HTML is a fundamental building block of the web, on top of which all website functionality is built.

HTML is where we're starting, because it's the absolute easiest structured language you can learn and produces immediate, gratifying results, that will hopefully keep you interested in coding as well as give you a playground that you can build upon and actually see your results in a web browser.

HTML stands for Hypertext Markup Language. This means it's  *markup* language, not a programming language. It is just a way to tell the web browser (e.g., Chrome, Firefox, Edge, Internet Explorer) how and what to display to the user.

It was originally just created for displaying documents at the inception of the internet, but additions kept being added to make websites capable of what they are today.

## Server/Client relationship

Websites are connected to the internet through servers. A server is just a program that listens for client requests.

A client is anything that connects to a server and asks for a resource.

So, for instance, a resource could be an HTML file.

For example, the address https://www.google.com points to a server. When you type https://google.com into your browser, your browser sends a request to that server's home page. If all goes according to plan, https://www.google.com replies to that request with an HTML file.

There are other kinds of requests a client can send too, but they're generally sent after the initial request for the home page.

## Assignment

You assignment is to create a web site for Penelope, our cub.

This is going to be a plain HTML website, meaning it won't have any CSS or JavaScript (concepts we will cover later). This inherently limits the functionality though, which is ok, though, because we will more functionality on  to it later.

First though, you are going to need to learn the concepts of HTML. So the first step is to create an account at https://codecademy.com  and complete the HTML module. This may take a few days, but stick with it!

Next we're going to create an actual website! But the server is going to be your own computer.

Your browser is capable of requesting files directly from your computer. But instead of the scheme `https://`, you use the scheme `file://`. The `file://` scheme indicates you would like it to display a file at the given path on your computer.

You can test this functionality by dragging a plain text file to your browser. Find or create a plain text file (with a `.txt` extension) and drag it to your web browser. The address should have the scheme `file://`.

The scheme (e.g. `http://`, `file://`, `http://`, etc.) tells the browser how the resource should be handled.