<template>
  <div>
    <div id="map"></div>
  </div>
</template>

<script>
export default {
  name: "MapView", // 컴포넌트 이름 지정
  data() {
    return {
      // map 객체 설정
      map: null,
    };
  },
  setup() {},
  created() {},
  mounted() {
    // api 스크립트 소스 불러오기 및 지도 출력
    if (window.kakao && window.kakao.maps) {
      this.loadMap();
    } else {
      this.loadScript();
    }
  },
  unmounted() {},
  methods: {
    // api 불러오기
    loadScript() {
      const script = document.createElement("script");
      script.src = "//dapi.kakao.com/v2/maps/sdk.js?appkey=//&autoload=false";
      script.onload = () => window.kakao.maps.load(this.loadMap);

      document.head.appendChild(script);
    },
    // 맵 출력하기
    loadMap() {
      const container = document.getElementById("map");
      const options = {
        center: new window.kakao.maps.LatLng(33.450701, 126.570667),
        level: 3,
      };

      this.map = new window.kakao.maps.Map(container, options);
      this.loadMarker();
    },
    // 지정한 위치에 마커 불러오기
    loadMarker() {
      const markerPosition = new window.kakao.maps.LatLng(
        33.450701,
        126.570667
      );

      const marker = new window.kakao.maps.Marker({
        position: markerPosition,
      });

      marker.setMap(this.map);
    },
  },
};
</script>

<style lang="scss" scoped>
#map {
  width: 800px;
  height: 500px;
}
</style>
