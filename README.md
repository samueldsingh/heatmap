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

## Creating the map using Mapbox GL JS
Now that you understand the purpose of heatmaps and the paint properties you will be working with,
it's time to set up your map. For our example, we will be using the Mapbox Dark [template style](https://docs.mapbox.com/studio-manual/reference/styles/#mapbox-template-styles). You can find the [Style URLs](https://docs.mapbox.com/help/glossary/style-url/) for each of the template styles in [Mapbox API documentation](https://docs.mapbox.com/api/maps/styles/).

In your text editor, create a new index.html file, then copy and paste the below code into it. Make sure to use an [access token](https://docs.mapbox.com/help/glossary/access-token/) that is associated with your account. Once you add this code and save your index.html file, you can preview the file in your browser to make sure you see the map.

```
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='utf-8' />
    <title>Make a heatmap with Mapbox GL JS</title>
    <meta name='viewport' content='width=device-width, initial-scale=1' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/v2.14.1/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v2.14.1/mapbox-gl.css' rel='stylesheet' />
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
    </style>
</head>
<body>
  <div id='map'></div>
  <script>
    mapboxgl.accessToken = 'pk.eyJ1Ijoic2FtdWVsZHM3IiwiYSI6ImNsZ3Z6aG5pbjA4cnAzZHBsejQ1cXFha20ifQ.gPsqiwIKL3RKWXK8DY9xlg';
    const map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/dark-v11',
      center: [-79.999732, 40.4374],
      zoom: 11
    });

   // we will add more code here in the next steps

  </script>
</body>
</html>
```

