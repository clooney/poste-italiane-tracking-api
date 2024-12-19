# TrackingMore: Poste Italiane Tracking API
[Poste Italiane Tracking API](https://www.trackingmore.com/poste-italiane-tracking-api.html) enables you to connect tracking info of Poste Italiane shipments into your system, improving shipment visibility. 

Besides Poste Italiane, TrackingMore supports shipment tracking across 1,200+ global carriers through a robust [multi-carrier shipment tracking API](https://www.trackingmore.com/tracking-api).

TrackingMore provides API compatibility with seven programming languages. Comprehensive documentation for setup and use is included within this repository to facilitate the integration process.

### Features
   *  Unified real-time tracking information for Poste Italiane shipments.
   *  Webhook support for automatic shipment status updates.

### Tracking Status Glossary

We categorize shipment statuses into clear, concise strings like pending, notfound, transit, and more, each indicating a specific stage in the shipment's journey.
String | Description 
----|------
inforeceived | The courier has received the package info and is about to pick up the package.
transit	| The package is in transit and has a good transportation condition.
pickup	| The package has arrived at the local point or is on the way to your home.
undelivered	| The delivery of the package was attempted but failed due to some reasons. Usually, the courier will arrange another delivery soon.
delivered |	The package has been delivered. Congratulations!
exception | The package might have been sent to the sender, damaged, lost or other exceptions.
expired	| The last track of the package has not been updated for 30 days. When this happens, please contact the Courier for more details.
notfound | The tracking info is not available currently. But you may track it after a while.
pending | The package is pending as the courier did not return the tracking infomation.

### Server Response Codes
The API responds with standard HTTP status codes to indicate the success or failure of an API request, such as 200 OK for successful requests or 401 Unauthorized for authentication errors.
Code | Description
----|------
200	| Success - Request response is successful.
400	| BadRequest - Request type error. Please check the API documentation for the request type of this API.
4101 | BadRequest - Tracking No. already exists.
4102 | BadRequest - Tracking No. no exists. Please use 「Create a tracking」 API first to create shipment.
4103 | BadRequest - You have exceeded the shipment quantity of API call. The maximum quantity is 40 shipments per call.
4110 | Bad Request - The value of tracking_number is invalid.
4111 | Bad Request - Tracking_number is required.
4112 | Bad Request - Invalid Tracking ID.
4113 | Bad Request - Retrack is not allowed. You can only retrack an expired tracking.
4120 | Bad Request - The value of courier_code is invalid.
4121 | Bad Request - Cannot detect courier.
4122 | Bad Request - Missing or invalid value of the special required fields for this courier.
4130 | Bad Request - The format of Field name is invalid.
4160 | BadRequest - The awb_number is required or invaild format.
4161 | BadRequest - The awb airline does not support yet.
4162 | BadRequest - A batch supports only 20 awb_numbers.
4163 | BadRequest - Failed to delete air waybill number.
4164 | BadRequest - Failed to create air waybill number.
4165 | BadRequest - Query failed: Air waybill number not created.
4166 | BadRequest - Failed to delete an uncreated air waybill number.
4167 | BadRequest - The air waybill number already exists, no need to create it again.
4168 | BadRequest - You have exceeded the number of API calls created. The maximum quantity created each time is 20 air waybill numbers.
4190 | BadRequest - You are reaching the maximum quota limitation, please upgrade your current plan.
401 | Unauthorized - Authentication failed or has no permission. Please check and ensure your API Key is correct.
403	| Forbidden - Access prohibited. The request has been refused or access is not allowed.
404 | NotFound - Page does not exist. Please check and ensure your link is correct.
429 | TooManyRequests - Exceeded API request limits, please try again later. Please check the API documentation for the limit of this API.
511	| ServerError - Server error. Please contact us: service@trackingmore.org.
512	| ServerError - Server error. Please contact us: service@trackingmore.org.
513	| ServerError - Server error. Please contact us: service@trackingmore.org.




