# classical-music
<script>
map.on("load", function() {
        // Add an image to use as a custom marker
        map.loadImage(
          "https://daks2k3a4ib2z.cloudfront.net/5ea5f8c50881540a15ba7289/5f18f24c21df271fdc03645f_placeholder-filled-point%20(1)-p-130x130q80.png",
          function(error, image) {
            if (error) throw error;
            map.addImage("custom-marker", image);
            // Add a GeoJSON source with 3 points.
            map.addSource("points", {
              type: "geojson",
              data: {
                type: "FeatureCollection",
                features: [
                  {
                    type: "Feature",
                    properties: {'description':
'<strong>Mad Men Season Five Finale Watch Party</strong><p>Head to Lounge 201 (201 Massachusetts Avenue NE) Sunday for a <a href="http://madmens5finale.eventbrite.com/" target="_blank" title="Opens in a new window">Mad Men Season Five Finale Watch Party</a>, complete with 60s costume contest, Mad Men trivia, and retro food and drink. 8:00-11:00 p.m. $10 general admission, $20 admission and two hour open bar.</p>'},
                    geometry: {
                      type: "Point",
                      coordinates: [-73.9455556, 40.8323113]
                    }
                  },
                  {
                    type: "Feature",
                    properties: {'description':
'<strong>Truckeroo</strong><p><a href="http://www.truckeroodc.com/www/" target="_blank">Truckeroo</a> brings dozens of food trucks, live music, and games to half and M Street SE (across from Navy Yard Metro Station) today from 11:00 a.m. to 11:00 p.m.</p>'},
                    geometry: {
                      type: "Point",
                      coordinates: [-73.972729, 40.793897]
                    }
                  },
                  {
                    type: "Feature",
                    properties: {'description':
'<strong>A Little Night Music</strong><p>The Arlington Players\' production of Stephen Sondheim\'s  <a href="http://www.thearlingtonplayers.org/drupal-6.20/node/4661/show" target="_blank" title="Opens in a new window"><em>A Little Night Music</em></a> comes to the Kogod Cradle at The Mead Center for American Theater (1101 6th Street SW) this weekend and next. 8:00 p.m.</p>'},
                    geometry: {
                      type: "Point",
                      coordinates: [-73.9634756, 40.8080582]
                    }
                  }
                ]
              }
            });

            // Add a symbol layer
            map.addLayer({
              id: "symbols",
              type: "symbol",
              source: "points",
              layout: {
                "icon-image": "custom-marker"
              }
            });
          }
        );
        // When a click event occurs on a feature in the places layer, open a popup at the
        // location of the feature, with description HTML from its properties.
        map.on("click", "symbols", function(e) {
          var coordinates = e.features[0].geometry.coordinates.slice();
          var description = e.features[0].properties.description;

          // Ensure that if the map is zoomed out such that multiple
          // copies of the feature are visible, the popup appears
          // over the copy being pointed to.
          while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
            coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360;
          }

          new mapboxgl.Popup()
            .setLngLat(coordinates)
            .setHTML(description)
            .addTo(map);
        });
        // Center the map on the coordinates of any clicked symbol from the 'symbols' layer.
        map.on("click", "symbols", function(e) {
          map.flyTo({
            center: e.features[0].geometry.coordinates
          });
        });

        // Change the cursor to a pointer when the it enters a feature in the 'symbols' layer.
        map.on("mouseenter", "symbols", function() {
          map.getCanvas().style.cursor = "pointer";
        });

        // Change it back to a pointer when it leaves.
        map.on("mouseleave", "symbols", function() {
          map.getCanvas().style.cursor = "";
        });
      });
    </script>
