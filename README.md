# gn-path-follower

Navigation path follower for mobile phones, cars or gn-gps-simulator. Below is a little screencast:

![Loading gif](https://cloud.githubusercontent.com/assets/9342018/17696472/d6acaabe-63ae-11e6-94ed-f1354a0837a4.gif)

## Setup Instructions

Clone the project (or download and extract zip).

```
git clone https://github.com/Greennav/gn-path-follower
```

### Dependencies

Element dependencies are managed via [Bower](http://bower.io/). You can install that (globally) via:

```
npm install -g bower
```

Move in the project folder and download the element's dependencies:

```
bower install
```

### Documentation and Demo

Use [Polyserve](https://github.com/PolymerLabs/polyserve) to play with gn-path-follower, read the documentation and watch the demo. You can install it via:

```
npm install -g polyserve
```

And you can run it via:

```
polyserve
```

Once running, you can preview your element at `http://localhost:8080/components/gn-path-follower/`, where `gn-path-follower` is the name of the directory containing it.

**Note:** This element can be combined with [`gn-api`](https://github.com/Greennav/gn-api) to get its routing informations. `gn-api` will be installed automatically as dev-dependency via bower, so you can see it in action at the demo. In addition `gn-api` needs data via its `url` property. To get a mockup response you can install and start [`routing service`](https://github.com/Greennav/service-routing).

### Short example

Call the `startSimulation()` method and the position will move according to the next coordinates obtaining from server data (see [`gn-api`](https://github.com/Greennav/gn-api) and [`routing service`](https://github.com/Greennav/service-routing)). Also you can stop and reset the simulation with the appropriate methods.

```html
<!-- To get mockup data use gn-api and service-routing. -->
<gn-api id="gnapi" route="{{route}}"></gn-api>

<!-- Don't forget to get the route. -->
<paper-button on-tap="gnapi.getRoute()">get route</paper-button>

<!-- Change speed in waypoint per second easily, even live. -->
<paper-slider id="speed" pin snaps
              max="5" min="0.5" step="0.5" value="1"></paper-slider>

<paper-button on-tap="sim.startSimulation()">start</paper-button>
<paper-button on-tap="sim.stopSimulation()">stop</paper-button>
<paper-button on-tap="sim.restartSimulation()">reset</paper-button>

<gn-gps-simulator id="sim"
                  route="{{route.route}}"
                  longitude="{{lon}}"
                  latitude="{{lat}}"
                  interpolation-iter="5"
                  speed="10"></gn-gps-simulator>

<div id="map" class="flex">
  <gn-notification-container id="notifications"
                             hidden="true"
                             turn-code="[[direction]]"
                             distance="[[turnDistance]]"
                             locale="en"></gn-notification-container>
  <gn-path-follower id="map"
                    route="{{route.route}}"
                    latitude="[[lat]]"
                    longitude="[[lon]]"
                    onpath="{{onpath}}"
                    dist="{{distance}}"
                    turn-code="{{direction}}"
                    turn-dist="{{turnDistance}}"></gn-path-follower>
  </div>
```
