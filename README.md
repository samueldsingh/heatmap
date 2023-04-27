# Heatmap

Heatmaps can be used to display large amounts of points in a way that is visually engaging 
and encourages your audience to explore your map. To create this heatmap you need a mapbox
account and an access token. We'll be using the GeoJSON file of street trees in the city of 
Pittsburgh from the [Western Pennsylvania Regional Data Center](http://www.wprdc.org/) file of street trees in 
the city of Pittsburgh from the Western Pennsylvania Regional Data Center.

We are more interested in showing the density of points over an area. This type of heatmap does not visualize 
density by aggregating features within a set of boundaries in the way a choropleth map does, 
but instead displays a continuous gradient between points.

Heatmaps aren't only useful for visualizing point density. They can also help visualize relative 
differences between those points. You can assign each point a higher or lower importance based 
on the value of a particular property within the dataset. In our heat,we will weight your map 
by the DBH property in your data. DBH stands for "diameter at breast height" and is a standard 
way of measuring a tree's diameter at 4.5 feet above the ground. In general, it is safe to assume 
that a tree with a higher DBH is older and larger. When you give these larger trees a higher weight 
compared to smaller saplings, your visualization can be an effective approximation of the area 
that is shaded by trees' leaves.

# Heatmap paint properties
To add a heatmap layer to our map, you will need to configure a few properties. Understanding 
what these properties mean is key to creating a heatmap that accurately represents your data 
and strikes the right balance between too much detail and being a single, generalized blob.

- heatmap-weight: Measures how much each individual point contributes to the appearance 
of your heatmap. Heatmap layers have a weight of one by default, which means that all points 
are weighted equally. Increasing the heatmap-weight property to five has the same effect as placing 
five points in the same location. You can use a stop function to set the weight of your points 
based on a specified property.
- heatmap-intensity: A multiplier on top of heatmap-weight that is primarily used as a convenient 
way to adjust the appearance of the heatmap based on zoom level.
- heatmap-color: Defines the heatmap's color gradient, from miniumum value to maximum value. 
The color displayed is dependent on the heatmap-density value of each pixel (ranging from 0.0 to 1.0). 
The value of this property is an expression that uses heatmap-density as the input. For inspiration on color choices for your heatmap, take a look at Color Brewer.
- heatmap-radius: Sets the radius for each point in pixels. The bigger the radius, the smoother the heatmap and the less amount of detail.
- heatmap-opacity: Controls the global opacity of the heatmap layer.
