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

**D3 Select used to call Update Filters function when Input changes**
``` javascript
 d3.selectAll("input").on("change", updateFilters);
 ``` 

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

## Summary
