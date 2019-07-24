# User Manual : LAPD Historic Crime Map
##### Created by Bryan Borenstein, Private Cloud Admin, LLC
##### Email: [bryan@privatecloudadmin.com](mailto:info@example.com)


## Purpose: 

This pupose of this app is to visualize all historic criminal record data provided by Los Angeles County via [Catalog.Data.gov](https://catalog.data.gov/dataset/crime-data-from-2010-to-present-c7a76), using a map to visualize location data, as well as a histogram to show crime occurences per hour for any chosen day between 01-JAN-2010 and 16-JUL-2019. 

## Background 

This application was written in Python version 3.7.3, in conjunction with [Plotly's](https://plot.ly) open-source library, [Dash](https://dash.plot.ly/introduction). The cleaned dataset used for input was loaded, cleaned, formatted, and subsequently exported into .csv format using Oracle's 12c Database in conjunction with SQL Developer. 

## Structure

In conjunction with Python, Plotly's Dash library can be broken down into two categories:

#### 1. Layout:

The visual structure of the app was primarily created using Plotly's `dash_html_components` library, which includes component classes for all HTML tags - including keyword arguments. This allows for smooth integration within Python; rendering out traditional HTML without the necessity of writing the page in traditional HTML. 

For more information regarding `dash_html_components`, please reference the library's [User Documentation](https://dash.plot.ly/dash-html-components).


#### 2. Interactivity:

The interactivity of the app was created using Plotly's Python library [`dash-core-components`](https://dash.plot.ly/getting-started); which is a feature rich library that includes all the classes required to create the interactive components of the application: these include higher level component libraries such as Plotly's [plotly.js](https://plot.ly/javascript/), HTML, CSS, and [React.js](https://reactjs.org/). 

For more information on the specific classes included, please see the `dash-core-components` [User-Documentation](https://dash.plot.ly/dash-core-components).

### Understanding @Callbacks

There are a variety of update methods provided within the web app for updating data in real-time, called `@Callbacks`. The image below visualizes the structure of the callbacks, which can be defined as the process steps that update the application, based on user-interation. 

![alt text](https://files.catbox.moe/8rfko9.png "Web-App Callbacks Visualized")

## Dataset

The dataset (.csv file which is converted to a Python DataFrame) contains 3 attributes, or columns, which are `Date/Time`, `Lat`, and `Long`

#### 1) `Date/Time`: 

This column represents the date and time of a specific crime occurring, and is formatted as such: `YYYY-MM-DD HH:MI:SS` and is used to query the records by date, and time, by using the calendar input within the application, as well as the time - which can be further updated utilizing the last multi-selection drop down, `Select Time(s)`.

#### 2) `Lat`:

This column represents the latitude, which is at most a 6 digit coordinate. 

#### 2) `Long`:

This column represents the longitude, which is at most a 6 digit coordinate. 

### Mapping Data To The Web App

The points on the map, which represent either a specific police report ID, or crime occurrence, or 1 of 21 LAPD Community Stations, known as 'Districts', are created by joining the `Lat` and `Long` columns to create a 10 to 12 digit geographic grid coordinate; allowing for highly accurate location data representing a geolocation of a crime taking place, based on the `@Callback` date selected in the `Date/Time` attribute of the record/row. 

### Optimization

By selectively exporting the .csv files with only the features, or attributes required, the web app can efficiently query this large dataset, with nearly 2 million rows, in an extremely efficient manner.
The application itself begins by importing the .csv files from a [GitHub Repository](https://github.com/bborens/datasets) as Python DataFrames, and then joining them to make a single sorted DataFrame, which is then used by the application to query all historic data. 

## More Information

For a complete view of all application files, please visit the web application's [GitHub Repository](https://github.com/bborens/WebApp).   
