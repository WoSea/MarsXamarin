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
It allows you to define the page's elements, including it's position, color, text and many other properties.

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

In this scenario, a `StackLayout` works perfect. A `StackLayout` allows us to easily position elements in our XAML, setting horizontal and vertical properties.

Let's define a `StackLayout` element: 

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
</StackLayout>
```

This `StackLayout` fills the whole page, with some padding on the edges. It also defines a spacing of 10 between the elements in a vertical order.

A `StackLayout` is useless without elements in it. Let's add in `ListView` and `Entry` elements into the `StackLayout`.

```xml
<StackLayout Spacing="10" Padding="10" HorizontalOptions="Fill" VerticalOptions="Fill" Orientation="Vertical">
        <ListView x:Name="MessageListView"
                        VerticalOptions="StartAndExpand"
                        HorizontalOptions="Fill"
                        >
        </ListView>
    
        <Entry Placeholder="Message"
                VerticalOptions="End"
                HorizontalOptions="Fill"
                HorizontalTextAlignment="End"
                />
</StackLayout>
```

In this `StackLayout`, we've added a `ListView` and `Entry`. It's important for us to also define the `VerticalOptions` and `HorizontalOptions` properties of the elements
so that the elements know how to be positioned within the `StackLayout`.

The `ListView` in it's current state won't be able to work properly though. Remember that we define the visual properties of elements within our XAML, but
a `ListView` is special in the sense that it has its own elements as well. When the list is populated, it will have its own rows/cells.

Currently, our `ListView` doesn't know how it should display these cells. Luckily, it's fairly simple to define how these cells should be displayed.

In this snippet, we use a simple `TextCell`, which is a pre-defined cell type provided by Xamarin. It's a simple cell that has Text and Detail properties.

```xml
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
```

## Data binding
### Introduction
Often times, UI isn't static. It is dynamic and needs to display data accordingly.

For example, if we wanted to populate a `ListView`, we can't just hardcode data in. That makes the list pretty useless.
What you would do instead, is to retrieve data from a database or service and display it on the list.

But then comes another problem. Data changes all the time and updates can be made to the data. If the data is updated,
we will need to manually update the displayed list as well, which means you have to write more code.

As developers, we want a easier way to do this and that's where data binding comes in.
Data binding allows you to establish a contract bewteen the data and the display.

### ListView Binding
In our case, the `ListView` will be used to display messages to and from the bot. We will use an `ObservableCollection`, which is a special collection type that can be binded to a `ListView`.

Previously in Mission 1, we created a `MessageListItem` class that we will be able to use here.

Let's open `MainPage.xaml.cs` and make a new `ObservableCollection` that takes in the type `MessageListItem`.

```cs
ObservableCollection<MessageListItem> messageList = new ObservableCollection<MessageListItem>();
```

Previously, in our XAML, we gave the `ListView` a name of "MessageListView". Assigning a name to the element in XAML allows us to access it as a variable
in the code-behind file of the XAML. We can call the variable in our `.xaml.cs` file.

Let's use that to bind our newly created `ObservableCollection` to the `ListView`.

We can do this in the constructor of the MainPage.

```cs
//ObservableCollection to store the messages to be displayed
ObservableCollection<MessageListItem> messageList = new ObservableCollection<MessageListItem>();

public MainPage()
{
    InitializeComponent();

        //Bind the ListView to the ObservableCollection
        MessageListView.ItemsSource = messageList;
}
```
Now that's done! Any new additions to the `messageList` collection will magically reflect on the UI in the `MessageListView`.

### Input events
We also have a entry box that allows the user to enter messages.