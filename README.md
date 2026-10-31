import { Valhalla } from '@routingjs/valhalla';

const valhalla = new Valhalla('https://valhalla1.openstreetmap.de'); // خادم تجريبي

async function getRoute() {
  const route = await valhalla.directions({
    locations: [
      { lat: 33.3152, lon: 44.3661 }, // نقطة البداية (بغداد)
      { lat: 33.3128, lon: 44.3615 }  // نقطة النهاية
    ],
    costing: 'auto' // وسيلة النقل (سيارة)
  });
  console.log(route);
}import MapLibreGL from '@maplibre/maplibre-react-native';
import { View } from 'react-native';

// ... (تكوين الاتصال بـ Valhalla للحصول على بيانات المسار)

const MapScreen = () => {
  const routeGeoJSON = { /* بيانات GeoJSON التي حصلت عليها من Valhalla */ };

  return (
    <View style={{ flex: 1 }}>
      <MapLibreGL.MapView style={{ flex: 1 }} mapStyle="https://demotiles.maplibre.org/style.json">
        <MapLibreGL.Camera centerCoordinate={[44.3661, 33.3152]} zoomLevel={13} />
        {routeGeoJSON && (
          <MapLibreGL.ShapeSource id="routeSource" shape={routeGeoJSON}>
            <MapLibreGL.LineLayer id="routeLayer" style={{ lineColor: 'blue', lineWidth: 4 }} />
          </MapLibreGL.ShapeSource>
        )}
      </MapLibreGL.MapView>
    </View>
  );
};# -
