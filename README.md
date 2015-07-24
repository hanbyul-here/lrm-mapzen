Leaflet Routing Machine / Valhalla by Mapzen
=====================================


     ██▒   █▓ ▄▄▄       ██▓     ██░ ██  ▄▄▄       ██▓     ██▓    ▄▄▄      
    ▓██░   █▒▒████▄    ▓██▒    ▓██░ ██▒▒████▄    ▓██▒    ▓██▒   ▒████▄    
     ▓██  █▒░▒██  ▀█▄  ▒██░    ▒██▀▀██░▒██  ▀█▄  ▒██░    ▒██░   ▒██  ▀█▄  
      ▒██ █░░░██▄▄▄▄██ ▒██░    ░▓█ ░██ ░██▄▄▄▄██ ▒██░    ▒██░   ░██▄▄▄▄██ 
       ▒▀█░   ▓█   ▓██▒░██████▒░▓█▒░██▓ ▓█   ▓██▒░██████▒░██████▒▓█   ▓██▒
       ░ ▐░   ▒▒   ▓▒█░░ ▒░▓  ░ ▒ ░░▒░▒ ▒▒   ▓▒█░░ ▒░▓  ░░ ▒░▓  ░▒▒   ▓▒█░
       ░ ░░    ▒   ▒▒ ░░ ░ ▒  ░ ▒ ░▒░ ░  ▒   ▒▒ ░░ ░ ▒  ░░ ░ ▒  ░ ▒   ▒▒ ░
         ░░    ░   ▒     ░ ░    ░  ░░ ░  ░   ▒     ░ ░     ░ ░    ░   ▒   
          ░        ░  ░    ░  ░ ░  ░  ░      ░  ░    ░  ░    ░  ░     ░  ░
         ░                                                                    


Extends [Leaflet Routing Machine](https://github.com/perliedman/leaflet-routing-machine) with support for [Valhalla](https://mapzen.com/projects/valhalla).

Valhalla is a free, open-source routing service with dynamic run-time costing that lets you integrate automobile, bicycle, and pedestrian navigation into a web or mobile application. To use Valhalla with the Leaflet Routing Machine, install the lrm-valhalla plug-in with npm and get your free API key from mapzen.com/developers.

## How to use

As with the other LRM plug-ins, you can [download lrm-valhalla](https://mapzen.com/resources/lrm-valhalla-0.0.9.zip) and insert the JavaScript file into your page right after the line where it loads Leaflet Routing Machine:

    [...]
    <script src="leaflet-routing-machine.js"></script>
    <script src="lrm-valhalla.js"></script>
    [...]

Insert your [Valhalla API key](https://mapzen.com/developers) and the routing mode ( auto, bicycle, or pedestrian); see the [Valhalla API documentation](https://github.com/valhalla/valhalla-docs/blob/gh-pages/api-reference.md) for more information.

    L.Routing.control({
      [...]
      router: L.Routing.valhalla('my-api-key', 'auto')
      formatter: new L.Routing.Valhalla.Formatter()
    })


## Using Valhalla with npm and Browserify

Like other plug-ins, the Valhalla plug-in can be installed using npm instead of downloading the script manually:

    npm install --save lrm-valhalla

Once the Valhalla plug-in is installed, update the router and formatter instances to tell the Leaflet Routing Machine to use Valhalla’s engine. 

    var L = require('leaflet');
    require('leaflet-routing-machine');
    require('lrm-valhalla');

    L.Routing.control({
      router: L.Routing.valhalla('my-api-key', 'auto'),
      formatter: new L.Routing.Valhalla.Formatter()
    });

For router, insert your [Valhalla API key](https://mapzen.com/developers) and the routing mode (such as auto, bicycle, or pedestrian); see the [Valhalla API documentation](https://github.com/valhalla/valhalla-docs/blob/gh-pages/api-reference.md) for more information. (Note that no options are needed for formatter.)

You can also change the routing mode after the router is created. Say you had different transportation options on your map and wanted to change `transitmode` to bicycle when that button is clicked: 

    var rr = L.Routing.valhalla('my-api-key', 'auto');
    [...]
    bikeButton.onClick: function () {
      rr.route({transitmode: "bicycle"});
    }

## Running local example

If you want to run your lrm-valhalla plug-in locally for test and development purposes:

- Install lrm-valhalla through npm or [download the contents of the lrm-valhalla repo](https://github.com/valhalla/lrm-valhalla/archive/master.zip)
- get your API key from [mapzen.com/developers](https://mapzen.com/developers)
- paste it into the example's index.js and choose the transportation mode (auto, bicycle, or pedestrian)
- start a local web server (such as python -m SimpleHTTPServer or the local server you prefer)
- go to localhost:8000/examples in your browser (all assets to run Valhalla are in the /examples folder)

