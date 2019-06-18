# Capstone Project fail notes
### Fixing the footers
I noticed that the footers on the original site were linked to an image that no longer existed. I wanted to fix this, but in a way where it would not happen again. I searched online for a good quality `.jpg` file of the Carleton University crest, and saved a copy of it in `~/images/`. I then put the url (found by opening the image in GitHub and right clicking `open in new tab`) to that into this code, which I then put on the bottom of every page.
```
</div>
	<div class="footer2">
		<div class="container">
			<p>
			</p>
			<p><img src="<URL>" height="45"> Carleton University History Department</p>
		</div>
	</div>
```
### Deleting extranous pages
I noticed that there were still many pages from older projects left in this repository, which I decided to delete because they were taking up space and had the chance of confusing anyone that would look into the repository. I made sure that I was only deleting files that were unrelated to Canada's atomic history by opening the HTML file and reading it. 
### Changing urls to my github account
I also noticed that when I forked this repo, the urls still linked to the older site, which I was not working on. I could have fixed this more easily by using regex in order to find and replace the previous creator's username with my own, but due to impatience and not wanting to deal with having to download the files and then reupload them, I instead manually replaced them all. 
### Fixing a code error
The original site had an error in its code, having `html lang=“en”>` at the beginning of each page, which I noticed that I was able to see for a split second when refreshing the pages. I realized that this was because the code was not complete, and simply added a `<` to the beginning of each HTML page so that they said `<html lang=“en”>`. This completely resolved my issue. 
### Changing the map
While the original black and white map was useable, I decided that I didn't really like it, mainly because it was SO plain. When making data visualization, it is important to balance aesthetic with data, and for them to compliment eachother.

Looking through the original code, I noticed that the map was made with Stamen, so I then decided to look online and see if I was able to customize a map with that. From there, I found the template for stamen maps, which was `http://<server>/<customizations>/{z}/{x}/{y}.jpg`. I then tested it out by replacing `toner` with `watercolor` in this piece of code from `index.html`:

```
var map = L.map('map', {
    center: [57.35, -88.35],
    zoom: 4,
    layers:[
      L.tileLayer('https://stamen-tiles-{s}.a.ssl.fastly.net/toner/{z}/{x}/{y}.png'),
     
    ]
});
```
Doing this changed the map on the site from black and white to a nice watercolour, but it lacked borders and place names. By looking around Stamen more, I found their service MapStack, which allows users to create a map using their options. With this, I decided that I liked the watercolour, and so kept that as a layer. I did change the original watercolour (which was beige/brown and blue for land and water) by altering the colour, choosing a shade of green that was both calming, but also reminiscent of toxic waste. I chose this colour because it is pleasant to look at, but also conveys informtion about what the site is conveying: atomic experiments and nuclear activity creates toxic waste that affects everything from the land to water. I also added a layer from the toner map, which contained borders and place names. With this new map, there is no obvious way to get a url that would work as a map, but I figured it out!

To do this, I right clicked on the map, and and chose “open in new tab”. The customizations here exist between `.com/` and `/{random number}`. I then copy and pasted them into this URl template `http://{s}.sm.mapstack.stamen.com/<customizations>/{z}/{x}/{y}.png`, and then inserted this this URL into the index.html page here:
```
var map = L.map('map', {
   center: [57.35, -101.35],
   zoom: 4,
   layers:[
     L.tileLayer(‘<url>’),

   ]
});
```

One last thing I did with the map was change the center coordinates, which were 57.35, -88.35. I figured out a centre-ish coordinate by looking at a map of canada, and deciding that Reindeer Lake is close enough to the centre. I also decided that the longitude was good as it was, as it already showed both the North and South-most locations we were highlighting, and so just replaced -88.35 with -101.35 which was the latitude of Reindeer Lake where I happened to click it. When I went to check the site, it all looked good!
### Stylesheet changes
With the new map, I decided that I wanted to add colour to the site that would compliment it. I did this by saving a screenshot of a part of the map, and loading it into coolors.co which created a palette for me. I then chose two colours from that palette, a dark blue-ish green and a yellow-y beige as the colours I would use. I chose the dark green as my link colour, as it needed to be a dark colour in order to stand out against the background. I chose the beigh as the colour of my header and footer, as it would be a nice accent. I could have chosen a colour for the backgrounf of the text pages, but decided that because black text on a white background is the most legebile, it was fine as is. Plus, that would be adding another colour to my palette, which I believe works fine as is. 

When I began working on editing the stylesheet, I noticed that the `.html` pages in the `~/sites/` folder and `index.html` were using different stylesheets, `~/sites/CSS/style.css` and `~/CSS/style.css` respictively. Given more time, I would have changed this, but as it was, I simply made sure that the two stylesheets were identical. 

To change the header and footer colour, I repleced <hex> in the following lines of code with the hex code given to me by coolors.co. 

#### For the footer:
```
.footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  /* Set the fixed height of the footer here */
  height: 60px;
  background-color: #<hex>;
}

.footer2 {
  position: absolute;
  bottom: 0;
  width: 100%;
  /* Set the fixed height of the footer here */
  height: 60px;
  background-color: #<hex>;
}
```

#### For the header:
It should be noted that in the original code, the header was a gradient and thus kept that code. I would have changed it so that the gradient was not something happening at all, but instead just replaced all of the hex codes into the colour I wanted, causing the gradiation to not be noticeable. 
```
.navbar-default {
  background-image: -webkit-linear-gradient(top, #<hex> 0%, #<hex> 100%);
  background-image:      -o-linear-gradient(top, #<hex> 0%, #<hex> 100%);
  background-image: -webkit-gradient(linear, left top, left bottom, from(#f4efd9), to(#f4efd9));
  background-image:         linear-gradient(to bottom, #<hex> 0%, #<hex> 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffffffff', endColorstr='#ff<hex>', GradientType=0);
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  background-repeat: repeat-x;
  border-radius: 4px;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, .15), 0 1px 5px rgba(0, 0, 0, .075);
          box-shadow: inset 0 1px 0 rgba(255, 255, 255, .15), 0 1px 5px rgba(0, 0, 0, .075);
```













