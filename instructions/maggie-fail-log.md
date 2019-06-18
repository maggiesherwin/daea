# Capstone Project fail notes
### Fixing the footers
I noticed that the footers on the original site were linked to an image that no longer existed. I wanted to fix this, but in a way where it would not happen again. I searched online for a good quality `.jpg` file of the Carleton University crest, and saved a copy of it in `~/images/`. I then put the URL (found by opening the image in GitHub and right clicking `open in new tab`) to that into this code, which I then put on the bottom of every page.
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
### Deleting extraneous pages
I noticed that there were still many pages from older projects left in this repository, which I decided to delete because they were taking up space and had the chance of confusing anyone that would look into the repository. I made sure that I was only deleting files that were unrelated to Canada's atomic history by opening the HTML file and reading it. 
### Changing URLs to my GitHub account
I also noticed that when I forked this repo, the URLs still linked to the older site, which I was not working on. I could have fixed this more easily by using regex in order to find and replace the previous creator's username with my own, but due to impatience and not wanting to deal with having to download the files and then re-upload them, I instead manually replaced them all. 
### Fixing a code error
The original site had an error in its code, having `html lang=“en”>` at the beginning of each page, which I noticed that I was able to see for a split second when refreshing the pages. I realized that this was because the code was not complete and simply added a `<` to the beginning of each HTML page so that they said `<html lang=“en”>`. This completely resolved my issue. 
### Changing the map
While the original black and white map was useable, I decided that I didn't really like it, mainly because it was SO plain. When making data visualization, it is important to balance aesthetic with data, and for them to compliment each other.

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
Doing this changed the map on the site from black and white to a nice watercolour, but it lacked borders and place names. By looking around Stamen more, I found their service MapStack, which allows users to create a map using their options. With this, I decided that I liked the watercolour, and so kept that as a layer. I did change the original watercolour (which was beige/brown and blue for land and water) by altering the colour, choosing a shade of green that was both calming, but also reminiscent of toxic waste. I chose this colour because it is pleasant to look at, but also conveys information about what the site is conveying: atomic experiments and nuclear activity creates toxic waste that affects everything from the land to water. I also added a layer from the toner map, which contained borders and place names. With this new map, there is no obvious way to get a URL that would work as a map, but I figured it out!

To do this, I right clicked on the map, and chose “open in new tab”. The customizations here exist between `.com/` and `/{random number}`. I then copy and pasted them into this URL template `http://{s}.sm.mapstack.stamen.com/<customizations>/{z}/{x}/{y}.png`, and then inserted this URL into the index.html page here:
```
var map = L.map('map', {
   center: [57.35, -101.35],
   zoom: 4,
   layers:[
     L.tileLayer(‘<url>’),

   ]
});
```

One last thing I did with the map was to change the center coordinates, which were 57.35, -88.35. I figured out a centre-ish coordinate by looking at a map of Canada, and deciding that Reindeer Lake is close enough to the centre. I also decided that the longitude was good as it was, as it already showed both the North and South-most locations we were highlighting, and so just replaced -88.35 with -101.35 which was the latitude of Reindeer Lake where I happened to click it. When I went to check the site, it all looked good!
### Stylesheet changes
With the new map, I decided that I wanted to add colour to the site that would compliment it. I did this by saving a screenshot of a part of the map, and loading it into coolors.co which created a palette for me. I then chose two colours from that palette, a dark blue-ish green and a yellow-y beige as the colours I would use. I chose the dark green as my link colour, as it needed to be a dark colour in order to stand out against the background. I chose the beige as the colour of my header and footer, as it would be a nice accent. I could have chosen a colour for the background of the text pages but decided that because black text on a white background is the most legible, it was fine as is. Plus, that would be adding another colour to my palette, which I believe works fine as is. 

When I began working on editing the stylesheet, I noticed that the `.html` pages in the `~/sites/` folder and `index.html` were using different stylesheets, `~/sites/CSS/style.css` and `~/CSS/style.css` respectively. Given more time, I would have changed this, but as it was, I simply made sure that the two stylesheets were identical. 

To change the colours, I replaced <hex> in the following lines of code with the hex code given to me by coolors.co. 

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
#### For the links
With the links, I decided to have them all be the same colour, regardless of hovering or use. I did this mainly because it meant I did not need to choose a third colour. 
```
a { color: #<hex> !important; /* color of links */ }
a:hover { color: #<hex> !important; /* color of links when hover mouse over */ }
a:active { color: #<hex> !important; /* color of links when active */ }
a:visited { color: #<hex> !important; /* color of links after user has visited it */ }
```
### Fixing the tooltips
I also decided to do a little sprucing up of the tooltips so that they did not have any arbitrary capitalization. I did this by opening `~/sites/aa-sites-popup.csv` and editing the text there.
### Editing Délįne
Because of the emotional impact of the Délįne page, I decided that it would be a good idea to add a documentary in order to increase the connection between reader and subject. I added the video using youtube's embed feature, which I then placed into the page's code. I then moved the video around, refreshing the site at the same time in order to see what I was doing. I continued rearranging it and the other images on the page so that they worked better with the text wrapping it in an effort to avoid hanging lines. I also found mentions of other sites we have pages of and added a link to their respective pages. I then made the headers of the paragraphs smaller so that not all of the headers were the same. I also used CSS style padding to make sure the images looked correct and did not have text right against them. I also tested all of the links in the references section to make sure they were all still live and found alternatives for broken ones. Finally, I tackled the content of the page, editing it so that it made more sense and was less repetitive, and added a "lasting impact" section to address continuing issues at the site. I also changed the spelling of Deline to Délįne because names have meaning, and the people there deserve to have their name spelled correctly.
### Editing Port Radium
I found this page to be much easier, especially after the previous one. Once again, I rearranged the images and changed the padding so that they worked better with the text. I added a "lasting impact" section here as well and again tested the links. I also added a new image that complimented the "lasting impact" section and showed Port Radium as it exists today. I found this necessary here (unlike Délįne) because Port Radium's changes were much more apparent and impactful. I added the image much like I added the Carleton Crest image, but instead put it into this code `<img src="<url>" style="float:left; padding-right:35px">`, and changed the style specifications to arrange the image where I wanted it to be.
