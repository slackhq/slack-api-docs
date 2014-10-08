## Unfurling

Slack can automatically find URLs in a message and create attachments based on
the content of those URLs. We call this functionality “unfurling”.

When deciding whether to unfurl a link we consider the type of content that
has been linked to. We treat "media" – that is images, tweets, videos, or audio –
differently to pages that are primarily text-content.

Here are some examples of media content:

* [http://www.youtube.com/watch?v=wq1R93UMqlk](http://www.youtube.com/watch?v=wq1R93UMqlk)
* [http://www.flickr.com/photos/karstenmay/11787125913/](http://www.flickr.com/photos/karstenmay/11787125913/)
* [https://twitter.com/tweetsoutloud/status/416692366037094400](https://twitter.com/tweetsoutloud/status/416692366037094400)
* [http://imgs.xkcd.com/comics/regex_golf.png](http://imgs.xkcd.com/comics/regex_golf.png)

While these are examples of text-based content:

* [http://www.cnn.com/2014/01/06/tech/web/ces-unveiled/index.html?hpt=hp_c3](http://www.cnn.com/2014/01/06/tech/web/ces-unveiled/index.html?hpt=hp_c3)
* [https://slack.com/](https://slack.com/)

By default we unfurl all links in any messages posted by users. For messages
posted via webhooks or [the chat.postMessage API method](/methods/chat.postMessage),
we will unfurl links to media, but not other links.

If you'd like to override these defaults on a per-message basis you can pass
`unfurl_links` or `unfurl_media` while posting that message. `unfurl_links`
applies to text based content, `unfurl_media` applies to media based content.
These flags are mutually exclusive, the `unfurl_links` flag has no effect on
media content.

Note that our servers need to fetch every URL in a message in order to
determine what kind of content it references. If you'd like to stop this
from happening, set both `unfurl_links` and `unfurl_media` to false when posting
the message.

## Examples

All of these examples are for incoming webhooks, but similar rules apply to
our other APIS:

    # api.slack.com is text based, so this link will not unfurl:
    {"text": "https://api.slack.com"}

    # passing "unfurl_links: true means the link will unfurl:
    {"text": "https://api.slack.com", "unfurl_links": true}

    # this xkcd link is an image, so the content will be unfurled by default:
    {"text": "http://imgs.xkcd.com/comics/regex_golf.png"}

    # we can disable that using the unfurl_media flag:
    {"text": "http://imgs.xkcd.com/comics/regex_golf.png", "unfurl_media": false}

## Custom Attachments

If you'd like more control over the format of the attachments, you can create
a custom attachment when posting a message to Slack. Our
[attachments documentation](/docs/attachments/) gives more details on the
available options.
