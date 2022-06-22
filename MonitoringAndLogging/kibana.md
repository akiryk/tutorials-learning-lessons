# Kibana

Kibana lets you visualize your Elasticsearch data and navigate the Elastic Stack so you can do anything from tracking query load to understanding the way requests flow through your apps.

## Make a Dashboard

To make a dashboard, you need to first have some visualizations

### Make a Visualization

- Go to Kibana and select the "Visualize" Tab. 
- Click the `PLUS` icon and select a visualization type, e.g. Tag Cloud
- For a new search, use `stores:*log*` 
- Use the Buckets panel in side bar to choose what to display in visualization.

### An exampole

- Choose "pie chart" as the type of chart


### RegisterGroup
The `RegisterGroup` component enables you to use batch actions, such as fetching data for several items or updating several subscribers.
| Prop | Type |  Required / Default | Description
| --- | --- | --- | --- |
|`groupName` | string | no | an arbitrary identifier for a group
|`fetchSelectionOfItems`| function | no | An async batch fetch function that should return a promise, see example below.
|`identifierGenerator`| function | no | A function for generating an identifier based on the form of your data, see example below.
