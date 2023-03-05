# Data Visualization with D3

D3, or D3.js, stands for ***Data Driven Documents***. It's a JavaScript library for creating dynamic and interactive data visualizations in the browser.

D3 is built to work with common web standards – namely HTML, CSS, and Scalable Vector Graphics (SVG).

D3 supports many different kinds of input data formats. Then, using its powerful built-in methods, you can transform those data into different charts, graphs, and maps.

In the Data Visualization with D3 courses, you'll learn how to work with data to create different charts, graphs, hover elements, and other ingredients to create dynamic and attractive data visualizations.

# Import D3.js

```jsx
<script type="module">
  import * as d3 from 'https://cdn.jsdelivr.net/npm/d3@7/+esm'		
</script>
```

# ****Add Document Elements****

```jsx
<body>
</body>
<script>
import * as d3 from 'https://cdn.jsdelivr.net/npm/d3@7/+esm'

d3.select("body")
  .append("h2")
  .text("Learning D3")
</script>
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled.png)

# ****Select a Group of Elements****

```jsx
d3.select("ul")
  .selectAll("li")
  .text("list item")
```

# ****Work with Data****

The first step is to make D3 aware of the data. The `data()` method is used on a selection of DOM elements to attach the data to those elements. The data set is passed as an argument to the method.

A common workflow pattern is to create a new element in the document for each piece of data in the set. D3 has the `enter()` method for this purpose.

```html
<body>
  <h2>Existed h2</h2>
</body>
```

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body")
  .selectAll("h2")
  .data(dataset)
  .enter()
  .append("h2")
  .text("New Created h2")
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%201.png)

# ****Work with Dynamic Data****

The D3 `text()` method can take a string or a callback function as an argument:

```html
<body>
</body>
```

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body")
	.selectAll("h2")
  .data(dataset)
  .enter()
  .append("h2")
  .text(d => `${d} USD`);
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%202.png)

# ****Add Inline Styling to Elements****

```html
<body>
</body>
```

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body")
	.selectAll("h2")
  .data(dataset)
  .enter()
  .append("h2")
  .text(d => `${d} USD`)
	.style("color","red")
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%203.png)

# ****Change Styles Based on Data****

```html
<body>
</body>
```

You can use a callback function in the `style()` method and include the conditional logic. The callback function uses the `d` parameter to represent the data point:

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body")
	.selectAll("h2")
  .data(dataset)
  .enter()
  .append("h2")
  .text(d => `${d} USD`)
	.style("color", d => d<20?"red":"green")
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%204.png)

# ****Add Attributes with D3****

```jsx
<style>
  .bar {
    width: 25px;
    height: 100px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
</body>
```

D3 has the `attr()` method to add any HTML attribute to an element, including a class name.

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body")
	.selectAll("div")
	.data(dataset)
	.enter()
	.append("div")
	.attr("class","bar")
```

# ****Update the Height of an Element Dynamically****

In this section, We can combine the previous sections to create ***a simple bar chart***. There are two steps to this:

1. Create a `div` for each data point in the array
2. Give each `div` a dynamic height, using a callback function in the `style()` method that sets height equal to the data value

```html
<style>
  .bar {
    width: 25px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
</body>
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%205.png)

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body").selectAll("div")
  .data(dataset)
  .enter()
  .append("div")
  .attr("class", "bar")
  .style("height", d => `${d*4}px`)
```

# ****Change the Presentation of a Bar Chart****

```html
<style>
  .bar {
    width: 25px;
		// add margin
	  margin:2px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
</body>
```

![Untitled](Data%20Visualization%20with%20D3%20ff1b571ffbfa40b7bb140fa5a84beccb/Untitled%206.png)

```jsx
const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
d3.select("body").selectAll("div")
  .data(dataset)
  .enter()
  .append("div")
  .attr("class", "bar")
	// scale the height
  .style("height", d => `${d*10}px`)
```

# ****Learn About SVG in D3****

*SVG* stands for *Scalable Vector Graphics*.

Here "scalable" means that, if you zoom in or out on an object, it would not appear pixelated. It scales with the display system, whether it's on a small mobile screen or a large TV monitor.2

SVG is used to make common geometric shapes.

# ****Dynamically Set the Coordinates for Each Bar****

The last challenge created and appended a rectangle to the `svg` element for each point in `dataset` to represent a bar. Unfortunately, they were all stacked on top of each other.

# ****Invert SVG Elements****

In SVG, the origin point for the coordinates is in the upper-left corner. An `x`
 coordinate of 0 places a shape on the left edge of the SVG area. A `y`
 coordinate of 0 places a shape on the top edge of the SVG area. Higher `x`
 values push the rectangle to the right. Higher `y`
 values push the rectangle down.

To make the bars right-side-up, you need to change the way the `y` coordinate is calculated. It needs to account for both the height of the bar and the total height of the SVG area.

# ****Add Labels to D3 Elements****