# UFOs
UT bootcamp Module 11:  Javascript / HTML / bootstrap

## Overview

Purpose of this module challenge was to use a combination of HTML, bootstrap, and javascript to:
1.  Build & format a webpage using bootstrap & css
2.  Understand significance of directory structure to organize files being referenced
3.  Use javascript to perform the following:
    - Build & populate a data table
    - Create an interactive search for user to filter data in the displayed table
    - Use of If statement to populate filter elements
    - Use of loop to go through all filter elements & check if they apply to the table
    - Update the table based on filters applied

## Results

In order to perform search, following pseudo steps are necessary:

1.  We need to collect inputs from user on what they want to filter.  This is achieved through use of D3 SelectAll upon a change event.  We use this event to call a function to update our filters.

**D3 Select used to call Update Filters function when Input changes**
``` javascript
 d3.selectAll("input").on("change", updateFilters);
 ``` 
2.  Using an empty "dictionary" called Filters, we collect the values input by user to filter and they are organized according to the id for input box they are applied:  date, city, state, shape.

**Function to Update Filters**
``` javascript
    let changedElement = d3.select(this);
    let elementValue = changedElement.property("value");
    console.log(elementValue);
    let filterId = changedElement.attr("id");
    console.log(filterId);
    if (elementValue) {
        filters[filterId] = elementValue;
    }
    else {
        delete filters[filterId];
    }

    filterTable(updateFilters);
```

3.  Using the now populated Filters dictionary, we need to update our table to only show rows with matching data.  For reference, these resources were used:
   [Object.entries reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)
   [forEach loop reference](https://masteringjs.io/tutorials/fundamentals/foreach-object)

**Function to Update Table Based on Filters**
``` javascript
   let filteredData = tableData;
   Object.entries(filters).forEach(([filterId,value]) => {
      filteredData = filteredData.filter(row => row[filterId] === value)
      console.log(filters)
    });
    buildTable(filteredData);
  }
```
Example highlighting 2 filters applied.
![example](/example.png)

## Summary

One drawback of this web page is the cases where no data is found.  Empty table is returned, but to be more user friendly there should be some confirmatin message to the user that the filter conditions they have applied do not exist in the data set.  Furthermore, the data set is static and limited to a brief period of 2010.  To make more useful, I would recommend the following changes:
- Collect user input to update the data set with new UFO sightings to expand the data set or connect site via API to a UFO database.
- Further refine the filter to return message if no data found.
- Make the input boxes reactive so they update table as inputs are entered not requiring a full entry and <enter> key to be pressed.
- Allow partial or case insensitive search
