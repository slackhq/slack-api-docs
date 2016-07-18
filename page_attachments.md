# Attachments

It is possible to create more richly-formatted messages using Attachments.

Attachments can be added to messages in different ways:

* For [Incoming Webhooks](https://my.slack.com/services/new/incoming-webhook), send a regular payload, but include an `attachments` array, where each element is a hash containing an attachment.
* For [the Web API](/methods/chat.postMessage), include an `attachments` property, containing a JSON-encoded array of attachment hashes.


## Attachment structure

Messages can have zero or more attachments, defined as an array. Each hash in that array will contain multiple properties:

    {
        "attachments": [
            {
                "fallback": "Required plain-text summary of the attachment.",

                "color": "#36a64f",

                "pretext": "Optional text that appears above the attachment block",

                "author_name": "Bobby Tables",
                "author_link": "http://flickr.com/bobby/",
                "author_icon": "http://flickr.com/icons/bobby.jpg",

                "title": "Slack API Documentation",
                "title_link": "https://api.slack.com/",

                "text": "Optional text that appears within the attachment",

                "fields": [
                    {
                        "title": "Priority",
                        "value": "High",
                        "short": false
                    }
                ],

                "image_url": "http://my-website.com/path/to/image.jpg",
                "thumb_url": "http://example.com/path/to/thumb.png"
            }
        ]
    }

The following parameters can be used to customize the appearance of a message attachment:

###fallback
A plain-text summary of the attachment. This text will be used in clients that don't show formatted text (eg. IRC, mobile notifications) and should not contain any markup.

###color
An optional value that can either be one of `good`, `warning`, `danger`, or any hex color code (eg. `#439FE0`). This value is used to color the border along the left side of the message attachment.

![Screenshot of attachments with colors](/img/api/attachment_color.png)

###pretext
This is optional text that appears above the message attachment block.

![Screenshot of an attachment with pretext](/img/api/attachment_pretext.png)

###author parameters
The **author** parameters will display a small section at the top of a message attachment that can contain the following fields:

* ####author_name
Small text used to display the author's name.

* ####author_link
A valid URL that will hyperlink the `author_name` text mentioned above. Will only work if `author_name` is present.

* ####author_icon
A valid URL that displays a small 16x16px image to the left of the `author_name` text. Will only work if `author_name` is present.

![Screenshot of an attachment with an author image and name](/img/api/attachment_author.png)

###title and title_link
The `title` is displayed as larger, bold text near the top of a message attachment. By passing a valid URL in the `title_link` parameter (optional), the `title` text will be hyperlinked.

![Screenshot of an attachment with a title](/img/api/attachment_title.png)

###text
This is the main text in a message attachment, and can contain standard message markup ([see details below](#message_formatting)). The content will automatically collapse if it contains **700+ characters** or **5+ linebreaks**, and will display a "Show more..." link to expand the content.

![Screenshot of an attachment with a formatted text](/img/api/attachment_text.png)

###fields
Fields are defined as an array, and hashes contained within it will be displayed in a table inside the message attachment.

* ####title
Shown as a bold heading above the `value` text. It cannot contain markup and will be escaped for you.

* ####value
The text value of the field. It may contain standard message markup ([see details below](#message_formatting)) and must be escaped as normal. May be multi-line.

* ####short
An optional flag indicating whether the `value` is short enough to be displayed side-by-side with other values.

![Screenshot of an attachment with some attachment fields](/img/api/attachment_fields.png)

###image_url
A valid URL to an image file that will be displayed inside a message attachment. We currently support the following formats: GIF, JPEG, PNG, and BMP.

Large images will be resized to a maximum width of 400px or a maximum height of 500px, while still maintaining the original aspect ratio.

**Notice:** If `image_url` is supplied `thumb_url` is ignored.

![Screenshot of an attachment with a large image](/img/api/attachment_image.png)

###thumb_url
A valid URL to an image file that will be displayed as a thumbnail on the right side of a message attachment. We currently support the following formats: GIF, JPEG, PNG, and BMP.

The thumbnail's longest dimension will be scaled down to 75px while maintaining the aspect ratio of the image. The filesize of the image must also be less than 500 KB.

**Notice:** If `image_url` is supplied `thumb_url` is ignored.

![Screenshot of an attachment with a thumbnail image](/img/api/attachment_thumb.png)

---

##Putting it all together

Using a combination of the provided message attachment parameters, you can create a variety of message layouts to suit your needs. Here are a few examples of what's possible:

#### Example: Groove

![Screenshot of a groove message](/img/api/attachment_example_groove.png)

    {
        "attachments": [
            {
                "fallback": "New ticket from Andrea Lee - Ticket #1943: Can't rest my password - https://groove.hq/path/to/ticket/1943",
                "pretext": "New ticket from Andrea Lee",
                "title": "Ticket #1943: Can't reset my password",
                "title_link": "https://groove.hq/path/to/ticket/1943",
                "text": "Help! I tried to reset my password but nothing happened!",
                "color": "#7CD197"
            }
        ]
    }

#### Example: Honeybadger

![Screenshot of a honeybadger message](/img/api/attachment_example_honeybadger.png)

    {
        "attachments": [
            {
                "fallback": "ReferenceError - UI is not defined: https://honeybadger.io/path/to/event/",
                "text": "<https://honeybadger.io/path/to/event/|ReferenceError> - UI is not defined",
                "fields": [
                    {
                        "title": "Project",
                        "value": "Awesome Project",
                        "short": true
                    },
                    {
                        "title": "Environment",
                        "value": "production",
                        "short": true
                    }
                ],
                "color": "#F35A00"
            }
        ]
    }

#### Example: Datadog

![Screenshot of a datadog message](/img/api/attachment_example_datadog.png)

    {
        "attachments": [
            {
                "fallback": "Network traffic (kb/s): How does this look? @slack-ops - Sent by Julie Dodd - https://datadog.com/path/to/event",
                "title": "Network traffic (kb/s)",
                "title_link": "https://datadog.com/path/to/event",
                "text": "How does this look? @slack-ops - Sent by Julie Dodd",
                "image_url": "https://datadoghq.com/snapshot/path/to/snapshot.png",
                "color": "#764FA5"
            }
        ]
    }

---

## Automatic unfurling

Slack can also automatically create attachments based on the contents of URLs
in the message. Our [unfurling documentation](/docs/unfurling/) gives more
details on this functionality and how you can control it.

## Message Formatting

Slack messages may be formatted using Slack's standard message markup, a simple markup language similar to [Markdown](https://daringfireball.net/projects/markdown/). **[Learn how to format messages.](/docs/formatting)**
