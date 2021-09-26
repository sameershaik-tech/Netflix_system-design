#NETFLIX SYSTEM_DESIGN
![Netflix-High-Level-System-Architecture](https://user-images.githubusercontent.com/81900840/134771404-c76aea5e-1a48-4084-addd-0df53c5276b9.png)


Netflix operates in two clouds: 

1.AWS 

2.Open Connect.

Both clouds must work together seamlessly to deliver endless hours of customer-pleasing video.

Netflix has 3 main components which we are going to discuss today

1.OC or netflix CDN

2.backend

3.client

Before Deep Dive into the Netflix System Design Lets first talk about some high level working of Netflix and then jump in to these 3 components.

The things which are not responsible for content serving is handled in AWS.

Everything that happens after you hit play is handled by Open Connect. Open Connect is Netflix’s custom global content delivery network (CDN).

Open Connect stores Netflix video in different locations throughout the world. And the content is displayed by the client is coming from near
by open connect locations when you press the play button .

CDN - A content delivery network (CDN) is a system of distributed servers (network) that deliver pages and other Web content to a user or a client, based on the geographic locations of the user, the origin of the webpage and the content delivery server.


How Netflix onboard a movie/video:




Before the movie is made available to users, Netflix will convert the video into a format that works best for your devices. This process is called transcoding or encoding.

Transcoding is the process of converting an audio or video file from one encoding format to another in order to increase the number of compatible target devices a media file can be played on.
![live-transcoding-diagram-detailed-1140x630](https://user-images.githubusercontent.com/81900840/134773394-c5ace687-0eb2-474c-a197-d913598885b7.png)


Whys do we need to do it? why cant we just play the source video?

The original movie/video comes in a high definition format that’s many terabytes in size. Also Netflix supports 2200 different devices. Each device has a video format that looks best on that particular device. If you’re watching Netflix on an iPhone, you’ll see a video that gives you the best viewing experience on the iPhone.

Netflix also creates files optimized for different network speeds. If you’re watching on a fast network, you’ll see higher quality video than you would if you’re watching over a slow network. And also depends on your Netflix plan. that said netflix does create approx 1,200 files for every movie !!!!

Thats a lot of files and processing to do transcoding Now we have all the files we need to stream it.

OC Open connect comes in to picture, OC is Netflix own CDN no thirdparty CDN


![tier-fill](https://user-images.githubusercontent.com/81900840/134799479-497c8cd0-a03c-44a8-9dd1-c28c431eeabb.png)
![0_uVkn1qszk2fH9IjT](https://user-images.githubusercontent.com/81900840/134799490-ba58cecb-7d3a-4b00-8bb5-675a115c1489.jpeg)
![25067243468_6e16c1052a](https://user-images.githubusercontent.com/81900840/134799509-2f811f04-9867-4e60-9076-a1617f055c0e.jpg)


Advantages of OC

1.Less expensive
2.Better quality
3.More Scalable


So once the videos are transcoded these files are pushed to all of the OC servers.

When user loads Netflix app All requests are handled by server in AWS Eg: Login, recommendations, home page, users history, billing, customer support etc. Now you want to watch a video, when you click play button of the Video. Your app automatically figures out the best OC server, best format and best bitrate for you and then the video is streamed from a nearby Open Connect Appliance (OCA) in the Open Connect CDN.

The Netfix apps are so intelligent that they constantly check for best streaming server and bitrate for you and switches between formats and servers to give best viewing experience for you.

Now what netflix does is with all of your search, viewing, location, device, reviews and likes data on AWS it uses Hadoop | Machine learning models to recommend new movies which you might like…

And this cycle goes on and on

Netflix supports 2200 different devices,including smart Tv ,Android,Ios,Gaming consoles and web apps.


Netflix Built using React JS:
![What-is-ReactJS](https://user-images.githubusercontent.com/81900840/134799892-66e8dd6d-bfe2-4f7e-be2d-bbf8a5a83cb2.jpg)

React was influenced by a number of factors, most notably:
1) startup speed, 
2) 2) runtime performance, and 
3) 3) modularity










