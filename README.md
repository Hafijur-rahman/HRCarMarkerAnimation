# HRCarMarkerAnimation

[![](https://jitpack.io/v/TecOrb-Developers/HRMarkerAnimation.svg)](https://jitpack.io/#TecOrb-Developers/HRMarkerAnimation)



<br>
<meta name="google-site-verification" content="9xX5qBXiwU0-eOti0o3ujCSFXmus9BTbz6Dw5FNmtm0" />
Smooth marker animation on google map along with proper turns and camera bearing. 
<br>

# Demo
<img src="https://github.com/TecOrb-Developers/HRMarkerAnimation/blob/master/markerAnimation.gif?raw=true" width="250" height="400"/>

<br><br>

## Steps:

Pass the Marker to animate, googlemap, Location of current position and Old Location of the marker of the user, 
duration of the animation & UpdateLocationCallBack Callback interface.

``` java
 private Location mLastLocation;
 private Location oldLocation;
 
 new HRMarkerAnimation(googleMap,1000, new UpdateLocationCallBack() {
                        @Override
                        public void onUpdatedLocation(Location updatedLocation) {
                            oldLocation = updatedLocation;
                        }
                    }).animateMarker(mLastLocation, oldLocation, marker);
```
<br>
Here marker, googlemap,mLastLocation refers to the position of marker,oldLocation position refers to the position of 
the maker for calculating the slop of marker. 
These four fields are mandatory.
<br><br>

<br>

  duration refers to the animation time. By default it will take 1000.
callback is the interface of Googlemap UpdatedLoation Callback return Old location. It requires when the user wants to animate the next animation 
after the first has finished.
<br>


The isMarkerVisible method return true or false if marker is visible on user device screen then it return false 
whenever the marker is not visible means outside the screen then it automatically animate to center of the screen

For eg-

``` java
private boolean isMarkerVisible(GoogleMap googleMap, LatLng newLocation) {
        return googleMap.getProjection().getVisibleRegion().latLngBounds.contains(newLocation);
    }
```
Note:
    If you are animating car onLocationChanged() then,
   Ideal location request for car animation should be as below. Greater than the interval mentioned will give
   more good results but less than this may hamper the animation.
   ``` java
    mLocationRequest = new LocationRequest();
    mLocationRequest.setInterval(1000 * 5);
    mLocationRequest.setFastestInterval(1000 * 3);
    mLocationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
   ``` 
 

## Dependency

```groovy
App Level:
dependencies {
	   implementation 'com.github.TecOrb-Developers:HRMarkerAnimation:xyz'
	}
  
```
```groovy
Project Level:
maven { url 'https://jitpack.io' }
``` 
 Replace xyz with latest version
 
  <br><br>

# Developers