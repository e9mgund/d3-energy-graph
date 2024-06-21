# Locational Marginal Price - ERCOT Chart Documentation

## Brief Summary :
The LMP [^1] - ERCOT [^2] graph provides a visual representation of Day ahead and Real Time Prices of energy. It is rendered in the form of a step-Line chart. It has numerous fetaures, including but not limited to , the interactive date selector , dynamic axes , crosshairs , tooltips and the toggle-able legend.

## Technologies used :
1. **Bootstrap :**
    + For Beautiful rendering of the webpage.
2. **Bootstrap icons :**
    + A light-weight icons module.
3. **D3.js :**
    + d3.js (or D3.js) is a free, open-source JavaScript library for visualizing data.
4. **Plot :**
    + Observable Plot is a free, open-source, JavaScript library for visualizing tabular data, focused on accelerating exploratory data analysis.
5. **Flatpickr :**
    + Flatpickr is a lightweight and powerful datetime picker.

## Structure :
1. Imported all the required modules via CDN in the ```<head>``` of the document.
2. **Section 1**: Headers and Date Picker input.
    - *_flatpickr_* : Handles the required css and js functionality automatically.
        -  Returns *_Date_* objects StartDate and EndDate as output. These objects will used to send an AJAX request to the backend for data selection.
3. **Section 2** : Contains ```<svg>``` tag to store the graph.```<g>``` tags for crosshair and ```<div>``` element for the tooltip.
    - Height : 800px
    - Width : 1800px
4. **Section 3** : Contains the Legend. 
    - Two toggle-able buttons : **Real Time** and **Day Ahead**
5. Inside second ```<script>``` tag imported the Plot framework which is based on D3.js via CDN.
6. This document accepts data as *.csv* file.
7. Input :
    - Initial Format : 
        - Date : Strings
        - Prices : Strings
    - Processed Format :
        - Date : Date objects (Used ```Date()``` constructor)
        - Prices : Float values
        - Empty Fields : ```NaN``` value

8. Variables :
    1. **showRTM** : Boolean to handle RTM visibility
    2. **showDAM** : Boolean to handle DAM visibility
    3. **plotContainer** : Constant object to contain graph
    4. **marks** : Constant array of strings for marks in the plot
    5. **crosshair** : Constant object to contain crosshair
    6. **tooltip** : Constant object to contain tooltip
    7. **mouseX, mouseY** : Integers to contain the mouse pointer position
    8. **d0 , d1** : Constant objects containing data records
    9. **d** : Constant array of data objects

9. Functions :
    1. ```drawplot()``` :
        + Return type : Void
        + Functionality :
            1. Removes all the elements from the graph.
            2. Checks the booleans _showRTM_ and _showDAM_.
            3. If ```true``` then adds respective marks of graph in *marks* array.
            4. Appends the plot into the *plotContainer* element.
            5. Selects the elements with ".crosshair" class for the *plotContainer* element.
            6. Selects the elements with ".tooltip" class.
            7. For *mouseover* event :
                + tooltip opacity : 0.85
                + crosshair display : null
            8. For *mouseout* event :
                + tooltip opacity : 0
                + crosshair disply : none
            9. For *mousemove* event :
                + function call to the ```mousemove()``` function.
    
    2. ```mousemove()``` :
        + Return type : Void
        + Parameters : **event** object
        + Functionality :
            1. Calculation of *mouseX* and *mouseY* mouse pointer positions.
            2. Bisection of dates based on the mouse pointer position, so that pointer can move only on plotted x-axis intervals.
            3. Calculation of *xPos* i.e position of crosshairY rule.
            4. Addition of transform attributes to the crosshairX and crosshairY rules.
            5. Addition of DAM and RTM prices into the inerHTML of tooltip element.
            6. Removal of DAM or/and RTM based on the truth values of booleans showDAM and showRTM.
            7. Adjustment in the positioning of the tooltip element based on pointer position on the screen.
    
    3. **Arrow functions for Graph toggle** :
        + Return type : Void
        + Functionality :
            1. Negates the truth values of *showRTM* and *showDAM*.
            2. Checking the truth values of *showRTM* and *showDAM* :
                + If ```true``` :
                    + class attribute of elements with *.dam* / *.rtm* id : "bi bi-toggle-on"
                    + style attribute of elements with *.toggle-dam* / *.toggle-rtm* :
                        + opacity : 1
                + If ```false``` :
                    + class attribute of elements with *.dam* / *.rtm* id : "bi bi-toggle-off"
                    + style attribute of elements with *.toggle-dam* / *.toggle-rtm* :
                        + opacity : 0.50

## References :
+ https://getbootstrap.com/docs/5.3/getting-started/introduction/
+ https://d3js.org/what-is-d3
+ https://observablehq.com/plot/what-is-plot
+ https://flatpickr.js.org/getting-started/

## Footnotes :
[^1]: LMP - Locational Marginal Price
[^2]: ERCOT - Electric Reliability Council of Texas
