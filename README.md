# iucn-red-list-spatial-data
Converting IUCN Red List to GeoJSON

## Download IUCN data
Once you have created an account at http://www.iucnredlist.org/ you can [download data as shapefiles](http://www.iucnredlist.org/technical-documents/spatial-data).

## Converting to GeoJSON

For background see [How to convert Shapefiles to GeoJSON maps for use on GitHub (and why you should)](https://ben.balter.com/2013/06/26/how-to-convert-shapefiles-to-geojson-for-use-on-github/) and [Managing GeoJSON data using GDAL](https://savaslabs.com/2015/05/25/manage-geojson.html).

IUCN shapefiles can be big, and the resulting GeoJSON can be huge (for example, if a species distribution is based on geographic provinces, and the polygons follow those the geographical boundaries with a high degree of precision).

### Install GDAL

On a Mac download precompiled GDAL from http://www.kyngchaos.com/software:frameworks and add 
```
export PATH=/Library/Frameworks/GDAL.framework/Programs:$PATH
```
To .bash_profile

### Convert one file

Simply use ogr2ogr:

```
ogr2ogr -f GeoJson species_13418.geojson species_13418.shp
```

### Extract GeoJSON for one species from multi-species file

The GDAL utility **ogr2ogr** can be used to extract and simplify GeoJSON. For example, given the data for shrimps (FW_SHRIMP) we can extract data for *Euryrhynchus amazoniensis* like this:

```
ogr2ogr -f GeoJson Euryrhynchus_amazoniensis.geojson FW_SHRIMP.shp -sql "SELECT * FROM FW_SHRIMP WHERE binomial='Euryrhynchus amazoniensis'" -simplify 0.1
```

Note the use of **-simplify 0.1** to simplify the polygon (without this the file is huge), and the SQL to extract just the data for one species (the species in the dataset are listed din the *.dbf file).




