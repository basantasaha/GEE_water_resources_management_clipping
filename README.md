# GEE_water_resources_management_clipping


var selected = admin2.filter(ee.Filter.eq('ADM2_NAME', 'Bankura'));

var geometry = selected.geometry()
 
 var rgbVis = {
   min:0.0,
   max: 3000,
   bands:['B4', 'B3', 'B2'],
 };
 var filtered = s2.filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 30))
 .filter(ee.Filter.date('2019-01-01','2020-01-01'))
.filter(ee.Filter.bounds(geometry))

var image = filtered.median();
var clipped = image.clip(geometry);
//ctrl + space for autocomplete
Map.centerObject(geometry);
Map.addLayer(clipped, rgbVis, 'composite');
Map.addLayer(geometry,{color: 'red'}, 'selected admin2');
