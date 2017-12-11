JQuery Heatmap Plugin
=====================

Easy heatmap-style background-coloring for HTML elements.

**Note:** this is entirely the great work of David Larsen: https://github.com/DLarsen/jquery-hottie
 I only renamed it to sound a bit less.. naughty (sorry, David) and added a few minor features that I needed for my own use cases.

In its most simple form, this plugin parses the html contents of the selected elements and parses them as floats.

Given the following markup:

    <ul id="example1">
      <li>1<li>
      <li>2<li>
      <li>3<li>
      <li>4<li>
      <li>5<li>
    </ul>

    $('ul#example1 li').heatmapper();

Frequently, the numeric values used for coloring will not be found in the 
contents of the selected elements.  You can pass a function as an option 
which tells the plug-in how to retrieve the numeric value.


    <ul id="example2">
      <li data-hist="4">Alabama</li>
      <li data-hist="3">Alaska</li>
      <li data-hist="7">Arizona</li>
      <li data-hist="1">Arkansas</li>
      <li data-hist="9">California</li>
      <li data-hist="5">Colorado</li>
    </ul>

    $('ul#example2 li').heatmapper(
    {
    readValue : function(e) {
      return $(e).attr("data-hist");
    }
    });

You can also pass in a color scheme as an array. Low order colors correspond to low values.  
High order values correspond to high values.

    <table id="mytable">
        <tr><td>2.59</td><td>0.68</td><td>1.35</td><td>1.35</td><td>2.03</td><td>1.60</td></tr>
        <tr><td>1.39</td><td>0.70</td><td>-1.22</td><td>1.08</td><td>-1.00</td><td>-2.12</td></tr>
        <tr><td>2.87</td><td>0.59</td><td>1.22</td><td>-0.57</td><td>1.08</td><td>3.00</td></tr>
        <tr><td>0.99</td><td>0.25</td><td>0.48</td><td>0.50</td><td>0.99</td><td>-1.77</td></tr>
    </table>

    $("#mytable td").heatmapper({
        colorArray : [ 
            "#63BE7B",
            "#FBE983",
            "#F8696B"
        ]
    });


If you want to split ( "center" ) multi-color gradients around a specific value, the **centerVal** option can be used.
This option is specifically designed for bicolor heat maps when the values are often asymmetrically distributed
around a neutral value. For example if we have negative and positive values and we want the negative
values to be shaded in red and positive values shaded in green, this can be accomplished by using 
3 colors in colorArray, with the "neutral" color in the middle (usually a light gray color).

    $("#mytable td").heatmapper({
      centerVal : 0,
      colorArray : [
       "#FF4040",
       "#FBFBFB", //centerVal anchored color
       "#40FF40"
      ]
    });

**Note:** in order to show a bi-color heatmap for **ratio** values centered around 1, 
with values >= 1 tinted with one color (e.g. green) and those <=1 shaded with
a different color (e.g. red), the '''settings.preMin'' value should also be set to 1
in order to obtain the maximum tinting for the actual minimum value in the data:
or presenting ratio values ```centerVal``` would be set to 1.

  $("#mytable td").heatmapper({
    preMin : 1,
    centerVal : 1,
    colorArray : [
     "#FF6060",
     "#FBFBFB",
     "#40FF40"
    ]
  });

See ''example.html'' for an example of a bicolor heat map for 
odd-ratio values.
