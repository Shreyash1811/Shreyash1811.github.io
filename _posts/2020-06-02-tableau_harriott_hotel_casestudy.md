---
title: "Harriott Hotel Group case study : Annual Analytics on Tableau and Alteryx"
date: 2020-06-02
categories: [Tableau]
tags: [Data Analysis]
header:
  image: "/images/harriott_group/header.jpg"
excerpt: ""
mathjax: "true"
---
# Harriott Hotel Group (HHG)

## *Comfortably Classy*

A hotel chain with a national footprint that has several brands
& serves customers in all types of demographics areas.
Harriott would like to understand the general state of their
business along with how amenities impact their top line
revenue.

# Data Collection and Preliminary Analysis
## *Merge and explore the revenue, hotel, amenity, and customer files. Do preliminary EDA to understand current state business.*
## The process I followed:
- Used Alteryx to merge and transform the text data before importing it to tableau
- Build a simple report based on the output file (Tableau or PBI)

<img src="\images\harriott_group\alteryx_flow.PNG" alt="drawing" height="1600" width="1600"/>

## Areas to analyze:
- Revenue per hotel YoY
- Occupancy rate per hotel – Is there seasonality?
- Room night pricing. What's the average and range?
- Are there different types of customers that stay at each hotel? Is there clusters of customers that have the same behavior?
- How does Business vs Leisure effect pricing?


<html>
    <head>
        <title> Harriott Hotel Group : Annual Analytics on Tableau and Alteryx </title>
    </head>
    <body>
        <h5>This the Status Dashboard: </h5>
        <div class='tableauPlaceholder' id='viz1591128049764' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_Harriott&#47;Dashboard&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Shreyaskumar_Kathiriya_Harriott&#47;Dashboard' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_Harriott&#47;Dashboard&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1591128049764');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1200px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1200px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='2027px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

    </body>
</html>
