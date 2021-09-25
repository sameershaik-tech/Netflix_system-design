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

Open Connect stores Netflix video in different locations throughout the world. And the content is displayed by the client is coming from near by

open connect locations when you press the play button .




