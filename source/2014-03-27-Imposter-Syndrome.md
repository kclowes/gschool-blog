---
title: Impostor Syndrome
date: 2014-03-27 22:12 UTC
---

I have read so many articles, blogs, etc. about impostor syndrome, and how prevalent it is in software developers. And I feel
like I can relate to every single one of them in some way. As I am beginning to have a visceral understanding of what
software engineers do on a daily basis, it is no wonder this 'syndrome' is so common. There is always a newer and better
way to do things out there and always something to learn. We frequently fail. Sometimes on purpose. Since we practice
test driven development in gSchool, we have to fail before we move on to make sure our tests are working properly.

If you are struggling with impostor syndrome, I highly recommend the following article:
[Overcoming Impostor Syndrome by Alicia Liu](https://medium.com/tech-talk/bdae04e46ec5 "Impostor Syndrome"). The stigma
associated with software engineers is that they have been coding in basements since their age reflected single digits,
and in that time they have amassed huge amounts of knowledge. While this is certainly true for some, many of my classmates
do not fit that mold. We have been exploring what it means to become developers as adults. I am so grateful that I have
the opportunity to learn in an environment where failure is required on a daily basis. It makes the act of failing
way less intimidating because it is inevitable but also encouraged.

In the spirit of feeling like an impostor, we learned a little about Sinatra this week, and I am going to attempt to
explain what happens when a GET request is issued from the browser. We learned about sequence diagrams and
how to draw them, about the controller and views. When a GET request is issued, the browser pings the controller. The controller
tells the database (or wherever you are storing your data) which item it wants and the database sends it back to the
controller. Then, the controller tells the HTML to render. When it is rendered, the app then sends the HTTP response
back to the browser. If all is good, you have a response code in the 200s. A response code in the 300s is also okay
because it means that the page will be redirected. 400s mean client error, and 500s mean there was a server error.
According to the Mozilla Developer Network, response codes in the 100s are informational. I haven't seen very many
100 codes, but I also haven't looked very hard for those. You can see the response code by right clicking on the page somewhere,
and selecting 'Inspect Element'. If you reload the page, you can see all sorts of fun things. I provided a screen shot showing
where the status code is below:

![alt text](/images/inspect_element_ss.png "Inspect Element SS")

A note to the wise: you have to make sure that you reload the page while you have the 'Inspect Element' window open or else nothing will show
up.

Below is an example of the code that the controller uses in Sinatra to render the erb:

![alt text](/images/get_request.png "Get Request")

This little guy puts the block in the heap until a GET request is issued from the browser. When a GET request is issued the do block
gets added to the stack to be executed. How cool is that?