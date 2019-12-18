# vectorstyles.github.io

This reposity holds style definitions for [BorgerGIS](https://github.com/frederiksberg/borgergis).

## Style Format 

Styles are represented in the JSON format.

Example style
```JSON
{
    "Motionsruter": {
        "type": "line",
        "paint": [
            {
                "name": "line-color",
                "value": "#BF360C"
            },
            {
                "name": "line-width",
                "value": 3
            }
        ],
        "layout":[
            {
                "name": "line-cap",
                "value": "round"
            }
        ],
        "symbols": {
            "minZoom":14,
            "maxZoom":22,
            "type":"point",
            "textProperty":"navn",
            "paint": [               
                {
                    "name": "icon-color", //Key name
                    "value": "black"
                }
            ],
            "layout":[
                {
                    "name": "text-field",
                    "value": "{navn}"
                }
            ]
        }
    }
}
```

The style definition contains layer names as keys, which maps to the name of the layer in Tegola.

Paint and layout properties are in the form of 
```
{
    "name": "text-field",
    "value": "{navn}"
}
```
Where name is the key from [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers)  
and value is value

### Layer properties

| Property        | Definition           | Possible Values  |
| ------------- |-------------| -----|
| type (required)     | what geometry type the layer is drawn as eg. line, circle, fill | Refer to [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers) for possible values |
| paint (required)     | Paint properties that should be applied to the layer       |   Refer to specific layer type for possible properties eg. fill [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-fill) |
| layout (required) | Layout properties that should be applied to the layer      |    Refer to specific layer type for possible properties eg. fill [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-fill) |
| symbols (optional) | Optionally adds a symbol layer on top of the layer, which can show labels       |    {Object} / None |
| attributeSortOrder (optional) | Optionally sort layer properties, so the ones listed are placed at the top       |    [array] / None |

### Symbol properties

| Property        | Definition           | Possible Values  |
| ------------- |-------------| -----|
| minZoom (required)    | Lowest zoom to show labels | [0..22] (must be smaller than maxZoom) |
| maxZoom (required)     | Highest zoom to show labels  | [0..22] (must be larger than minZoom)  |
type (required)     | label type  | [ 'point' , 'line' , 'dynamic' ]  |
| paint (required)     | Paint properties that should be applied to the layer       |   Refer to  [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-symbol) |
| layout (required) | Layout properties that should be applied to the layer      |    Refer to [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-symbol) |


#### Label type
| Value        | Definition           | 
| ------------- |-----------------|
| point    | Refer to [ symbol-placement ] in [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-symbol) |
| line     | Refer to [ symbol-placement ] in [Mapbox Style Guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/#layers-symbol)  |
| dynamic     | useful for polygon layers, where you want the label to always be visable  |


## Data driven styling 

With mapbox gl js it possible to make data driven styling, based on a variety of values such as zoom or feature properties.

The following is an example of a layer where the `fill-color` property is based upon a data driven style.  
 To get more info visit [Mapbox documentation](https://docs.mapbox.com/help/tutorials/mapbox-gl-js-expressions/)
```json
 {
    "name": "fill-color",
    "value": [
        "match",
        [
            "get",
            "antal"
        ],
        1,
        "green",
        5,
        "red",
        "white"
    ]
}
```
