# Folders

**Folders** are a way to save and organise your [Event Items](./items.md).

Event Items can be [moved](./items.md#move-event-item-to-folder) or [copied](./items.md#copy-event-item-to-folder) from the inbox to a **folder**. Items saved in to a folder will never be deleted by the Cloudview AutoTrash functionality. Storing items into a folder is therefore a way to permanently save them.

## Endpoints

* [List of Folders](#list-folders) - `GET /folder/get_list.[json|xml]`
* [Create Folder](#create-new-folder) - `POST /folder/create.[json|xml]`
* [Rename Folder](#rename-folder) - `POST /folder/rename.[json|xml]`
* [Move Folder](#move-folder) - `POST /folder/move.[json|xml]`
* [Delete Folder](#delete-folder) - `POST /folder/delete.[json|xml]`

********************

## List Folders


Gets a list of *Folder Objects*.

```
GET /item/get_list.[json|xml]
```

### Parameters

* **folder_id** - if specified, gets a list of folders that are children of the folder specified by the ID. Otherwise, gets list of all top level folders.

### Results

An alphabetically sorted list of *Folder Objects*, containing:
 - folder_id
 - name

### HTTP Error Codes

 - *400* if `folder_id` is not a positive integer
 - *403* if folder matching `folder_id` does not belong to user 
 - *404* if no folder found with a matching `folder_id`


## Create New Folder

Create a new folder, either a top level folder or as a sub/child folder of the specified parent.

```
POST /folder/create.[json|xml]
```

### Parameters

* **name** - *required*, the name of the folder to be created
   - string 3..64
* **parent_id** - *required*, if 0, create a top level folder, if > 0 then make the new folder a sub/child of the folder having this ID.
   - int >= 0

### Results

A *Folder Object* containing:
 - folder_id
 - name


### HTTP Error Codes

 - *400* if parameters invalid, including if the specified folder already exists
 - *403* if folder matching `parent_id` does not belong to user 
 - *404* if no folder found with a matching `parent_id`


## Rename Folder

Renames an existing folder.

```
POST /folder/rename.[json|xml]
```

### Parameters

* **folder_id** - *required*, ID of folder to rename
   - int >= 1
* **name** - *required*, the name of the folder to be created
   - string 3..64


### Results

A response indicating a success.

### HTTP Error Codes


 - *400* if parameters invalid, including if the specified name already exists
 - *403* if folder matching `folder_id` does not belong to user 
 - *404* if no folder found with a matching `folder_id`


## Move Folder

Move the folder.

```
POST /folder/move.[json|xml]
```

### Parameters


* **folder_id** - *required*, the ID of the folder to move.
   - int >= 1
* **parent_id** - *required*, the `folder_id` of the new parent folder. If 0, move the folder to the top level
   - int >= 0

### Results

A success response with code `14002`.

### HTTP Error Codes

 - *400* if parameters invalid.
 - *403* if folder matching `folder_id` or `parent_id` does not belong to user 
 - *404* if no folder found with a matching `folder_id` or `parent_id`
 - *409* if the folder is being moved to the same location or as a sub/child folder of itself


## Delete Folder

Permanently delete a folder and all of its contents.

```
POST /folder/delete.[json|xml]
```

### Parameters

* **folder_id** - *required*, the ID of the folder to delete
   - int >= 1


### Results

A success response with code `14100`

### HTTP Error Codes

 - *400* if parameters invalid.
 - *403* if folder matching `folder_id` does not belong to user 
 - *404* if no folder found with a matching `folder_id`


******************

[Back to main page](../README.md)
