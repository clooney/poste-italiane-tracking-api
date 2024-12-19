# TrackingMore: Tracking Webhook
The TrackingMore webhook delivers near real-time notifications for shipment status changes to a specified URL, allowing for customized status alerts. This service streamlines the monitoring process, ensuring immediate data response via your configured URL.

## Webhook Overview
### How to Set Up the Webhook
* Create your own webhook URL.
* Access [TrackingMore’s admin](https://www.trackingmore.com/signup.html).
* Add webhook URL under developer setting (Max. 4 URLs per account).


### Security Practices
TrackingMore supports either HTTP or HTTPS urls. Opt for HTTPS to secure data transmissions. 

Note: your endpoint will be public.

### Retry Mechanism
TrackingMore's webhook utilizes the POST method to transmit event-driven data. For deliveries that fail (HTTP responses outside the 200-299 range), there's a strategy to retry up to 14 times, utilizing an exponential back-off mechanism. The delay between retries is calculated using the formula: 2^(retry attempt) x 30 seconds, ensuring efficient and persistent attempt to deliver data without immediate repetition, enhancing the chance for success over time.

## Webhook Specification
### Webhook Signature
Each webhook notification includes a header with a digital signature. This signature, a base64-encoded HMAC, is generated using the sha256 algorithm with the webhook request body and your account's webhook secret.

### How to compute HMAC signature
* Get the Webhook Secret.

~~~
2e55b9a3-4dd1-4416-9897-c4bd1e3d738f
~~~

Note: Webhook Secret is only for V4 version Webhook.

* Compute HMAC signature by using Sha256. The following is a Golang example.

~~~
WEBHOOK_SECRET := "2e55b9a3-4dd1-4416-9897-c4bd1e3d738f"
timestamp := "1662371528"

func GenerateSignature(apiKey, timestamp string) string {
	h := hmac.New(sha256.New, []byte(WEBHOOK_SECRET))
	h.Write([]byte(timestamp))
	return hex.EncodeToString(h.Sum(nil))
}

// HMAC signature: a37084ab68ae16b77db1f8463f31be9fcc965e2515e03efecf8139bb1e511b06
~~~

* Compare the computed HMAC signature against the signature in the webhook's header for verification.

