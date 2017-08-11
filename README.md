# new-nepal-topojson

This module simply provides a topojson file that contains new administrative boundaries for Nepal.

## Usage
Import the module through npm:
`npm install new-nepal-topojson`


After importing you can easily use the topojson through leaflet as follows:

```javascript
import L from 'leaflet';
import { municipalities } from 'new-nepal-topojson';
import { districts } from 'new-nepal-topojson';

// some javascript code to initialize Leaflet Map here

L.TopoJSON = L.GeoJSON.extend({
  addData(jsonData) {
    if (jsonData.type === 'Topology') {
      for (const key in jsonData.objects) {
        const geojson = topojson.feature(jsonData, jsonData.objects[key]);
        L.GeoJSON.prototype.addData.call(this, geojson);
      }
    } else {
      L.GeoJSON.prototype.addData.call(this, jsonData);
    }
  },
});

const topoLayer = new L.TopoJSON();
topoLayer.addData(municipalities);
topoLayer.addData(districts)
topoLayer.addTo(map);

```
