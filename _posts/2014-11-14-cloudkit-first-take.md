---
layout: post
title: 'CloudKit First Take'
date: 2014-11-14 02:59
comments: true
categories: 
---
#CloudKit First Take
![CloudKit Background.JPG](http://user-image.logdown.io/user/1137/blog/1121/post/242633/p8TfxYVSRqO3KIGXW1Xr_CloudKit%20Background.JPG)

---

# 撒景賢
# james sa
# Speed 3D Inc.
# 3D拍拍
# @JAMEX

---

# The problem

The problem I want to solve is in our app (3DPIPO), we have right now 500MB+ 3D model assets. One 3D model takes from 5MB to 10MB based on the texture and resolution of the model.

Each Model is around 5~10MB.

---

# In first version

## Cache is good
^ We put everything in cache to make review happy. After that we managed a fallback model to store these assets.

^ As models become more and more, it becomes infeasible to use IAP to download the assets which will take up a lot of phone space and use only once. 3DPIPO will easily boost to 200MB after downloading multiple packs.

^ Therefore, I begin to revamp the underling service and looking for solution. The first paradigm is to maintain a catalog file containing all downloadable models along with their URI. By leveraging NSURLSession's default caching mechanism, this can be done easily.

^ With one catch, I have to build up my own assets management server which needs minimal security level and others.

^ When solving a problem, one should try a lot of solutions and look for the highest solutions or choose the right abstration of the problem.

---

# The Podcast
## Everyone needs some motiviation.

After hearing Ray Wanderlich's podcast, I tried CloudKit this morning using defaut sample. As version 2.0 (2014-0-13) 

https://developer.apple.com/library/prerelease/ios/samplecode/CloudAtlas/Introduction/Intro.html#//apple_ref/doc/uid/TP40014599

---

# The Setup

I can set up with only a few catch like creating application specific Record Type like `ReferenceItems` and `ReferenceSubitems`. Looks like other Record Type are created automatically but not these two.

ReferenceItems has attribute name as String
ReferenceSubitem has attribute  parent as Reference, and name as String

---

# The Catch

For Photos and Users record types, you have to create a bogy attribute to make the queriable in PUBLIC DATA.

---

# The result

In the end my [iCloud dashboard](https://icloud.developer.apple.com/dashboard/#iCloud.co.spe3d.CloudKitAtlas) looks like 

Items (2 attributes, location as Location, and name as String)
Photos (2 attributes, photo as Asset, bogy as Queriable)
User (1 attributes, boggy as Queriable)

Now you can head to User Records and Default Zone in PUBLIC DATA

The rest of the problem is data versioning.

---

![CloudKit Photos.png](http://user-image.logdown.io/user/1137/blog/1121/post/242633/7Dc7OjtaR86993uCQARJ_CloudKit%20Photos.png)

![CloudKit Users.png](http://user-image.logdown.io/user/1137/blog/1121/post/242633/UMDTR0z2TDGPKUQT52Pb_CloudKit%20Users.png)

---

# Tips for Defining Your App's Record Types

^ When defining your app’s record types, it helps to understand how you use those record types in your app. Here are some tips to help you make better choices during the design process:

-  Organize your records around a central record type. 
 
^ A good organization strategy is to define one primary record type and additional record types to support the primary type. Using this type of organization lets you focus your queries on your primary record type and then fetch any supporting objects as needed. If you define too many primary record types, your app’s interface may require more complexity to select or search for relevant records. For example, a calendar app might define a single calendar record (the primary record type) that contains multiple event records (a secondary record type) corresponding to events on that calendar. 
 
- Use references to create strong relationships between records. 
 
^ Although you can store the ID of a record or asset in a field using an NSString object, doing so is not recommended. Instead, use a CKReferenceobject to establish a formal relationship between the two objects. References also let you establish an ownership model between objects that can make deleting those records easier.

- Include version information in your records. 

^ A version number can help you decide at runtime what information might be available in a given record.

-  Handle missing keys gracefully in your code.

^ For each record you create, you are not required to provide values for all keys contained in the record type. For any keys you do not specify, the corresponding value is nil. Your app should be able to handle keys with nil values in an appropriate way. Being able to handle missing keys becomes important when new versions of your app access records created by an older version. 
 
- Avoid complex graphs of records.
 
^ Creating a complex set of relationships between records creates the potential for problems later when you need to update or delete records. If the owner relationships among your records are complex, it might be difficult to delete records later without leaving other records in an inconsistent state. 
 
- Use assets for discrete data files. 

^ When you want to associate images or other discrete files with a record, use a CKAsset object to do so. The total size of a record’s data is limited to 1 MB though assets do not count against that limit. 

---

#Con
##iOS8 only
##No Serverside scripting

#Pro
it's just a beginning

---

# Reference

[Designing for CloudKit](https://developer.apple.com/library/ios/documentation/General/Conceptual/iCloudDesignGuide/DesigningforCloudKit/DesigningforCloudKit.html#//apple_ref/doc/uid/TP40012094-CH9-SW1)

[The problem now is the Data Transfer quota. The 25MB/day for assets worries me.](https://developer.apple.com/icloud/documentation/cloudkit-storage/)

[Ray Wenderlich's Beginning CloudKit](http://www.raywenderlich.com/83116/beginning-cloudkit-tutorial)

[CKAssets](https://developer.apple.com/library/ios/documentation/CloudKit/Reference/CKAsset_class/index.html#//apple_ref/occ/cl/CKAsset)

## Sample Code

[Cloud Captions](https://developer.apple.com/library/ios/samplecode/CloudCaptions/Introduction/Intro.html#//apple_ref/doc/uid/TP40014732-Intro-DontLinkElementID_2)

[WWDC Party based on CloudKit](https://github.com/sugarso/WWDC)

---

# One More Thing
We are recruting :)