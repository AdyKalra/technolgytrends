1. You Aren’t Gonna Need It (YAGNI)
  Don’t write code that you don’t need right now. It’s tempting to write some extra code because you think you will need it later on. The problem here is twofold.
  You probably don’t need it after all. Now there’s code just sitting there unused, and nobody dares to remove it because who knows what will break if they do.
  Unused code does not get updated. It can introduce bugs and security vulnerabilities that didn’t have to be there in the first place.
  Save yourself the time; you aren’t gonna need it!
2. Avoid Premature Optimization
Just like YAGNI, it is also tempting to optimize your code prematurely. The risks here:
Your code will be less clear to others.
You will spend time on a problem that likely doesn’t exist.
Let’s elaborate on these two points.
First, optimizing your code for speed often makes it more difficult to understand. Instead of taking the obvious, easy route, you’re implementing stuff like caching or loop unrolling or whatever fancy technique in places where it’s simply not needed.
You are adding complexity, and complexity has many downsides (see also: KISS).
Secondly, you don’t know how your code will perform until you run it. So, please don’t spend time optimizing it until there’s an actual problem.
More often than not, you'll find that it doesn’t matter how fast your code is. CPU cycles are cheap; working hours aren’t. You can just as well add more CPU power or wait a little longer and avoid complexity and potential bugs.
3. Don’t Be Clever
I prefer clarity over cleverness. Some super cool one-liner tricks might be nice for showing off but are a pain for those that read your code in the future. Don’t be that person. Post the cool tricks in your blog instead.

Photo by Olivia Bauso on Unsplash
I put a perfect example of this in another article of mine. Below is the code to trick #19 from that article. Can you figure out what it does by yourself? How long did it take you?

This code is more comprehensible if it is split up into multiple lines, with a comment or two to explain the arguments to the max() function.
Make your code as easy to understand as you possibly can. Assume it needs to be understood by another programmer who’s in a hurry to fix your bugs a year from now.
And let’s be honest. That other programmer might be you because a year from now, you’ve forgotten about that neat trick as well.
Van Rossum has said it himself during his time at Dropbox:
“Maintainable code is more important than clever code.”
4. Don’t Repeat Yourself (DRY)
Beginners often repeat code, doing the same or almost the same things. Say you want to open a file and read its contents. You can write a few lines and do so easily.
But if you need to read another file and get the contents of that one as well, don’t write the same code to open this different file. Or worse: copy-paste it!
Instead, you should realize that you can create a function instead. Two significant advantages here are:
Less code is easier to maintain and debug.
Small functions are easy to test (see Unit Testing).
A well-named function is a form of documentation (see: Document your code).
Pro tip: Some IDEs detect duplicate code and warn you about it, and some even help you extract methods or functions from the duplications.
5. Create Unit Tests
Unit testing is overlooked by many. I am guilty of this too. I often find myself creating unit tests after the fact, if at all. But even if you’re adding them after the fact, it’s still better than not adding them at all.
In the most extreme form, you apply a practice called test-driven development (TDD). With TDD, you first create a unit test and then implement the function. It forces you to test each function you create and think carefully about what that function needs to do and what the expected output will be. A good book covering this topic is Test Driven Development: By Example.
Another advantage of creating unit tests is that you or others can change the code with much more confidence. After the change, you run all the tests. If nothing fails, the chances that you just created a breaking change are slim.
Creating unit tests helps you to:
Write better code with fewer bugs.
Adapt your code with more confidence in a later stadium.
Force you to create smaller functions that do one thing.
Document your code by giving usage examples.
6. Keep It Simple, Stupid (KISS)
This powerful mantra is not just used in software development. In essence, it means “don’t overcomplicate things” or “try to think of the simplest solution possible.”
Dijkstra, one of the pioneers of computer science, once said: “Simplicity is a prerequisite for reliability.” The simpler your solution is, the harder it is to introduce bugs. As simple as that.
“Simplicity is a prerequisite for reliability.”
7. Adhere to a Fixed Code Style
Adhere to a coding style. Especially when working in teams. As an example, some people prefer to use accolades like this:
while (true)
{
  // do cool stuff
}
While others prefer this more compact style:
while (true) {
  // do cool stuff
}
Both have pros and cons. But by all means, stick to one. If you are in a team, that might mean you’ll need to stick to a coding style that does not have your preference.
Each language has its tools and de facto standards in this regard. You’ll need to Google around for the best practices for the language of your choice. Also, for most languages, there are auto-formatters that you can install in your IDE. It can save you lots of time so make sure to find one that you like.
Here are a few links to get you started:
Google has style guides for many languages.
For Python, there’s PEP8. Many IDEs have PEP8 plugins that check your code as you type.
For Java, you can use tools like Checkstyle to define a style (or use one readily available) and enforce proper code styling during compilation. Some IDEs also help you in this regard after some initial setup.
8. Document Your Code
There are three ways to document code:
Using comments inside of your code.
Writing documentation in a separate document.
Writing self-documenting code.
To start with comments: use them sparsely. Only use comments where clarification is needed and do not state the obvious.
Writing documentation can be beneficial. Think of all those GitHub repositories. It has become a de facto standard to include a README.md file in the root of your project.
This file describes a few essential things:
What is this code? What problem does it solve?
How can you start working on this code? Include specific instructions to create a development environment, if any.
How do end-users use the software?
Offer related links, like more documentation, background info, etcetera.
Where and how should people ask for help?

