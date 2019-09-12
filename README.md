## mapbuilder-vega Introduction

This is a repository for hosting the configurations for the Vega Widgets which are used in the GFW MapBuilder application. For more information on MapBuilder please reference the MapBuilder repository: https://github.com/wri/gfw-mapbuilder

The Vega widgets are stored in the [Resource Watch API](https://resource-watch.github.io/doc-api/index-rw.html), and can be updated through requests via Postman or another API client. Post requests can also be made through the widget editor in the forest-atlas CMS. In order to make post requests you first obtain a bearer token for the API from the WRI API team.  

- The endpoint for posting (POST Request) new widgets is *https://api.resourcewatch.org/v1/dataset/<dataset_id>/widget*
- The endpoint for updating (PATCH Request) an existing widget is *https://api.resourcewatch.org/v1/dataset/<dataset_id>/widget/<widget_id>*

Please note that in order to post a widget you must first create a dataset. For the MapBuilder, the dataset you use does not matter since MapBuilder only uses the widget and not the dataset. However, it is best practice to make sure your datasets are orgonized and related widgets are under the same datasets. For example, if you were to create several custom widgets for a single MapBuilder instance you might want to put them all under the same dataset.

All MapBuilder widgets stored in the API should include the following in thier requests:

1. **Name**: The Name of the widget
2. **Description**: A brief description of the widget
3. **Application**: The name of the application which will use the widget (please specify forest-atlas)
4. **The widget configuration**: The VEGA configuration for the widget. **Note:** Parameters which are passed from MapBuilder to the vega widget should not be included in the configuration

## Sample Requests

The following is an example of a POST request for a MapBuilder widget:

```
curl -X POST https://api.resourcewatch.org/v1/dataset/a97036a8-5526-4b85-8ffb-9ee2cdd9b34a/widget \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "widget": {
      "application":[
         "forest-atlas"
      ],
      "name":"Annual Tree Cover Loss",
      "description": "This widget is used in mapbuilder to presents results on annual tree cover loss. The widgets requires that a geostore ID, a tree cover threshold, and date range be appended to the Analysis url.",
      "widgetConfig": {}
   }
}'
```
The following is an example of a PATCH request for a MapBuilder widget. Managers and Users of the API can only update the content that they create.

```
curl -X PATCH https://api.resourcewatch.org/v1/dataset/a97036a8-5526-4b85-8ffb-9ee2cdd9b34a/widget/95c2c559-ca78-4b7a-b18b-7b2bca14ce83 \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
   "widget": {
      "application":[
         "forest-atlas"
      ],
      "name":"Annual Tree Cover Loss",
      "description": "This widget is used in mapbuilder to presents results on annual tree cover loss. The widgets requires that a geostore ID, a tree cover threshold, and date range be appended to the Analysis url.",
      "widgetConfig": {}
   }
}'
```

For more information on interacting with the Resource Watch API please reference: https://resource-watch.github.io/doc-api/index-rw.html#create-a-widget

## Global MapBuilder Widgets

The tables below list the global MapBuilder widgets which are included in the Global folder of this repository. The table includes:

1) Widget name in this repository
2) A description of what the analysis is used for
3) The datasetID in API
4) The WidgetID in API
5) A link to the widget in the API
6) The analysis url used in the Vega
7) A list of parameters which must be passed from MapBuilder to the VEGA.
8) A working call to the analysis endpoint in the Resource Watch API, in which the necessary parameters have been added to the call.

#### Carbon Emissions from Biomass Loss

This widget is used by MapBuilder to display results of the biomass loss analysis. It requries that MapBuilder pass a tcd treshold, period, and geostore to the Vega Widget which will be apended to the Vega url analysis call.

| Widget Name     |Carbon-Emissions.json|
| -----------     |---|
| Description     |This widget is used to calculate carbon emissions from above ground biomass loss|
| DatasetID       |ca7ddf2b-4c4b-485f-afe7-3c1d3eea0c1f|
| WidgetID        |ac38fdbd-fdb1-4d8e-9109-674013fb51a2|
| API Widget Link |https://production-api.globalforestwatch.org/v1/dataset/ca7ddf2b-4c4b-485f-afe7-3c1d3eea0c1f/widget/ac38fdbd-fdb1-4d8e-9109-674013fb51a2|
| VEGA Analysis Url|https://production-api.globalforestwatch.org/v2/biomass-loss?table=true|
| Parameters to Pass|period,tresh,geostore|
| Analysis Endpoint |https://production-api.globalforestwatch.org/v2/biomass-loss?table=true&period=2001-01-01,2018-12-31&geostore=18fe450d0cfd37754d61416e9113a9bd&thresh=30|







