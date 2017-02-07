# Mission 2: Making an interface to interact with the bot

## Introduction
In this mission, we will learn how to create a simple Xamarin UI using XAML.

This UI will contain a `ListView` for displaying the messages between the user and the bot, as well as an `Entry` for sending messages to the bot.

We will also learn how to bind data, as well as use the class we made in Mission 1 to work with the bot.

## Default page
In the project, there should be a `MainPage.xaml`. This `.xaml` file represents the first page your application will default to when you start it.

Every `.xaml` file also has a "Code Behind" file which can be used to contain the code and logic for that page. You can see this file by clicking the small arrow next to the `MainPage.xaml` file and clicking on `MainPage.xaml.cs`.

In this tutorial, we will be using both the `.xaml` and `.xaml.cs` files to design the UI and make it work.

## Crafting your UI in XAML
XAML is often used to define the visual contents of an application's page.

XAML allows you to define the elements in an application's page, including it's position, color, text and many other properties.

For example, let's open and look at the default `MainPage.xaml` that we have:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MarsBuddy"
             x:Class="MarsBuddy.MainPage">

	<Label Text="Welcome to Xamarin Forms!" 
           VerticalOptions="Center" 
           HorizontalOptions="Center" />

</ContentPage>
```

This is a simple layout with 1 `Label` saying "Welcome to Xamarin Forms!" that is horizontally and vertically centered in the application.

Of course, we can also change many other properties of the `Label` in XAML, some examples being size and color. That would look something like this:

```xml
<Label Text="Welcome to Xamarin Forms!" 
        TextColor="#77d065" 
        FontSize = "20"
        VerticalOptions="Center" 
        HorizontalOptions="Center" />
```

For our simple chat application, we want to have 2 things:
1. A `ListView` to show the messages in the conversation
2. A `Entry` (text box) which will use to enter text we want to send to the bot

In this scenario, a StackLayout works perfect. A StackLayout allows us to easily position elements in our XAML.