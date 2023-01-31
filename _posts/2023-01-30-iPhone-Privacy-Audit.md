---
layout: post
title: iPhone Privacy Audit
author: Phillip Kittelson
categories: cybersecurity
tags: audit iPhone iOS cybersecurity privacy
date: 2023-01-30
sharing-tag: Text to include for posts.
image: AppPrivacyReport.PNG
---
This post covers iPhone, however, the features I discuss may be available on popular platforms such as Android.

The integrations available on our mobile devices have, no doubt, enhanced our lives. It is nice to reserve a table at your favorite restaurant using a service like Open Table and have that reservation popup automatically on your calendar. However, when it comes to sharing data on your device with apps, every user should understand what they are being asked to grant access to. Apple has done a relatively good job with making the types of data apps are asking for front and center when you download an app from the Apple App Store, however, I don’t believe most users truly understand what some of this access means.

Users can decline to grant access to data and services (such as Bluetooth) on their device as the install apps from the App Store. This isn’t enough. You should routinely conduct a sort of “privacy audit” on your device, and the types of data these apps have access to. Here are my recommendations:

### Delete unused apps
Even if you religiously grant or deny access to data and services as you download apps, you should review the installed apps on your device often, similar to the process a system administrator might use to remove software and reduce the attack footprint of their system. As vulnerabilities in apps are discovered and made public, not all app developers rush to patch those issues. A good rule of thumb: if you haven’t used the app in more than six months, delete it. On an iPhone, you can delete the app by tapping and holding the icon of the app you want to remove, and selecting the option to remove the app. The best way to remove more than one app is to visit the __iPhone Storage__ section in __Settings__. __iPhone Storage__ gives you a high-level view of the space available on your phone and shows the last used date for each app. __Settings__ > __General__ > __iPhone Storage__.

### Stop downloading apps your phone already has features for
Years ago, many phones lacked features we would consider basic today, such as using the camera flash as a flashlight. Before this functionality was built into the phone’s software, users would have to download apps to take advantage of this loved function. Malware developers took advantage of this and published camera apps which did more than just turn on the flashlight. If your phone already provides a feature you want, shy away from downloading apps to achieve the same goal.

### Review App Permissions
After deleting unused apps, check out the current permissions your apps have been granted. There is hardly any reason a flashlight app should be accessing your GPS location or have access to Bluetooth or network connectivity. The __Privacy & Security__ section in settings lists all the app and data permissions on your phone. __Settings__ > __ Privacy & Security__.

### Get Educated
As an informed user, you should really understand the types of data apps can access and take advantage of. Certainly, there is value in granting access to your Contacts to the Facebook or Instagram apps to find your current friends on these platforms. Is there a good reason either one would need to use the Health Data on your phone? Should a meal prep app have access to the microphone on your phone? I don’t see any beneficial reason for either of these situations. Here is a break down of what data is available on an iPhone:
- **Contacts** provides apps access to the contacts contained on your phone. Social media apps, apps involving scheduling, and meetings are prime candidates for this data source.
- **Location Services** can allow apps to track your location in real time. Navigation apps, apps that tag geolocation in meta data (such as photos) would be apps you’d grand location services to. Location services can be granular:
    - **Never** prevents the app from accessing your geolocation at all
    - **Ask Next Time or when I share** can be used to provide one-time geolocation to an app
    - **While using the app** only allows an app to access geolocation while the app is in use. I only allow Google Maps, and other navigation apps, to access my geolocation while I have the app open.
    - **Always** provides constant access to your location. Apps such as __Find My__, Apple’s native location app, and apps where you share your real-time location to trusted friends or family members, could be granted always access.
- **Calendars** provides access to create and access the calendar items on your phone. Allowing your phone to pull information from the email client to create calendar items is a beneficial feature.
- **Reminders** grants access to apps to create or read the reminders in the Reminders app of your phone.
- **Photos** access allows an app to access photos on your device. Posting a photo to Facebook or Instagram would require this access. Google’s reverse photo search feature would require this access. 
- **Bluetooth** access allows apps to access other devices via the Bluetooth antenna. Connecting a Google Home to your home network is a good example of an app requiring this feature. Ride share apps, such as Lime o Zip Car use Bluetooth to communicate with the scooter or rental car you’re trying to unlock.
- **Local Network** gives apps the ability to establish network connections. A streaming app, such as __NetFlix__ or __Disney+__ needs network access, while an app you use to edit photos probably doesn’t.
- **Microphone** grants apps access to listen and record sound from your phone’s microphone. Recording a video, making a Zoom call are legitimate reasons an app would need to access your microphone. An app which promises to turn your likeness into a giraffe, is not.
- **Speech Recognition** sends recorded voice to Apple to profess requests. While microphone only allows sound recording, determining what you are asking for when you say, “__Hey Siri, when does my nearest Target store close__?” requires this access.
- **Camera** access allows apps to capture photos and video from phones camera.
- **Health** data has been increasingly available on mobile devices, giving us useful integrations and data access to life healthier lifestyles. A pedometer app, or step counter, is a great example. I can’t think of a reason to allow the Starbucks app access to this info.
- **Research Sensor & Usage Data** grants data to sources and sensors which would otherwise be unavailable to an app. An example of this type of access includes health studies and wellness research.
- **HomeKit** is Apple’s smart home service, which can allow you to control lights, temperature, and other connected devices in your home.
- **Media & Apple Music** access allows an app to know what’s in your media library, and the types of music you play.
- **Files and Folders** access allows an app to access the files you have stored locally on your phone. Storing an sharing a PDF document natively on your phone, without using a proprietary app is an example. Sharing that same PDF via iMessage, or email uses this feature.
- **Motion & Fitness** access allows an app to track telemetry on your phone, count steps, or your physical output during exercise.
- **Focus** access allows the newer Focus feature status to be shared with apps. If you’ve ever texted someone and received an automated “I’m driving text” back is an example.

### Get Extra Geeky
If you’re feeling __really__ geeky, or want to have utter control and understanding of the data access, and connections your iPhone has to offer, tap into the __iOS App Privacy Report__. This feature allows you to see the data and sensor access, as well as network connections. For the average user, this is probably overkill. You can turn on the feature and view the report by going to __Settings__ > __Privacy & Security__, then tap __App Privacy Report__, and turn the feature on.
