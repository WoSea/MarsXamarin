# Challenge 2: Finding Aliens
After finishing Mission 3, we have a camera control that can take pictures.
That picture is then passed into the Microsoft Computer Vision API which can help describe the picture.

Let's try to make the app work with another cognitive service, the Face API.
This API allows us to detect faces in an image, which could be helpful for detecting aliens or extra lifeforms on Mars.

Just like the Computer Vision API has a Nuget to help us interact with it, Face API does as well.

Here's an example tutorial on how to use the Face API in C#:
https://www.microsoft.com/cognitive-services/en-us/face-api/documentation/Tutorials/FaceAPIinCSharpTutorial

Hint: You just need to call the Face API method using the stream from the camera, similar to how the CV API is called.
In this case, I haven't provided an API key, but you can simply use a free API key by signing into your Microsoft account on the Cognitive Services site.

## Finishing requirements
After taking the picture, your application should be able to detect the number of faces in the picture using the Face API
and display an alert with the number of faces.