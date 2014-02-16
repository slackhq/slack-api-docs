# Attachments

It is possible to create more richly-formatted messages using Attachments.

Attachments can be added to messages in different ways:

* For [Incoming Webhooks](https://my.dev.slack.com/services/new/incoming-webhook), send a regular payload, but include an `attachments` array, where each element is a hash containing an attachment.
* For [the API](/methods/chat.postMessage), include an `attachments` property, containing a JSON-encoded array of attachment hashesh.
* For [Hammock](https://github.com/tinyspeck/hammock), pass an array of attachment hashes.


## Attachment structure

Messages can have zero of more attachments, defined as an array. Each hash in that array will contain multiple properties:

	{
		"fallback": "Required text summary of the attachment that is shown by clients that understand attachments
						but choose not to show them.",

		"text": "Optional text that should appear within the attachment",
		"pretext": "Optional text that should appear above the formatted data",

		"color": "#36a64f", // Can either be one of 'good', 'warning', 'danger', or any hex color code

		// Fields are displayed in a table on the message
		"fields": [
			{
				"title": "Required Field Title", // The title may not contain markup and will be escaped for you
				"value": "Text value of the field. May contain standard message markup and must be escaped as normal.
							May be multi-line.",
				"short": false // Optional flag indicating whether the `value` is short enough to be displayed side-by-side
							with other values
			}
		]
	}

Here is an example attachment generated from an incoming webhook:

<img src="/img/integrations/incoming_webhook_attachment.v1391019288.png" style="border-radius: 0.5rem; border: 1px solid #DDD;">


## Automatic unfurling

We will automatically fetch and create attachments for certain well-known media urls, but we will not unfurl links
to primarily text-based content, unless you specify in your payload that you want that.
If you do, pass `"unfurl_links": true` when sending your message.

Example links that will unfurl without the flag:

* [http://www.youtube.com/watch?v=wq1R93UMqlk](http://www.youtube.com/watch?v=wq1R93UMqlk)
* [http://www.flickr.com/photos/karstenmay/11787125913/](http://www.flickr.com/photos/karstenmay/11787125913/)
* [https://twitter.com/tweetsoutloud/status/416692366037094400](https://twitter.com/tweetsoutloud/status/416692366037094400)
* [http://imgs.xkcd.com/comics/regex_golf.png](http://imgs.xkcd.com/comics/regex_golf.png)

While these will require the flag on the payload to be unfurled:

* [http://www.cnn.com/2014/01/06/tech/web/ces-unveiled/index.html?hpt=hp_c3](http://www.cnn.com/2014/01/06/tech/web/ces-unveiled/index.html?hpt=hp_c3)
* [https://slack.com/](https://slack.com/)