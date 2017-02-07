# Mars Mission: Xamarin

## Mission Brief
Your crew on Mars has lost contact with Earth and as a result is lacking some essential functions for the mission. Your team has some satellite phones running Android, but the communcation tablets are running Windows.

Your crew has just found an alien bot on Mars that understands English, but we need an interface to interact with the bot. As we need a tool that works across all the team's devices, we will be building an application in Xamarin.

After establishing a connection, We also need to create a tool that can patch our camera feeds into the Computer Vision API, in order to identify unknown objects.

## Prerequisites
Go through this [install document](https://github.com/jamesleeht/MarsXamarin/blob/master/INSTALL.md).

## Starting Point
In this repository there is a blank Xamarin.Forms shared project that has been pre-configured with the right nugets for you.

The main nugets installed in this project are:
- [Bot Connector DirectLine](https://www.nuget.org/packages/Microsoft.Bot.Connector.DirectLine/3.0.0)
- [Rest Client Runtime](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime/)

These nugets allow us to communicate with the bot using pre-defined methods and classes, without the need for manually writing HTTP calls.

Click on the `MarsBuddyBlank` submodule in this repository to download the starting project.  

## Introduction
Xamarin allows you to write your code base once in C#/.NET and have it deployed across the 3 popular mobile platforms, iOS, Android and Windows Phone.

In this Mars Mission guide, we will learn to build a Xamarin Forms app that:

1. Connects to a bot
2. Has an interface that allows you to interact with it
3. Use the Microsoft Computer Vision API with camera images from the app