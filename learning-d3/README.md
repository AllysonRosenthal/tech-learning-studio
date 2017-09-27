# Learning D3

## Week 1
Things I did:
 * Cloned the [textbook repo](https://github.com/AllysonRosenthal/d3-book)
 * Set up development environment for D3
   * Download D3
   * Create index.html
   * ~Set up a local server using Python~

### In Class
I spent today trying to get off the ground with D3. There's a pretty big chunk of assumed knowledge around web programming (which Murray warns about in the first chapter of his book). I thought I'd be in good shape, since I have a solid grasp of how HTML, CSS, and JavaScript work. 

It turns out that there are quite a few things that didn't come with warnings, since Murray assumes you either are already comfortable with certain tools (Git, in this instance) or will avoid them. I'm actually in a middle ground, where I am *familiar* with Git, but not quite *comfortable* with it. Luckily, all of my simple questions have been asked before, and I was able to find the answers via Stack Overflow and the GitHub help documentation. So, I was able to get the bulk of the first project set up, but more slowly than I would have liked. 

I also ran into a problem with the command line developer tools, which I had to install for inscrutable reasons. I've used Git from the command line with no problems before, so I'm slightly baffled by that one. Again, this hiccup was easily overcome, but waiting for the download and installation slowed me down.

### Outside of Class
I'm going to be sure to get the setup finished, so I can spend my time in class next week actually working through the textbook and examples. I'm also going to investigate how to share the project through bl.ocks.org, since it looks like that isn't covered in the textbook that I've chosen, but would be my preferred method for turning in this project.

**Update 9/13/17**: Instructions for sharing a D3 project using bl.ocks are available [here](https://bl.ocks.org/-/about). Learning about how bl.ocks pulls in your projects via GitHub gists lead me to [this page](https://help.github.com/articles/about-gists/), which I found to be a helpful overview of gists.

#### New Project
I attended one of [Open Austin's](https://www.open-austin.org/) Civic Hack Nights on Tuesday, September 12th (which was the evening before our weekly class meeting). While there, I got plugged in to a [visualization project](https://github.com/open-austin/consumer-protection) using the city's data on consumer financial complaints. We decided to use D3, since I told the project lead that I'm working on learning D3, and he was cool with using this project as a learning opportunity. 

Since I had yet to actually start working through any examples, I basically still had no idea how to start writing D3. So, we started from someone else's example. Once we changed the data reference to point to our data instead of the example data, everything just stopped working. The error said the data was `NaN`, despite the CSV clearly containing numbers. The whole evening ended up going to trying (and failing) to troubleshoot that issue, but now that I'm set up with a project, I can use it to reinforce the examples in the book.


## Week 2

Things I did:
 * Set up a local server
 * Made bars show up
 * Got those bars to reflect real data

### In Class
#### Issue #1
The book tells you how to set up a Python web server with `SimpleHTTPServer`, but doesn't tell you how to stop it. So, when I went set up the learning-d3 project, I was already using the recommended port for my tech-learning-studio folder. It was easily fixed by 1. trying a different port and 2. a Stack Overflow thread with the solution, but it's a little frustrating to be asked to run a command with no note about how to kill the process.

You can actually navigate from the tech-learning-studio folder to the learning-d3 folder if it's already being served by adding the filepath to the URL. Basic, but unlikely that anyone who needs setting up a local server explained (as in Chapter 4) will know how to navigate it once it's set up. I only figured it out after looking at the URL containing the full filepath in the Chapter 5's first example.

#### Aha moment #1
Scott Murray calls out an almost impossible to debug issue in Chapter 5: When a CSV is pulled into D3, everything is a string. You can only see that it's a string by logging the data to the console *after* it's been pulled in (which is why we kept getting the `NaN` error yesterday, even though it was a number...before getting pulled into the script). Having an in-progress project that let me see the problem play out and then finding the solution was really satisfying, and I'll definitely remember this gotcha in the future. If I had just been reading through the chapter, I probably would have skimmed right over that very important detail, and been at a loss as to why everything was broken when I inevitably forgot to convert the strings to floats.

#### Aha moment #2
After calling `data()` in a function chain, you can pass `d` into an anonymous function to actually get at the individual data values in your dataset. As someone who has done even minimal programming before, this capability is borderline magic. It's so easy! You can't screw up getting the right value attached to the right element! D3 just *does it for you*. I'm starting to see the hype around D3 itself, instead of just the lovely examples of what it can produce.

Overall, I find myself getting distracted by how the web works. To get by with D3, you only need a high level understanding of it, but it's pretty fascinating stuff, and I keep finding myself down rabbit holes when I search a term from the book. To keep that curiosity productive, I may switch my second D3 project to exploring a web framework instead. A preliminary search suggests Flask is the best entry-level framework, and it would build on my existing familiarity with Python, which has been withering in the year or so since I've used it.

### Outside of Class
I set aside some time to work on the consumer protection project. Having a project that isn't just for class is a good motivator for me to work on it more often, especially since Open Austin meets roughly once a week, so the project lead is likely to check in with me in person. 

I was able to work through enough of the chapter on bar charts to make something that actually shows up in the browser, which is awesome and validating. Along the way, I ran into some trouble getting the data to load in a useful manner. 

#### Issue #2
The book example used a hardcoded array to keep the examples simple, but that made it hard for me to troubleshoot my minimally complicated CSV loading by looking at a version that works. Eventually I just flipped around the book looking for examples and cross-referencing them with their sample code online until I found one that helped.

#### Issue #3
While the dataset was loading from the CSV, Javascript just kept running and went ahead to the function that needed the dataset, which cause an `undefined` error. 

So, I needed my function that was using the dataset to be inside or chained to the function that loads the data. I was able to figure it out because the errors and my `console.log` outputs were showing up out of order. The data wouldn't show up because it hadn't loaded yet, even though it was loaded "before" the function in the code.

I had a strong feeling that had something to do with it, since that's called out in the book as an issue. I had read that section about two weeks prior, so it was just a niggling impression that I had heard this "song" before and naming it was on the "tip of my tongue," so to speak. That's a huge benefit of actually sitting down and reading a textbook vs. jumping between the relevant parts (which I did start doing because I got excited about things starting to work. Basically, my inquiry into learning D3 started to be driven by, "okay, so how do I do this thing that will make what's in front of me better?" instead of "how do I do all of D3?").

While I was troubleshooting, the problem wasn't so much that I didn't know how to fix the problem, it's that I didn't know what the problem was. The process of finding a name for the problem was the most challenging part of the day. I could have asked for help, since the project lead happened to be in the cafe I was working in (I was hanging out across the street from the location for the next Open Austin meetup a few hours before it started, so it wasn't a wild coincidence) and told me to let him know if I needed help with something, but I wanted to figure it out myself. I feel that the biggest part of being a self-sufficient programmer is being able to debug your own code. I think of it like cooking: anyone can follow a recipe if someone hands them all the pre-measured ingredients, but you're only winning *Chopped* if you can take whatever the mystery basket throws at you. It's still nice to feel supported, though, and I would have asked for help if I hadn't had that inkling of what was wrong thanks to reading the textbook.

#### Aha moment #3
I wasn't totally wrong about what was happening in Aha moment #1, but I was missing a big chunk of how D3 stores data in my mental model. The `NaN` error came up again, and I was extremely sure the data was a after Aha moment #1. This time, this issue was that each item is an object, and thus `NaN`. The object has the numerical data attached to it as an attribute, so you have to tell D3 which part of that object is a number. I repeatedly clicked on the actual word `Object` in the console output to confirm that the data was a number, not a string, before it suddenly dawned on me that the items in the array were, in fact, objects, not numbers. 

## Week 3

### In Class
As I'm trying to work through some of the examples, I keep getting frustrated by not understanding *why* a particular thing behaves in certain ways. I'm not really satisfied with a function inexplicably working when it's rearranged (to reuse the issue I ran into earlier in the week as an example), and will find myself stuck, not because I can't get something to work, but because I don't know why one of the ways I poked at the problem was the magic solution. 

As I've had more moments where I figured out why something works, I've realized that the structure of the book frequently introduces a scenario that I'll never use again as the "simple" task before building up to something more common. I've been letting myself get stuck on those tasks without moving on to the examples that are relevant to using D3 in practice. Today, I've been trying to catch myself getting hung up on the details of the very first example I'm given, and letting myself move on to the examples that build on (and further explain) those concepts. So far, doing that has let me recontextualize my questions with the next example, and I've had more concepts click by pushing forward and trusting that I'll get it if I let the preliminary example go for long enough to consider another application of that concept.

## Week 4
 * yet another NaN error when I tried to scale the data
 * solved by copy-pasting the error message into Google -- Stack Overflow to the rescue
 * the prevailing convention (in both the book and the issue + solution on Stack Overflow) seems to be accessing an object's attributes by index using bracket notation
 * I prefer using dot notation so far -- it lets me access what I want by name, which makes it easier for me to see what's going on, and it's easier for me to remember the name of what I want vs. its position in the object's attribute array
 * operating under the assumption that these people know more about d3 best practices than I do, I looked up dot vs. bracket notation in d3, and found [this page](https://medium.com/@prufrock123/js-dot-notation-vs-bracket-notation-797c4e34f01d), which provided a solid explanation of why bracket notation will work in many more cases than dot notation. Essentially, JavaScript only reads dot notation as explicit string keys associated with that object. Brackets, on the other hand, are evaluated as you go, and therefore give you a lot more flexibility in how you access that information (especially with things like loops). 
 * it takes way more time to make the graph useful than to make pretty blocks of color (scales, axes, labels)
 * **Issue**: inverted y-axis (0 at the top) -- huge pain to troubleshoot (each thing that I fixed introduced another issue -- ex. flipping yScale also flips direction that bars are drawn)
 * book example is a scatterplot
 	* d3 is really not designed for bar charts -- there are way faster and easier ways to get there. But, as a learning tool, I thought making a bar chart would be fine anyway. If I could do it again, I'd actually start from a slightly more complex project (even something just one step up, like a scatterplot). D3 handles complexity so well that it seems like its more difficult to get it to do something simple. On the other hand, it's forced me to really isolate what I want d3 to do and how to get there, which I think has led me to a deeper understanding of what I'm doing than I would have otherwise gotten to.
 * Update: the book does revisit bar charts in Chapter 9. I'm a little annoyed that this further discussion of scales is two chapters after the actual chapter on scales. While this structure works if you're genuinely sitting down and working through the entire book, it makes it much harder to use as either a reference or a guide for your own project. Plus, the main content of the book goes on until the appendices start on page 359. It seems pretty out of line with most people's attention span to expect a reader to go through every single page, and it's definitely out of line with my own attention span.