Clear directions can save lives in some sectors. Photo by Calle Macarone on Unsplash
Most important of all is to write code that documents itself. This is also the hardest part because it requires experience and best practices. To illustrate this more, here are a few things that help:
Use good design, so your codebase is easy to navigate and structured logically.
Follow best practices, like DRY (don’t repeat yourself), YAGNI (you aren’t gonna need it), and KISS (keep it simple, stupid).
Don’t try to save characters. Use full names for your variables, classes, and functions. So, instead of wm, name it windowManager. Instead of rf, call it readFileToString. This name helps tremendously when others — or yourself, after a few months of not looking at the code — try to understand what’s going on.
Extract as much as you possibly can into functions and make these functions do one thing. Name them accordingly, and start with a verb. For example, a function that reads a file into a string could be named readFileToString(String fileName). Without reading the code in detail, people will know what it does. Ideally, your code is a sequence of function calls like this that almost read like human language. Only when needed, the reader can dive in deeper. This code documents itself!
9. Asking for Help: The Right Way

Photo by Jametlene Reskp on Unsplash
A professional only asks for help after extensively trying to find an answer in other ways. Before you ask a question:
Read the documentation — also called RTFM, short for “read the f***ing manual.”
Search Google for the answer if the documentation is not clear enough or does not solve your problem.
If that didn’t help, consider where to ask for help first:
A bug tracker is not the place to ask questions that are not about (potential) bugs.
A developer mailing group is intended for developers working on the product, not developers using the product.
Many projects have a page instructing you how and where to ask questions.
There are large Facebook groups dedicated to specific programming languages and technologies to ask more general questions. In my experience, they can be messy and have a lot of noise, but often you’ll get your answer, so it’s worth checking those out.
Finally, before writing down your question, take these points in mind:
Be kind, be grateful. The people that answer you and try to help you often do so in their spare time, for free.
Be as detailed as possible. Provide context: what are you working on, why, what have you tried so far?
Include error messages, (parts of) log files, and the code giving the problem. Don’t dump entire files. Only include what is needed to get proper help.
In general, be respectful of other people’s time.
10. Refactor
Refactoring is restructuring your code without changing its behavior.

Photo by Michał Parzuchowski on Unsplash
Why on earth would you do that? Well, to improve your code, obviously! There are a few facts of life that make refactoring necessary:
Your software never comes out perfect on the first try. It may work, sure, but it will be messy, and there will be duplication.
Computer code is continuously evolving. Even if you start with a perfect code base, it can get messy very quickly.
When working on a new project, you initially need to make significant changes, like reordering your initial draft into classes. Once that is done, the refactoring does not stop, though.
You should make a habit of making gradual improvements every time you work on the code. Leave a piece of code better than you found it, every time.
Small improvements you make over time add up to a codebase that is easy to read and maintain.

Don’t let your code evolve into a minefield. Photo by Robert Bye on Unsplash
An important effect of constant refactoring is that your code is less likely to turn into a minefield for others.
Perhaps you’ve seen such code before. The type where, if you change one line, the whole thing breaks incomprehensibly. By constantly refactoring, restructuring, and improving your code, you prevent it from turning into a minefield.
11. Be Professional

You don’t need to wear a suit to act like a professional. Photo by Hunters Race on Unsplash
You’re a professional. We are professionals. We work in a field of expertise that is in high demand. Don’t let anyone, anywhere, shoot you down. There’s still some undeserved stigma around people in IT, so let me state it clearly:
You’re not a geek.
You’re not a nerd.
You’re not “that computer guy/girl.”
You’re a software engineer, a data engineer, a data scientist, perhaps. Whatever it is you’re called, you’re a professional, just like lawyers and dentists are professionals.
You’ve learned and worked hard to do what you do. You possess the expertise that is required in pretty much every industry. Act like the professional you are. Don’t be afraid to call out those who don’t treat our profession with the respect it deserves.
12. Keep Learning
A professional keeps learning for the duration of their career. There is one constant in the world of IT, and that constant is change.
New languages are introduced each year. New JavaScript frameworks seem to be introduced each day. You have to keep learning to keep your knowledge relevant and up-to-date.
If you liked this article, here are some book titles that will help you become a better software engineer:
The Pragmatic Programmer — From Journeyman to Master
The Mythical Man-Month — Essays on Software Engineering
Clean Code — A Handbook of Agile Software Craftsmanship
The Clean Coder — A Code of Conduct for Professional Programmers
Clean Architecture — A Craftsman’s Guide to Software Structure and Design


[the-12-habits-of-highly-effective-software-developers](https://betterprogramming.pub/the-12-habits-of-highly-effective-software-developers-fffb15dc9b15)
