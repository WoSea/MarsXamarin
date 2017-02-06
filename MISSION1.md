# Mission 1: Connecting a bot to Xamarin

## Introduction
In this mission, we will be connecting to a bot built in NodeJS and the Microsoft Bot Framework. Bots built using the Microsoft Bot Framework have a Direct Line channel.
This channel is essentially a REST API that allows us to interact with the bot using HTTP requests and responses.

Although it is possible to setup your own classes and models for accessing the REST API, it can be troublesome. Luckily, there is a Nuget package published by Microsoft
for use with .NET projects which helps us abstract the REST API calls.

## Setup
Let's first start by creating a new Xamarin project in Visual Studio. In this case, we will use a Shared project. We will need to install all the relevant nugets.

## Connecting the bot
Our application needs to communicate with the bot in 2 ways: Sending and receiving messages. As a result, we will need to use methods to send messages to the bot as well as constantly receive messages from the bot.

The DirectLine nuget we installed will allow us to more easily implement this within our application without having to write any HTTP calls manually. Let's make a new class where we will contain and abstract all the connection-related code.

Right click on the main project and go to Add > New Item > Class and name it `BotConnection.cs`.

Let's add a few things to our new blank class.