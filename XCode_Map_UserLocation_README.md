# Using XCODE: Building a simple mobile app having map, User location and finding direction between two points

The following code is written to build a simple mobile app having map, user location and finding route between two points using Xcode 


```
//

//  ViewController.swift

//  Lab5FL

//

//  Created by mjk3ll3y on 3/11/18.

//  Copyright © 2018 Kulm. All rights reserved.

//


import UIKit

import MapKit


class ViewController: UIViewController, MKMapViewDelegate, CLLocationManagerDelegate {


    @IBOutlet var mapkitView: MKMapView!

    let locationManager = CLLocationManager()

    override func viewDidLoad() {

        super.viewDidLoad()

        

        mapkitView.delegate = self

        mapkitView.showsScale = true

        mapkitView.showsPointsOfInterest = true

        mapkitView.showsUserLocation = true

        

        locationManager.requestAlwaysAuthorization()

        locationManager.requestWhenInUseAuthorization()

        

        if CLLocationManager.locationServicesEnabled() {

            locationManager.delegate = self

            locationManager.desiredAccuracy = kCLLocationAccuracyBest

            locationManager.startUpdatingLocation()

        }

        let sourceCoordinates = locationManager.location?.coordinate

        let destCoordinates = CLLocationCoordinate2DMake(47.2456, -122.454)

        let sourcePlacemark = MKPlacemark(coordinate: sourceCoordinates!)

        let destPlacemark = MKPlacemark(coordinate: destCoordinates)

        

        let sourceItem = MKMapItem(placemark: sourcePlacemark)

        let destItem = MKMapItem(placemark: destPlacemark)

        

        let directionRequest = MKDirectionsRequest()

        directionRequest.source = sourceItem

        directionRequest.destination = destItem

        directionRequest.transportType = .automobile

        

        let directions = MKDirections(request: directionRequest)

        directions.calculate(completionHandler: {

            response, error in

            

            guard let response = response else {

                if let error = error {

                    print ("Something went wrong")

                }

                return

            }

            let route = response.routes[0]

            self.mapkitView.add(route.polyline, level: .aboveRoads)

            

            let rekt = route.polyline.boundingMapRect

            self.mapkitView.setRegion(MKCoordinateRegionForMapRect(rekt), animated: true)

        })

        

    }

    func mapView(_ mapView: MKMapView, rendererFor overlay: MKOverlay) -> MKOverlayRenderer {

        let renderer = MKPolylineRenderer(overlay: overlay)

        renderer.strokeColor = UIColor.blue

        renderer.lineWidth = 5.0

        return renderer

    }


    override func didReceiveMemoryWarning() {

        super.didReceiveMemoryWarning()

        // Dispose of any resources that can be recreated.

    }



}


```


