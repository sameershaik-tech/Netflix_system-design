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





