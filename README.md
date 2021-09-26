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
2)  runtime performance, and 
3) modularity

Netflix uses Amazons Elastic Load Balance (ELB) service to route traffic to our front end services. ELB’s are setup such that load is balanced across zones first, then instances. This is because the ELB is a two tier load balancing scheme.

The second tier of the ELB service is an array of load balancer instances (provisioned directly by AWS), which does round robin load balancing over our own instances that are behind it in the same zone.

ZUUL:

![Screen Shot 2016-11-15 at 12 20 33](https://user-images.githubusercontent.com/81900840/134800265-47edcd9a-c970-43d2-b979-5028c9224887.png)

The Netty handlers on the front and back of the filters are mainly responsible for handling the network protocol, web server, connection management and proxying work. With those inner workings abstracted away, the filters do all of the heavy lifting.

The inbound filters run before proxying the request and can be used for authentication, routing, or decorating the request.

The endpoint filters can either be used to return a static response or proxy the request to the backend service (or origin as we call it).

The outbound filters run after a response has been returned and can be used for things like gzipping, metrics, or adding/removing custom headers.


Features:

1.Supports http2
2.mutual TLS
3.Adaptive retries
4.Concorrency protection for origin


It helps in Easy routing based on query params, url, path. The main use case is for routing traffic to a specific test or staging cluster.


Advantages: ??

1.Authentication and Security: identifying authentication requirements for each resource.

2.Insights and Monitoring: tracking meaningful data and statistics.

3.Dynamic Routing: dynamically routing requests to different backend..

4.Stress Testing: gradually increasing the traffic.

5.Load Shedding: allocating capacity for each type of request and dropping requests.

6.Static Response handling: building some responses directly.

7.Multiregion Resiliency: routing requests across AWS regions.

Hystrix:

![reservation-system-diagram](https://user-images.githubusercontent.com/81900840/134801029-68565c28-88eb-456f-b6b3-5968bae14b9f.png)

Hystrix is a latency and fault tolerance library designed to isolate points of access to remote systems, services and 3rd party libraries. which helps in

Stop cascading failures

Realtime monitoring of configurations changes

Concurrency aware request caching

Automated batching through request collapsing

IE. If a micro service is failing then return the default response and wait until it recovers.


Microservices:

![netflix-microservices-diagram](https://user-images.githubusercontent.com/81900840/134801233-375af8ab-2c24-4035-95f1-e99a626dea39.jpg)

What is Microservices?


Microservice architecture, or simply microservices, is a distinctive method of developing software systems that tries to focus on building single-function modules with well-defined interfaces and operations.


How APIS gets response?

Netflix uses MicroServices architecture to power all of the APIs needed for applications and Webapps. Each API calls the other micro services for required data and then responds with complete response

1.We can use Hysterix which i aready explained

2.We separate critical services

Critical Micro services:

What netflix does is, they identify few service as critical (so that at last user can see recommended hit and play, in case of cascaded service failure) and these micro services works without many dependencies to other services !!

Stateless Services:

One of the major design goals of the Netflix architecture's is stateless services.

These services are designed such that any service instance can serve any request in a timely fashion and so if a server fails it’s not a big deal. In the failure case requests can be routed to another service instance and we can automatically spin up a new node to replace it.

EVCache:

When a node goes down all the cache goes down along with it. so performace hit until all the data is cached. so what netflix did is they came up with EVcache. It is wrapper around Memcached but it is sharded so multiple copies of cache is stored in sharded nodes. So everytime the write happens, all the shards are updated too..

When cache reads happens, read from nearest cache or nodes, but when a node is not available, read from different available node. It handles 30 million request a day and linear scalability with milliseconds latency.

SSDs for Caching:

Storing large amounts of data in volatile memory (RAM) is expensive. Modern disk technologies based on SSD are providing fast access to data but at a much lower cost when ]

compared to RAM. Hence, we wanted to move part of the data out of memory without sacrificing availability or performance. The cost to store 1 TB of data on SSD is much lower
than storing the same amount in RAM.

EC2 MySQL was ultimately the choice for the billing/user info use case, Netflix built MySQL using the InnoDB engine large ec2 instances. They even had master master like setup with “Synchronous replication protocol” was used to enable the write operations on the primary node to be considered completed. Only after both the local and remote writes have been confirmed.

As a result, the loss of a single node is guaranteed to have no data loss. This would impact the write latency, but that was well within the SLAs.

Read replica setup in local, as well as cross region, not only met high availability requirements, but also helped with scalability.

The read traffic from ETL jobs was diverted to the read replica, sparing the primary database from heavy ETL batch processing. In case of the primary MySQL database failure, a failover is performed to the secondary node that was being replicated in synchronous mode. Once secondary node takes over the primary role, the route53 DNS entry for database host is changed to point to the new primary.

Cassandra: -> 500 nodes 50 clusters

https://medium.com/netflix-techb...

Cassandra is a free and open-source distributed wide column store NoSQL database designed to handle large amounts of data across many commodity servers, providing high availability with no single point of failure



















