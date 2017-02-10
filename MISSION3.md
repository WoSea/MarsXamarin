# Mission 3: Using camera images to work with the Computer Vision API
Great! Now we have an application that can communicate with the MarsBot we found.
Next, we want to be able to scan objects on Mars and have the computer be able to identify them.

## Introduction
In this mission, we will implement a camera control in our application and send the taken photo to the [Microsoft Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api).
The CV API is part of the Microsoft Cognitive Services, a set of easy-to-use APIs which expose artificial intelligence and machine learning. The CV API allows us to detect what's in an image.

Although the CV API is a web service which requires HTTP requests and responses to work, it has a .NET library which will allow us photo
simply call methods within our application. This means that we won't need to manually structure our HTTP requests and handle JSON files.

There are 2 steps to this mission:

1. Implement a camera function
2. Send the captured image to the Computer Vision API and get a result


## Setup

### Nugets needed
There are 2 Nugets which we want to install in our project:

1. Xamarin Media Plugin
  * For camera controls
2. Computer Vision Client library
  * To work with the Computer Vision API

### Installation steps

1. Right-click on the solution and click "Manage NuGet packages for solution".
2. Click on the "Browse" tab
3. Search for `Xam.Plugin.Media`
4. Tick all the boxes on the right for the 3 platforms
5. Click install

Repeat the above steps and install `Microsoft.ProjectOxford.Vision` as well.


