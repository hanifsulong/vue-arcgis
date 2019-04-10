<template>
  <div ref="map" class="map" id="viewDiv"></div>
</template>

<script>
import { loadModules, loadCss } from 'esri-loader';


export default {
  mounted(){
    loadCss('3.28');
    const options = { version: '3.28', css: true};

    loadModules(['esri/map', 'esri/layers/ArcGISDynamicMapServiceLayer'], options)
      .then(([Map]) => {
        // var layer = new ArcGISDynamicMapServiceLayer(
        //   "http://sampleserver1.arcgisonline.com/ArcGIS/rest/services/Louisville/LOJIC_LandRecords_Louisville/MapServer",{
        //     useMapImage: true
        //   }
        // );

        // create map with the given options at a DOM node w/ id 'viewDiv'
        let map = new Map('viewDiv', {
          center: [101.736, 3.1805],
          zoom: 8,
          basemap: 'streets'
        });

      })
      .catch(err => {
        // handle any script or module loading errors
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
