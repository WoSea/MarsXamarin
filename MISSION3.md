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

![step1](https://raw.githubusercontent.com/jamesleeht/MarsXamarin/master/Images/solutionnugets.png)

1. Right-click on the solution and click "Manage NuGet packages for solution".
2. Click on the "Browse" tab
3. Search for `Xam.Plugin.Media`
4. Tick all the boxes on the right for the 3 platforms
5. Click install

Repeat the above steps and install `Microsoft.ProjectOxford.Vision` as well.

## Implementing the camera
Xamarin.Forms doesn't natively provide the ability to access camera APIs, 
but the `Xam.Plugin.Media` plugin helps us to access the camera APIs on each native platform in shared code.

In this lab, we will be testing the application in UWP, since only the UWP application runs on your computer natively and will be able to access your webcam.

As a result, we need to enable the webcam permission on the UWP project. Open `Package.appxmanifest` in your UWP project.

We want to make it so that the camera opens on a button click. Let's first define a button in our `MainPage.xaml`
below the `Entry` box.

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
        <ListView x:Name="MessageListView"
                        VerticalOptions="StartAndExpand"
                        HorizontalOptions="Fill"
                        >
            <ListView.ItemTemplate>
              <DataTemplate>
                <TextCell Text="{Binding Text}" Detail="{Binding Sender}" />
              </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    
        <Entry Placeholder="Message"
                VerticalOptions="End"
                HorizontalOptions="Fill"
                HorizontalTextAlignment="End"
                />

        <Button Text="Take Picture"
          VerticalOptions="End"
          HorizontalOptions="Fill"
          Clicked="TakePic"
          />
</StackLayout>
```

In the XAML, we defined that when we click the button, we should execute the `TakePic()` method.