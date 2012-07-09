# Web Hooks

## Introduction

Webhooks allow your application to be notified when specific events happen within Mozes. Currently, only the Data Collection hook has been implemented. 

All webhook payloads will contain three pieces of information:

`event` A slug defining which event fired this callback.

`fired_at` A timestamp of when the event was fired.

`data` A key/value hash containing the applicable information for the event.

## Setup

At this time, you can contact support via the [support center](http://support.mozes.com) to have a callback url added to your Mozes Connect account.

## Data Collection / Data Capture

The data collection payload contains the full hierarchy of account/project/campaign information as well as the user's ID. If the user interacted via SMS, his phone number will also be included. The `item_key` field will contain the slug defining what type of data was collected. The `item_value` will contain the data that the user submitted.

Commonly used `item_key` values are `email` and `dob`. In some cases, customized types my be used such as `name`, `zip_code` or even `favorite_color`. If your application only cares about email, you can filter out events based on this value.

### Example email address payload:

```json
{
    "event": "data_capture",
    "fired_at": "2012:05:16 23:10:35",
    "data": {
        "project_id": "74901",
        "user_id": "389952",
        "item_key": "email",
        "item_value": "user@domain.net",
        "campaign_id": "123456",
        "campaign_run_id": "62823",
        "channel_id": "236495"
        "account_id": "181198",
        "phone": "6305551073"
    }
}
```

### Example date of birth payload:

```json
{
    "event": "data_capture",
    "fired_at": "2012:05:16 23:10:35",
    "data": {
        "project_id": "74901",
        "user_id": "389952",
        "item_key": "dob",
        "item_value": "20120528",
        "campaign_id": "123456",
        "campaign_run_id": "62823",
        "channel_id": "236495"
        "account_id": "181198",
        "phone": "6305551073"
    }
}
```
