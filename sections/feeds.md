# Moderated Feed APIs

Introduction
----------------

The Mozes moderated Feed APIs are RSS 2.0 compliant web services that provide canned and moderated text to screen, tweet to screen and pics to screen messages for a given campaign.

Two different APIs are provided to retrieve moderated messages – one for Text & Tweet messages and another for Pictures. These APIs can be called via http and allow three parameters to be passed as arguments. The parameters are `campaign_id`, `count` and `format`. The feed type parameter is optional.

The response will always contain the latest messages. Canned messages will be returned along with latest messages if the number of messages available are less than `count`. Note that a maximum of 200 messages can be requested per feed call.

In the case of picture messages, images will be in JPEG format. It is the responsibility of the moderator to properly orient the picture before approving the message to be displayed.

Request URL
----------------

`http://api.mozes.com/feed?campaign_id=<campaignID>&count=<value>&format=json`


Request Paramters
----------------

`campaign_id` ID of campaign to pull user activities from.

`count` *Optional.* Specifies the number messages to return. Minimum `1`, Maximum `200`. Default `200`.

`format` *Optional.* Specifies the format of the feed. Values: `rss` or `json`. Defaults to `rss`.


Example Response
----------------

```xml
<?xml version="1.0"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:mz="http://www.mozes.com/mz">
<channel>
<title>Campaign Messages</title> 
<link>http://api.mozes.com/</link>
<atom:link type="application/rss+xml" href="http://api.mozes.com/feed?campaign_id=123456&amp;format=rss" rel="self"/>
<pubDate>Mon, 18 Jun 2012 16:22:05 -0700</pubDate>
<category>Content Feed</category>
<language>en-us</language>
<description>Content for campaign ID: 123456</description>
<item>
    <description>wassupppp?</description>
    <pubDate>Wed, 23 May 2012 15:35:00 -0700</pubDate>
    <category>text</category>
    <mz:timestamp>1337812500</mz:timestamp>
    <guid isPermaLink="false">com.mozes.message.724786</guid>
</item>
<item>
    <description>Hello World!</description>
    <pubDate>Wed, 23 May 2012 15:35:00 -0700</pubDate>
    <category>text</category>
    <mz:timestamp>1337812500</mz:timestamp>
    <guid isPermaLink="false">com.mozes.live_event_canned_message.7475</guid>
</item>
</channel>
</rss>
```

```json
[
    {
        "created_utc": 1337812500,
        "created_timestamp": "2012-05-23 15:35:00",
        "message_text": "wassupppp?",
        "type": "text",
        "id": "com.mozes.message.724786"
    },
    {
        "created_utc": 1337812500,
        "created_timestamp": "2012-05-23 15:35:00",
        "message_text": "Hello World!",
        "type": "text",
        "id": "com.mozes.live_event_canned_message.7775"
    }
]
```