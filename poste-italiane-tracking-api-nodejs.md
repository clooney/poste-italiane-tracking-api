Poste Italiane Tracking API - Node.js
================================
Use Node.js to track Poste Italiane shipments with Poste Italiane Tracking API.

Features
--------
- Real-time Poste Italiane tracking.
- Batch Poste Italiane tracking.
- Other features to manage your Poste Italiane tracking.

Installation
------------

Installation is easy:

    $ npm install trackingmore-sdk-nodejs

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your Poste Italiane shipments.

Usage
----------

Create a tracking (Real-time tracking):

      const TrackingMore = require('trackingmore-sdk-nodejs')
      const key = 'your api key'
      const trackingmore = new TrackingMore(key)
      
      const params = {
        'tracking_number': 'LS988368225NL',
        'courier_code': 'poste-italiane',
        'order_number': '',
        'customer_name': '',
        'title': '',
        'language': 'en',
        'note': 'test Order'
      }
      trackingmore.trackings.createTracking(params)
        .then(result => console.log(result))
        .catch(e => console.log(e))


Create trackings (Max. 40 tracking numbers create in one call):

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)
    
    const params = [{
        'tracking_number': 'CP098116093IT',
        'courier_code':'poste-italiane'
    },{
      'tracking_number': '1ZR8E2200404839077',
      'courier_code':'poste-italiane'
    }]
    trackingmore.trackings.batchCreateTrackings(params)
      .then(result => console.log(result))
      .catch(e => console.log(e))



Get status of the shipment:

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)

    # Perform queries based on various conditions
    const params = [{
        'tracking_number': 'LS988368225NL',
        'courier_code':'poste-italiane'
    },{
      'tracking_number': 'CP098116093IT',
      'courier_code':'poste-italiane'
    }]
    trackingmore.trackings.batchCreateTrackings(params)
      .then(result => console.log(result))
      .catch(e => console.log(e))


Update a tracking by ID:

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)
    
    const params = {
        'customer_name': 'New name',
        'note':'New test order note'
    }
    const idString = "97a7b322e346b7353d6dbb6fb37aed39"
    trackingmore.trackings.updateTrackingByID(idString, params)
      .then(result => console.log(result))
      .catch(e => console.log(e))

