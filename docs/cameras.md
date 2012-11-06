# Cameras

The **camera** objects of the API relate to the physic cameras that do the uploading of [Event Items](./items.md). The **camera** objects within the API contain the location information about the cameras (address and geo-positioning) and some meta data, such as if the camera is set to record events, if the camera should send alerts etc.

The **cameras** object within this section of the API only refer to cameras that are owned by the current user.

## Endpoints

* [List of Cameras](#list-of-users-cameras) - `GET /camera/get_list.[json|xml]`
* [Camera Details](#get-camera-details) - `GET /camera/details.[json|xml]`
* [Search for Cameras](#search-for-cameras) - `GET /camera/search.[json|xml]`
* [Liveview](#get-liveview-urls) - `GET /camera/liveview.[json|xml]`
* [Update Camera](#update-camera-details) - `GET /camera/update.[json|xml]`


****************

## List of User's Cameras

Get a list of `Camera Objects`.

```
GET /camera/get_list.[json|xml]
```

### Parameters

* **sort** - order in which to sort the results
    - a-z = sort alphabetically.
    - 0-9 = sort by user defined order *default*
    - Note: The *user defined order* relates to the order of the cameras as dictated by the main camera page in the website.

### Results

A list of `Camera Objects` containing:
 - camera id
 - label
 - latitude
 - longitude
 - record_video [bool]
 - is_hidden [bool]
 - is_owner [always TRUE]
 - alerts_count

Note: is_owner is a legacy value and is always listed as true when retriving your camera list.


## Get Camera Details

Get details for a specific camera

```
GET /camera/details.[xml|json]
```

### Parameters

* **camera_id** - *required* ID of camera


### Results

A `Camera Object` containing:
 - camera id
 - label
 - public_label
 - description
 - address1
 - address2
 - address3
 - county
 - country
 - postcode
 - latitude
 - longitude
 - alerts [bool]
 - record_video [bool]
 - is_hidden [bool]
 - is_owner [always TRUE]


### HTTP Error Codes

 - *400* if camera_id if not an integer or less than 1.
 - *403* If the camera does not belong to the user.
 - *404* If the camera does not exist.

## Search for Cameras

Get a list of `Camera Objects` based on the specified filters


```
GET /camera/search.[xml|json]
```

### Parameters


* **keyword** - *required* string to search cameras by

### Result

A list of `Camera Objects` containing:
 - camera id
 - label
 - latitude
 - longitude
 - record_video [bool]
 - is_hidden [bool]
 - is_owner [always TRUE]
 - alerts_count


### HTTP Error Codes

 - *400* if no keywords are given

## Get Liveview URLs

Returns an array of URLS for the Camera's Live View stream. Each URL is a different format of stream.

```
GET /camera/liveview.[xml|json]
```

### Parameters

* **camera_id** - *required* ID of camera

### Result

An array or URL strings for different formats of the Live View stream.

### HTTP Error Codes

 - *400* if camera_id is not a positive integer.
 - *404* if the camera does not exist.
 - *500* if the camera's live view is not connected.
 - *403* if the user is not the owner of the camera.
 - *409* if the camera is not live view capable

### Cloudview Custom Error Codes

 - 2000 Camera not found
 - 2001 Not owner of the camera
 - 2002 Live View not available for the camera
 - 2003 Live View is not connected

## Update Camera Details

Updates the camera details, including record state and alert state.

```
POST /camera/update.[xml|json]
```

### Parameters


* **camera_id** - *required* ID of the camera
* **label** - Private label for the camera (only the owner can see this label)
   - string 0..100
* **public_label** - Public label for the camera (network and other users see this label)
   - string 0..100
* **description** - Description of the camera
   - string 0..512 
* **address1** - First line of the address the camera is located at
   - string 0..100
* **address2** - Second line of the address the camera is located at
   - string 0..100
* **address3** - Third line of the address the camera is located at
   - string 0..100
* **county** - County the camera is located in
   - string 0..50
* **postcode** - Postcode of the camera's location
   - string 0..20
* **country** - Country the camera is located in
   - string 0..100
* **latitude** - Latitude of the camera's location
* **longitude** - Longitude of the camera's location
* **alerts** - Turn alerts on or off
   - bool 0 or 1
   - Note: If `record_video` is set to 0 and `alerts` is set to 1, you will never receive alerts as no events will be uploaded.
* **record_video** - Turn the record events function on/off (i.e. turn the camera on or off)
   - bool 0 or 1
   - Note: If `record_video` is set to 0 and `alerts` is set to 1, you will never receive alerts as no events will be uploaded.
* **is_hidden** - Stop the camera appearing on the public map. 
   - bool 0 or 1
   - Note: Even if your camera is "hidden", it will still appear on the maps of any networks it is a member of.

### Result

A response indicating success (if even if the record is not altered) with success code  `12000`

### HTTP Error Codes

 - *400* if camera_id is not a positive integer.
 - *404* if the camera does not exist.
 - *403* if the user is not the owner of the camera.



******************

[Back to main page](../README.md)
