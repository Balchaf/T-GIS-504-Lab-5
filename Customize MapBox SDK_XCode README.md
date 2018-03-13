# Customize MapBox SDK Example using XCODE

For this assignmnet, I take Mapbox SDK Examples from https://www.mapbox.com/install/ios/download/
Adding marker Template and customize in XCODE

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
/

//  ViewController.swift

//  AddinMarker

//

//  Created by mjk3ll3y on 3/11/18.

//  Copyright © 2018 Kulm. All rights reserved.

//


import Mapbox


class ViewController: UIViewController, MGLMapViewDelegate {

    override func viewDidLoad() {

        super.viewDidLoad()

        

        let mapView = MGLMapView(frame: view.bounds)

        mapView.autoresizingMask = [.flexibleWidth, .flexibleHeight]

        

        // Set the map’s center coordinate and zoom level.
        //This is where I changed the center coordiante from New york to Tacoma and in addition, I changed the zoom level to 15

        mapView.setCenter(CLLocationCoordinate2D(latitude: 47.244598, longitude: -122.437659), zoomLevel: 15, animated: false)

        view.addSubview(mapView)

        

        // Set the delegate property of our map view to `self` after instantiating it.

        mapView.delegate = self

        

        // Declare the marker `myschool` and set its coordinates, title, and subtitle.
        // I add markeer to my place of interest; Tacoma (University of Washington Tacoma) as a subtittle

        let myschool = MGLPointAnnotation()

        myschool.coordinate = CLLocationCoordinate2D(latitude: 47.244598, longitude: -122.437659)

        myschool.title = "My School!"

        myschool.subtitle = "University of Washington Tacoma"

        

        // Add marker `myschool` to the map.
        //the following line adds the annotation I declared above to added to the map

        mapView.addAnnotation(myschool)

    }

    

    // Use the default marker. See also: our view annotation or custom marker examples.

    func mapView(_ mapView: MGLMapView, viewFor annotation: MGLAnnotation) -> MGLAnnotationView? {

        return nil

    }

    

    // Allow callout view to appear when an annotation is tapped.

    func mapView(_ mapView: MGLMapView, annotationCanShowCallout annotation: MGLAnnotation) -> Bool {

        return true

    }

}


```

