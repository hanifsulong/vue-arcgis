<template>
  <div ref="map" class="map" id="viewDiv"></div>
</template>

<script>
import { loadModules } from 'esri-loader';

export default {
  name: 'Mapviewer',
  mounted(){
    const options = { version: '4.11', css: true}
    loadModules(['esri/views/MapView', 'esri/Map', 'esri/layers/FeatureLayer', 'esri/widgets/BasemapToggle'],options)
    .then(([MapView, Map, FeatureLayer, BasemapToggle]) => {

      var featureLayer = new FeatureLayer({
        url: "https://services.arcgis.com/P3ePLMYs2RVChkJx/ArcGIS/rest/services/ACS_Marital_Status_Boundaries/FeatureServer/2"
      });

      // then we load a web map from an id
      var webmap = new Map({
        // portalItem: { // autocasts as new PortalItem()
        //   id: 'f2e9b762544945f390ca4ac3671cfa72'
        // }
        basemap: "streets-navigation-vector",
        layers: [featureLayer]
      });
      // and we show that map in a container w/ id #viewDiv
      var view = new MapView({
        map: webmap,
        // logo: false,
        container: this.$refs.map,
        // center: [-73.95, 40.702],
        // zoom: 11
        center: [101.736, 3.1805],
        zoom: 8
      });

      var toggle = new BasemapToggle({
        view: view,
        nextBasemap: 'hybrid'
      })

      view.ui.add(toggle, 'bottom-right')

      view.popup.autoOpenEnabled = false
      view.on('click', function(e){
        // console.log(view.popup);
        view.popup.open({
          title: 'POPUP TITLE',
          content: `Longitude: ${e.mapPoint.longitude} </br> Latitude: ${e.mapPoint.latitude}`,
          location: e.mapPoint,
          zoom: false
        })
      })
    })
    .catch(err => {
      // handle any errors
      console.error(err);
    });
  }
}
</script>

<style lang="css" scoped>
  .map{
    height: 600px;
    width: 100%;
  }
</style>
