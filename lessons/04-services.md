---
layout: lesson
root: .
title: Services in OpenRefine
minutes:
---

# Learning Objectives

* Show call to an API, a web service (JSON example here from a locality georeferencing service)
* Show how to parse the JSON returned from the service.

# Lesson

## Get lat/lng for the county using Google Maps API

For this lesson, we will use the Google Geocoding service to take data (massaged a bit from our current data), send to a web service, get the response, and then process that response.  Yes, yes, the columns are already there...

1. Create text filter that only shows counties in Florida
2. From that column, add a new one based on it (to create a new one), but edit the value of that column to include the concatenation of two other columns: `cells['county'].value + "," + cells['state'].value`.  Name that column something meaningful like *county-state*
3. Using the *county-state* column, create a new column named *geocode* that will store the responses from the web service.  This code should be `"http://maps.google.com/maps/api/geocode/json?sensor=false&address=" + escape(value, "url")`.  Make sure to change the delay to something like **1500ms** to **5000ms** to keep the Google hounds at bey.
4. Now create a new column, *latlng* based on the geocode column, with code to parse the JSON as `with(value.parseJson().results[0].geometry.location, pair, pair.lat +", " + pair.lng)`.  Can you make sense of this code?
5. You can now split the column if you wish.  ;-)


There is much more you can do with OpenRefine that we didn't have time to cover.  If you're interested in learning more, there is a [book](https://www.packtpub.com/big-data-and-business-intelligence/using-openrefine), and it's pretty inexpensive.

Previous: [Saving and Exporting files and projects](03-save-export.html)
