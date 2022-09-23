<h1>My SDC Journal</h1>
<h2>Lessons Learned</h2>
<span>I chose to study on front end perfomance, specifically images. While I do feel there is plenty to learn in the area, a lot of performance, from my experience, is handled by caching.
<br>Anyway, here are my findings.
</span><br></br>
<h2>Images</h2>
<ul>
With NextJS in our groups case, I looked at load times, and noticed a freshly opened application with no initial editing had a perfomance rating of <b>~55</b> every time. Once I implemented the changed to images, fonts, and cleaned up javascript code I was able to achieve a local running time of <b>~63</b> everytime. With NextJS caching at its default state on the live application on render, This time jumps to <b>~93</b>, noting that caching had made a lot of my work actually obsolete, unless someone visits for the very first time. Lighthouse reports still tells me to properly size my images, but I also don't show the same report on the live site and I also followed Next JS documentation.<br></br>
<li>The correct format is important. PNG seems widely accepted, currently, as the standard for web applications. The ability to incorporate images with transparency with the ability to choose color density (PNG-8 vs PNG-24) vs practicality is very profound for a designer/developer. Below is from "https://www.designpowers.com/blog/image-file-formats": </li>
Pros: 

    Universal browser support

    Supports transparency

    Best used for graphical elements

    Lossless compression

    Small file size with limited colors

Cons: 

    Large file size with millions of colors

    Not ideal for printing–optimized for the screen


I actually used transparency from PNG in my very first front end project and didn't realize that was a benefit of PNG. The fact that it has univeral support is also huge. Now, for SDC, compression was a big deal and I was able to use Next JS to lower the quality of the photos with the "quality" attribute in an Image element. They difference for 75% and above, from my experience, was negligible. Also, I learned I was implementing the Image incorrectly, as it should be wrapped in a div. Overall, for implenting photos/images, I suppose my takeaway could be to make sure to look at file size, file type, and compression options.

</ul>
<h2>Preconnects/Preloads</h2>
<ul>
<li> Another thing I discovered while working with images and making load times faster was that the way I had implemented the font was incorrect, or at least not optimal. You should "preconnect" the font, and if you choose a font from google fonts, they come with the correct preconnect settings which I had omitted from the application the first time. For Next JS you need to utilize _document.js and <i>not</i> the css files or any other file as that will slow down your load times. Although in some instances you may see unformatted text, most cases will render a first over "flash of invisible text" or FOIT.</li>

</ul>
<h2>Caching</h2>
<ul>
<li>One very large difference in my lighthouse test was caching. I understand that in order to cache things, you still need to visit the website at least once. However, once you have a cache from the appliation or site, your load time improves dramatically. The user is able to get the first meaningful paint very quickly even with a lower connection speed. Using Next JS default caching, as I previously mentioned, brought the average score to <b>~93</b>. Caching is a neat way to do things and you should make sure that if you intend to have repeat users to definitely optimize your cache appropriately.</li>

</ul>

<h2>Some Takeaways</h2>
<p>For large sites and applications, like airbnb.com, its understandable to have longer full paint time with a lower rating on something like lighthouse. If you visit the homepage and run lighthouse I got about a 39% rating for airbnb. However, from a user experience perspect, on desktop with highspeed internet, I waited about 3 seconds to see a full website. With caching, I waited about 2 seconds, so roughly 33% less waiting. The youtube video "The cost of JavaScript" says that you should aim for an interactive application in under 5 seconds. Even with large blocking time, this is easily achieveable with having certain items preloaded (or maybe pre-rendered on the server, even). But having that cache of important information is important, as well as not sending too much data right away, like images (let them load while you render the rest). Scale things down and preload what you need.</p>