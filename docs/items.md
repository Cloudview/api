# Event Items

**Event Items** are the real "meat" of the Cloudview system. They are the actual recorded events uploaded by the [cameras](./cameras.md). Within the UI, the inbox contains the list of  **event items**.

An **event item** consist of a number of frames, some meta data such as the date and time the event was uploaded, if it is an alerted event as well as any user specified data, such as flags or notes.

An **event item** only ever belongs to one camera.

## Endpoints

* [List of Items](#list-event-items) - `GET /item/get_list.[json|xml]`
* [Item Details](#event-item-details) - `GET /item/details.[json|xml]`
* [List Frames](#get-list-of-frames) - `GET /item/frames.[json|xml]`
* [Get Total Alerted Items](#get-total-alerted-event-items) - `GET /item/alerts_count.[json|xml]`
* [Get Download URLs](#get-downloadable-versions-of-the-event-item) - `GET /item/get_video_urls.[json|xml]`
* [Get Share URLS](#get-public-share-url) `GET /item/get_share_url.[json|xml]`
* [Update Item](#update-event-item) `POST /item/update.[json|xml]`
* [Flag Item](#flag-event-item) `POST /item/flag.[json|xml]`
* [Move to Folder](#move-event-item-to-folder) `POST /item/move.[json|xml]`
* [Copy to Folder](#copy-event-item-to-folder) `POST /item/copy.[json|xml]`
* [Save Snapshot](#save-snapshot-from-event-item) `POST /item/save_snapshot.[json|xml]`
* [Delete Item](#delete-event-item) - `POST /item/delete.[json|xml]`

**********


## List Event Items

Gets a list of Inbox *Item Objects*. This is the API equivalent of viewing your inbox.

``` 
GET /item/get_list.[json|xml]
```

### Parameters

* **page** - which "page" of results you wish to view
   - default = 1
* **qty** - how many results per "page" are to be returned
   - integer >=1 <= 20
   - default = 10
* **alert** - restrict the results to listing only alerted or non-alerted event items
    - TRUE = return *only* alert event items
    - FALSE = return *no* alerted event items
    - Not specified = return all items regardless if they are alerted or not
* **camera_id** - if the camera ID is supplied, only return event items for the specified camera
* **datetime** - the date time boundary for the result listings. This works in conjunction with **datetime_reverse**
    - format: "yyyy-mm-dd hh:mm:ss"
    - if a **datetime** parameter is passed, it gets all items *older* than the specified **datetime**.
* **datetime_reverse** - boolean 
    - If **datetime_reverse** is passed, it gets all items *newer* thank the specified **datetime**. 
* **flag** - similar to the alerts, restrict the results to listing only flagged or non-flagged event items
    - TRUE = return *only* flagged event items
    - FALSE = return *no* flagged event items
    - Not specified = return all items regardless if they are flagged or not
* **new** - restrict the results to listing only viewed or unviewed (*new*) items
    - TRUE = return *only* new event items
    - FALSE = return *no* new event items
    - Not specified = return all items regardless if they are viewed or not

### Results

A list of *Item Objects#* containing:
 - item_id
 - camera_id
 - label [camera public label]
 - start_datetime
 - thumnail_url
 - thumbnail_urls [array of different resolutions]
 - is_snapshot [always FALSE]
 - is_new [bool]
 - is_owner [bool]
 - is_alert [bool]
 - flag

### HTTP Error Codes

 - *400* if parameters invalid

## Event Item Details

Gets extended details of a specific *Item Object*.

```
GET /item/details.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item

### Results

An `Item Object`, containing:
 - item_id
 - camera_id
 - label
 - start_datetime
 - thumnail_url
 - thumbnail_urls [array of different resolutions]
 - is_snapshot
 - is_new
 - note [note description]
 - folder_id [-1 > n ]
 - flag
 - shared [inc. sent]
 - end_datetime

### Errors

 - *400* if item_id is not a positive integer.
 - *404* if the item id does not exist.
 - *403* if the user does not have permsission to view this clip (owner or network)



## Get List of Frames

Get the list of images that comprise the Event Item.

```
GET /item/frames.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item

### Result

And `Item Object`, containing:
 - item_id
 - camera_id
 - label (public if current user is not the owner of the camera)
 - list of `Image Objects`
    * identifier
    * URL
    * datetime `yyyy-mm-dd hh:mm:ss`
    * milliseconds (depending on camera manufacturer, may be empty) 


### Errors

 - *400* if item_id is not a positive integer.
 - *404* if the item id does not exist.
 - *403* if the user does not have permsission to view this clip (owner or network)


## Get Total Alerted Event Items

> **Note:** This command will become deprecated in later versions of the API

Counts the number of alerted event items.


```
GET /item/alerts_count.[json|xml]
```

###  Parameters

* **camera_id** - if specified, only count the alerted event items for the specified camera

### Results

`item_count` with for number of alerted event items.


### HTTP Error Codes

 - *400* if parameters invalid
 - *404* if item object doesn't exist


## Get downloadable versions of the Event Item

Gets a list of `Video URLs`.

```
GET /item/get_video_urls.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item

### Results

A list of `Video URLs`
 - resolution
 - URL to video

### Errors

 - *400* if parameters invalid
 - *403* if user does not have permission to encode video from item.
 - *404* if item object doesn't exist

## Get Public Share URL

Generates a shared version of the specified Event Item and returns the URL of its publicly accessible page.

```
GET /item/get_share_url.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item

### Results

A URL to the publicly accessible page for the specified event item,

### HTTP Error Codes

 - *400* if parameters invalid
 - *403* if user does not have permission to share item
 - *404* if item object doesn't exist



## Update Event Item


### Parameters

* **item_id** - *required*, the ID of the event item
* **label** - the label for the event item (defaults to label of camera)
   - string 0..64
* **note** - the note associated with the specified event item
   - string 0..1024


### Results

A response indicating success (even if the record is not altered).

### HTTP Error Codes

 - *400* if parameters invalid
 - *403* if user does not have permission to share item
 - *404* if item object doesn't exist



## Flag Event Item

Sets the flag for specified *Item Object*.

```
POST /item/set_flag.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item
* **flagged** - *required*, bool
   - 1 = set item to flagged
   - 0 = set item to not flagged

### Results

Jabbakam Success code `13001`

### HTTP Error Codes

 - *400* if parameters invalid
 - *403* if user does not have permission to change flag value
 - *404* if item object doesn't exist

### Cloudview Custom Error Codes

 - *3000* Item not found
 - *3001* User does not have permission to view this item


## Move Event Item to Folder

Moves the specified *Item Object* to a folder.

```
POST /item/move.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item
* **folder_id** - *required*, the ID of the destination folder

### Results

 - Success code `13002` - item moved

### Errors

 - *400* if parameters invalid
 - *403* if user is not the owner of either the event item or folder 
 - *404* if item object doesn't exist or the folder does not exist
 - *409* the destination folder is the same as the folder the event is currently in

## Copy Event Item to Folder

Copies the specified *Item Object* to a folder.

```
POST /item/copy.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item
* **folder_id** - *required*, the ID of the destination folder

### Results

 - Success code `13003` - item copied (even if a copy already exists)

### Errors

 - *400* if parameters invalid
 - *403* if user is not the owner of either the event item or folder 
 - *404* if item object doesn't exist or the folder does not exist
 - *409* the destination folder is the same as the folder the event is currently in


## Save Snapshot from Event Item

Save a particular frame of specified event item to a folder.

```
POST /item/save_snapshot/[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item
* **folder_id** - *required*, the ID of the destination folder
* **identifier** - *required*, the filename identifier for the frame to save as a snapshot
   - string 27..64

### Results

 - Success code `13200` - snapshot created.
 - **item_id** - ID of the new snapshot item created within the folder
 
*Note*: If the same snapshot is already saved to the destination folder then success is still returned, but no new snapshot is created. The **item_id** returned is that of the existing snapshot item.

### Errors

 - *400* if item_id is not a positive integer, identifier doesn't match the item_id, folder is not a positive integer
 - *403* if user is not the owner of either the event item or folder
 - *404* if item object doesn't exist or the folder does not exist
 - *409* if the item_id refers to a snapshot item, not an event item


## Delete Event Item

Deletes the specified *Item Object*.

```
POST /item/delete.[json|xml]
```

### Parameters

* **item_id** - *required*, the ID of the event item

### Results

 - Success code `13100` - item deleted
 - Success code `13101` - item moved to trash

### Errors

 - *400* if parameters invalid
 - *403* if user does not have permission to delete the item object
 - *404* if item object doesn't exist


******************

[Back to main page](../README.md)
