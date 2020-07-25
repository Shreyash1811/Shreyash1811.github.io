---
title: "Tableau Dashboards"
permalink: /tableau/
date: 2020-02-10
header:
  image: "/images/banners/tableau_header.png"
---
|No.| Information  |
|---|---|
|1.| [Practice Charts](#pract)  |
|1.1| [Sunburst Chart](#char1) |
|2.|  [Case Study ](#case) |
|2.1| [Harriott Hotel Group](#case1) |
|2.2| [Office Destination Sales](#case2) |
|2.3| [Employment Now](#case3) |
|2.3| [Employment Now extended Analysis](#case4) |

# Practice Charts
<a id = "pract"></a>

## Sunburst Chart 1:
<a id = "char1"></a>
<html>
    <head>
        <title> Sunburst Sales Chart </title>
    </head>
    <body>
<div class='tableauPlaceholder' id='viz1595691198039' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Su&#47;SunburstSalesDashboard_15956909077580&#47;SunburstDashboard&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='SunburstSalesDashboard_15956909077580&#47;SunburstDashboard' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Su&#47;SunburstSalesDashboard_15956909077580&#47;SunburstDashboard&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1595691198039');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='800px';vizElement.style.height='827px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
</body>
</html>
<a id = "char1"></a>

# Case Study 1:
<a id = "case"></a>
# Harriott Hotel Group (HHG)

## *Comfortably Classy*

A hotel chain with a national footprint that has several brands
& serves customers in all types of demographics areas.
Harriott would like to understand the general state of their
business along with how amenities impact their top line
revenue.
<a id = "case1"></a>
# Data Collection and Preliminary Analysis
## *Merge and explore the revenue, hotel, amenity, and customer files. Do preliminary EDA to understand current state business.*
## The process I followed:
- Used Alteryx to merge and transform the text data before importing it to tableau

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
        <h5>STATUS DASHBOARD: </h5>
        <div class='tableauPlaceholder' id='viz1591128049764' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_Harriott&#47;Dashboard&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Shreyaskumar_Kathiriya_Harriott&#47;Dashboard' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_Harriott&#47;Dashboard&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1591128049764');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1200px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1200px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='2027px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

    </body>
</html>

# Case Study 2:
<a id = "case2"></a>
# Office Destination Sales Dashboard:
### Insights based on the Data analysis:
- The Sub categories we are losing the most money:
  - Binders
  - Machines
  - Tables
- Company is losing money in Central Region.

### Outliers in the Data:
- We see some inconsistency with consumer segment sales and profit.

*Even with high sales the revenue in this segment is growing negative.
Chances are this is due to change in making cost of the consumer segment attracted products. There are several reasons to boost in making cost for the manufacturing from government policies to natural disasters to as straight forward as scarcity of the raw materials*

<html>
    <head>
        <title> Office Destination Sales Dashboard</title>
    </head>
    <body>
        <h5>STATUS DASHBOARD:</h5>
        <div class='tableauPlaceholder' id='viz1591228107917' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Da&#47;DataVisualisationOfficeDestinationDashboard&#47;OfficeDestination&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='DataVisualisationOfficeDestinationDashboard&#47;OfficeDestination' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Da&#47;DataVisualisationOfficeDestinationDashboard&#47;OfficeDestination&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1591228107917');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='1727px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

    </body>
</html>


# Case Study 3:

# Employment Now:
<a id = "case3"></a>
### Background:
Employment Now! Is a Back to Work program contracted by the Human Resource Administration (HRA) of NY to assist
candidates enrolled in Public Assistance in finding and retaining employment. Their services include resume writing,
interview training, and free interview attire. Once prepared, participants will work closely with case workers who have
relationships with employers throughout NYC and refer them to various interviews.


<html>
    <head>
        <title> Office Destination Sales Dashboard</title>
    </head>
    <body>
        <h5>STATUS DASHBOARD:</h5>
        <div class='tableauPlaceholder' id='viz1591277315042' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;BB&#47;BB292YF9D&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='path' value='shared&#47;BB292YF9D' /> <param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;BB&#47;BB292YF9D&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1591277315042');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='1677px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

    </body>
</html>

## Further extended Analysis on Wages Distribution:

<a id = "case4"></a>
<html>
    <head>
        <title> Office Destination Sales Dashboard</title>
    </head>
    <body>
        <h5>STATUS DASHBOARD:</h5>
        <div class='tableauPlaceholder' id='viz1591277467466' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_EmploymentNow&#47;WagesDashboard&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Shreyaskumar_Kathiriya_EmploymentNow&#47;WagesDashboard' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sh&#47;Shreyaskumar_Kathiriya_EmploymentNow&#47;WagesDashboard&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1591277467466');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='1177px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

    </body>
</html>
