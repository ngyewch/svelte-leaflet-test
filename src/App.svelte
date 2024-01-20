<script lang="ts">
    import {onMount} from 'svelte';
    import {CircleMarker, GeoJSON, LeafletMap, TileLayer} from 'svelte-leafletjs';
    import type {GeoJSONOptions, MapOptions, TileLayerOptions} from 'leaflet';

    const mapOptions: MapOptions = {
        center: [1.250111, 103.830933],
        zoom: 13,
    };
    const tileUrl = "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png";
    const tileLayerOptions: TileLayerOptions = {
        minZoom: 0,
        maxZoom: 20,
        maxNativeZoom: 19,
        attribution: "© OpenStreetMap contributors",
    };
    const geoJsonOptions: GeoJSONOptions = {
        style: function (geoJsonFeature) {
            console.log('style', geoJsonFeature);
            return {};
        },
        onEachFeature: function (feature, layer) {
            console.log('onEachFeature', feature, layer);
        },
    };

    let leafletMap: LeafletMap;

    onMount(() => {
        if (leafletMap) {
            const map = leafletMap.getMap();
            if (map) {
                map.fitBounds([[1.266835, 103.796403], [1.232988, 103.854861]]);
            }
        }
    });
</script>

<div class="example" style="width: 100%; height: 100%;">
    <LeafletMap bind:this={leafletMap} options={mapOptions}>
        <TileLayer url={tileUrl} options={tileLayerOptions}/>
        <GeoJSON options={geoJsonOptions}/>
        <CircleMarker latLng={[1.2461196,103.8298412]}></CircleMarker>
    </LeafletMap>
</div>
