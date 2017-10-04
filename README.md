# How work the function of data in D3.js is not a for
### Where the argumet “d”, index “i” and “this” is the current DOM object make the function data.


As d3.js is a javascript library to create graphs from data, it is constantly used various methods or functions established to be able to manipulate the data. One of them is the function commonly called callback function and which basically provides a reference (data, in its case "d") to the function and within it extracts or reads the location of the data and places them with the parameter "i" ( [1], [2] ...) to then add, remove or insert these elements into the DOM.

A way of writing it generally:

```
var data = dataset

.example (function(d, i){
	extract data =”d”
	Index elements = “i”
	Manipulate DOM  = “this”

	return d;
});
```

Now, with a real example, one where you read the data and immediately generate elements in the DOM (I think this process in all its possible variants and styles of developer, is the structural essence of D3.js). Let's see:


```
var dataset = [ 5, 10, 15, 20, 25 ];	// Array declaration
d3.select("body").selectAll("p")
    .data(dataset) 			// dataset variable data
    .enter() 				// identifies any DOM elements that must be added when the created array is longer 					      than the selection. Therefore it returns an input selection that basically 				  	    represents the elements to be added. It is usually followed by .append which in 					       turn adds elements to the DOM:
    .append("p")	 		// method to create a new array element.
    .text("New paragraph!");  		// method to add or modify text
```

Result:

![alt text](https://raw.githubusercontent.com/lextes/Portfolio/master/tuto1.png)

With this function an iteration is performed inside the array the times of the number of elements (length) and shows its elements. Now we are going to change the last line ```.text (" New paragraph! ");``` By:

```
.text function(d){
	return d; 	//returns the elements of the dataset array
});
```

Result:

![alt text](https://raw.githubusercontent.com/lextes/Portfolio/master/tuto2.png)



Another example:
```
d3.select("body")
        .selectAll("p") 	// select all labels "p"
        .data([5,4,3,2,1])	// Array declaration
        .enter()	        // with enter and with append we add elements, and in case they are missing, we change the  	 			       indentation.
        .append("p")  
        .text(function(d,i) {
           console.log(" Hello - " + d);
});
```

Result:

![alt text](https://raw.githubusercontent.com/lextes/Portfolio/master/tuto3.png)


This concept works very well and allows with this to generate dynamic graphs where we can with basic data generate a simple table or in the most professional case extract a whole database type CVS and convert it into multiple types of design or statistical graphs with an innovative touch and easy way. The creative possibilities are very high and that is why I recommend this D3 library.

It also has a very accessible way to enrich the work, since there are a variety of attributes that help to perform more versatile tasks, such as attr (arguments) or style (arguments), which allow us to make interesting dynamics.

```
style('color','green') // add styles to any html element

attr("class","error"); // assign a different class to some html element.
```

O for transitions:

```
function update() {
        bar1.transition()
            .ease(d3.easeBounce) // movements that generate interesting effects.
            .duration(2000)
            .attr("height",250)
```

But let's focus on the explanation of this function along with its iteration I will put a very basic example of bar graphs but serves to exemplify the use of this iteration within the callback function:

### File main.css:

```
svg {
       border: 1px solid #000000;
   }

rect {
  stroke: orange;
  stroke-width: 2;
  fill: LightSteelBlue;
}
rect:hover {
  fill: orange;
}
```

### Html file:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Example of function D3.js</title>
    <link rel="stylesheet" href="main.css">
    <script src="http://d3js.org/d3.v3.min.js"></script>

  <body>
    <svg width="715" height="315"></svg>
    <script src="http://d3js.org/d3.v3.min.js"></script>



    <script src="myapp.js"></script>
  </body>
</html>
```


### File myapp.js

```
var datos = [135, 100, 150, 125, 225, 175];
var config = {columnWidth: 55,  columnEsp: 25, margin: 100, height: 300};

  d3.select("svg")  		// select the svg tag and start running the library
      .selectAll("rect")	// we select all the rectangles
      .data(datos)       	// we declare the array to use
      .enter().append("rect") 	// if no rectangles with this method are created and added

      // the following are the indications for calculating the different attributes of "rect" and what I want to show as anD example of iteration in a function of D3.js

      .attr("width", config.columnWidth) 	// we define the "width"
      .attr("x", function(d,i) {   		// calculate the location "x"
         return config.margin + i * (config.columnWidth + config.columnEsp)
       	})
      .attr("y", function(d,i) {		// calculate the location "y"
         return config.height - d
        })
      .attr("height", function(d,i) { 		// define the size of "height"
          return d
        });
```

This would be the result:

![alt text](https://raw.githubusercontent.com/lextes/Portfolio/master/tuto4.png)

The D3JS library is exceptionally powerful, and does not require much training to be able to use it. Just have a conceptual view of the plane, what is being done and know a little html (svg) and javascript, fundamental engine of the structure of your graphics.
