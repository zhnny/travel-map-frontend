<template>
  <div class="olmap" id="map">
  </div>
</template>

<style scoped>
.olmap {
  width: 100%;
  height: 100%;
}
</style>
<script>
import { Map, View } from "ol"
import * as olProj from "ol/proj"
import TileLayer from "ol/layer/Tile"
import XYZ from "ol/source/XYZ"
import SourceVector from 'ol/source/Vector'
import LayerVector from 'ol/layer/Vector'
import GeoJSON from 'ol/format/GeoJSON'


export default {
  name: "ol-map",
  components: {},
  data() {
    return {
      openMap: null,
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      var vectorSource = new SourceVector({
                url: "/final_map.json",
                format: new GeoJSON()
            })
      this.openMap = new Map({
        target: "map",
        layers: [
          new TileLayer({
            source: new XYZ({
              url: "http://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png",
            }),
          }),
          new LayerVector({
            source: vectorSource
          }),
        ],
        view: new View({
          // 将西安作为地图中心 
          center: olProj.fromLonLat([112.92597770690918,28.186654954789518]),
          zoom: 14,
        }),
        controls: [],
      });
    },
  },
};

</script>