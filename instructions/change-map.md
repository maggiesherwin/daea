- Created a map in Mapstack by Stamen: http://mapstack.stamen.com
- Right click on map and choose “open in new tab”
- Copy the url in the new tab.
- Copy all customizations between `.com/` and `/{random number}` and paste them into http://{s}.sm.mapstack.stamen.com/<customizations>/{z}/{x}/{y}.png
- Insert this URL into the index.html page here:
```
var map = L.map('map', {
   center: [57.35, -101.35],
   zoom: 4,
   layers:[
     L.tileLayer(‘<url>’),

   ]
});
```
