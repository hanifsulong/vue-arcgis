<template>
  <div ref="map" class="map" id="viewDiv"></div>
</template>

<script>
import { loadModules } from 'esri-loader';

export default {
  name: 'Mapviewer',
  mounted(){
    const options = { version: '3.28', css: true}
    loadModules(['esri/views/MapView', 'esri/Map'],options)
    .then(([MapView, Map]) => {
      // then we load a web map from an id
      var webmap = new Map({
        // portalItem: { // autocasts as new PortalItem()
        //   id: 'f2e9b762544945f390ca4ac3671cfa72'
        // }
        basemap: "streets",
      });
      // and we show that map in a container w/ id #viewDiv
      var view = new MapView({
        map: webmap,
        // logo: false,
        container: this.$refs.map,
        center: [-56.049, 38.485],
        zoom: 3
      });
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
