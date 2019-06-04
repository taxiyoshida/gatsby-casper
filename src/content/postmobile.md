---
layout: post
title: 2019 Prediction Post-mobile, Edge Strikes Back (2)
image: img/wearables-use-case-3.jpg
author: Ghost
date: "2018-09-30T07:03:47.149Z"
tags: 
  - Tests
---

# 3. Future is Edge

Computing continued to be pendulum of concentration and dispersion. Experiencing concentration of mainframe computers, and distribution through client servers, rise of mobile cause cloud concentration over the past 10 years. In recent years the Internet has concentrated on the cloud operated by Tech Giant. Majority of mobile applications are built on the cloud and data is being served from data center to your device. There are various types of cloud computing, but large-scale operators are limited to Amazon, Microsoft and Google.

In IoT, a large amount of sensors are connected to the network. The sensor creates a lot of data, but when all sensors send data to the cloud, the network is punctured. Most of the sensor data is unstructured data and the value density is low. Economic advantages of utilizing the cloud are also thin. Therefore, edge computing, which processes data in the close proximity of the data source itself, is regarded as important.

In a blog about object detection that runs DNN in Intel's FPGA, it is cited as a reason why edge platform is necessary. Intel is a supplier of FPGA to Microsoft. [(”High-throughput Object Detection on Edge Platforms with FPGA”)](https://ai.intel.com/high-throughput-object-detection-on-edge-platforms-with-fpga/)

- Slow or unreliable connectivity to cloud: certain situations require real-time analysis and corresponding responses to sensor data. Having a slow or unreliable network connectivity would severely impede proper functionality of such systems.

- Too much data is collected: even in situations that may not need strict real-time responses, sending huge quantities of data to the cloud may be impractical or too expensive. For example, a system of surveillance cameras could collect a huge amount of raw image frames. Expecting to pump all of this data to the cloud could be impractical or wasteful if only a few of these frames would have any objects of interest.

- Privacy and security of customer data: certain data collected might be highly secretive and its confidentiality would be essential to the customer’s business. In such cases, being able to avoid transmission of any such data over the internet would greatly decrease the attack surface thereby providing better security.

Machine learning freed the power of the edge. The embedded computer performs data processing (inference) on the spot. Cloud will play a stronger role as a place of training. Tesla is  good example. Automobiles with high-performance computing capabilities complete sensing, reasoning, decision-making, and action on the spot.

Number of sensors increases exponentially, and it will exist  everywhere (ubiquitous). The quality of sensing is improving. IDC [predicts](https://www.emc.com/leadership/digital-universe/2014iview/executive-summary.htm) that total amount of data generated from connected devices will exceed 40 trillion gigabytes by 2025.  Total amount of sensor data completely exceeds capabilities of the cloud.

Edge computing can also be described as a "data center mesh network" that processes or stores important data locally and pushes the processed data to a cloud storage repository covering an area of 100 square meters.

Edge computing has compatibility with next-generation 5G cellular network. When a communication provider incorporates 5G in wireless network, it is expected that towers for 5G will increased separately from the base station. Many of micro data centers will be added at towers. Vendors will be able to own or borrow space within tower and put their own micro data center capability (collocation). They can do edge computing: directly access the gateway to the carrier's extensive network, or connect to the public cloud. Public cloud providers such as Microsoft and Google will also try to increase number of micro data centers outside their own large scale data center and approach the edge to accommodate growing number of IoT devices.

There are unresolved security issues in IoT. Due to the explosive expansion of the nodes, attack targets increases drastically, resulting in countless vulnerabilities in the network. Physical security issues can be managed centrally in one place, but the more distributed computing is, the more cost of security will increase. Also, it is essential that edge devices share data and take autonomous and cooperative behavior without any latency.

The edge computing economy is gradually being secured. Due to the evolution of machine learning chips and networks, the cost of edge computing is considered to drop rapidly in near future. From the TPU that emphasizes the power cost, we can predict prospect of making edge computing cheaper and making it like something like "water" or "electricity".
 
# 3.1 5G

The 5 G use case to be introduced in Japan, Korea, China and America around 2020,  is roughly classified into three main types of services.

- Enhanced Mobile Broadband: 5G not only improves smartphones but also leads new immersive experiences such as VR and AR with a faster uniform data rate, or lower latency and cost per bit
- Ultra-reliable communication: 5G enables new services that can transform the industry with super reliability / availability, low latency links, such as critical infrastructure, vehicles, remote control of medical treatment
- Large Internet: 5G seamlessly connects an enormous number of embedded sensors to all by scaling up data rate, power, mobility and providing a very lean / low cost solution.

5G is designed for forward compatibility. It is said to support  expected services flexibly. 5G wraps the world in super high speed, large capacity "mesh" where it interconnects and controls machines, objects, and devices. Impact on the industry can be too large to estimate. There is the possibility to redefine wide range of industries from retail to education, transportation, entertainment, finance, manufacturing and everything else. This is technology that could greatly change the society such as cars and electricity.

# 3.2 Distributed, cooperation

Machine learning enables model at the location of the edge to process data and take action autonomously. The development of 5G strengthens the network that make autonomous machines connected. Ideally, autonomous machines should act autonomously and cooperate while sharing what they learned and information. Edge gives data with high value density and model trained on the cloud side is reflected on the edge again.

Cloud gives information to the edges that autonomously make decisions, thereby improving the quality of edge’s　decision making and allowing humans to enjoy its perfomance improvement.

![distributed-grid-cloud-networks](//images.ctfassets.net/4l4ail9691ba/5sWa0RZyO4ou0cOAieAuig/53cbacd59783055dc96e3cd26b2c416b/distributed-grid-cloud-networks.png)

# 3.3 ex) Autonomous car and 5G

Autonomous vehicle is typical example of autonomous machine, and area where large-scale investment has been made. Autonomous vehicles have a large amount of sensors and computing power to process tons of data and frequent and immediate decision making.

![Screen Shot 2018-10-16 at 16.43.41](//images.ctfassets.net/4l4ail9691ba/1vZTJ0iwRaugKG6aayOESK/c55f488faaecec4889f30a607aa47405/Screen_Shot_2018-10-16_at_16.43.41.jpg)

There is application area of 5G in autonomous vehicle. It is Vehicle-to-Vehicle (V2V) communication. Autonomous vehicles communicate with each other to avoid collision, reduce consumption of fossil fuel by efficient driving, and improve performance of entire transportation system.

V2X (Vehicle-to-Everything) is standard that communicates among vehicles, among roads and vehicles, or among human and cars. It is regarded as indispensable technology for achieving ADAS or automatic operation at level 3 or higher. Conventionally, research and development of V2X has been directed to communication format of WiFi called DSRC (Dedicated Short Range Communications). However, especially in Europe and the United States, the move from DSRC to V2X using a cellular network called "C - V 2X" is progressing rapidly.

Since 5G uses a much wider frequency band than the current cellular network, theoretically, it is possible to exchange a large amount of data at a much faster rate than today. It can help autonomous driving by telling other C - V 2X cars driving around in advance the actions intended by the C - V 2 X car.

Sensor data processing requirements are extremely severe, accidents may occur if there is even a bit of latency. Therefore, it is unthinkable to set a place of analysis and decision making   at the cloud. 

Communication with remote spots in real time is narrowed down to providing  information without urgency like traffic jam. Communication connecting machines is emphasized. The connection and corroboration among machines is called M2M (Machine to Machine).

# 3.4 General purpose robotics

Numerous application examples of autonomous machines are appearing. Drone can increase the number of Simultaneously operating units and expand range of activities by 5G multiple connection and low delay. 
In addition to the application to logistics such as home delivery, Drone also plays a role of “flying computer”, loading camera, data processing unit  and analytics capability on itself, sending only useful data to the center, taking specific actions, etc. Industrial robots have so far demanded very much by manufacturers, and unmanned production lines will become more common in the future. Other robots of housekeeping and cooking are also eagerly developed.

Current Human Computer Interface (HCI) is overly screen dependent, but diversification can be considered when we communicate with robots. It is already common to use voice interfaces for virtual agents like Google Assistant, not physical robots. If you tell a house keeping robot "Please clean the kitchen" in your voice, the robot will identify the master's intention and get things done.

Machine learning is opening up the possibility of robotics. The ultimate goal is a general-purpose robot that can carry out all the requirements people need. A lot of high-quality data is required to train the model, but this data amount requirement is clear bottleneck of social implementation of machine learning. In the past few years, making high-quality models with less data has become a common goal of machine learning stakeholders.

Deep Mind's AlphaZero / Alpha Go Zero is typical example. AlphaZero / Alpha Go Zero [achieves](https://deepmind.com/blog/alphago-zero-learning-scratch/) a rating far higher than humans with reinforcement learning without training data, after setting only rules of Go, Shogi and so on.

# 3.5 VR・AR・MR

5G is expected to promote social implementation of VR (virtual reality), AR (augmented reality), MR (mixed reality). Usage can be used not only in gaming and entertainment but also in the field of scientific research, medical care, product development, and retail.

Technology development of AR is the fastest, and in the short term consumer needs are also strongest. Currently AR machine can not render graphics immediately without goggle connected a large hardware of  enclosure. Consumers envision the famous "Barrettime" of "Matrix", but the hardware developed by AR startup like MagicLeap has not reached that stage.

![Screen Shot 2018-08-31 at 11.11.21](//images.ctfassets.net/4l4ail9691ba/1p9Ri77jeU28Ow8KeUw688/aa8a55cae5ca3c2d1cd22107aa5d6e70/Screen_Shot_2018-08-31_at_11.11.21.png)

Even if 5 G is large enough to endure sending AR data, it is not fun because  goggle must be connected with the big hardware. Fortunately the performance improvement of the GPU has not been stagnant so far, so anyone should be able to tamper with the AR in the streets, get things done and enjoy entertainment. There will be many people like Tom Cruise in "minority report".

Since mobile phones have a role as a "camera", there is a possibility that it will keep mobile phones to survive in the world. Especially for young people mobile phones are getting more valuable as devices for generating and viewing videos and images. Watching videos can be transferred to AR devices, but shooting is done by phone. Video viewing is shifted to the AR device, but shooting function may remain on the phone. The future market will answer on whether the camera becomes an independent use case like Go Pro. Anyway, it is strange that "the phone survives as a camera".

# 4. Conclusion

We are ahead of major changes in computers and their networks. Mobile was intense expansion of one point breakthrough, but in the future various  factors will widen it and will diversify as quickly as possible. 

It is not collapse of mobile, but mobile is hopeful gateway drag of the Internet and computing in emerging countries, and should keep a certain position even in wealthy countries (at least it is not a phone, the camera is promising). 
Machines that work autonomously around humans will increase drastically and will be developed as “human in the loop". By entrusting various jobs to the machine, time spent for high productivity will increase.

Our society creates tremendous productivity by doing things with autonomous machines that coordinate and cooperate. What you could not imagine with the previous centralized computing would be born in the future.

Economy making explosive development and argument on next economic principle after capitalism may be within the scope of the influence of changes in computing. The way we interact with machines is diversified, not very small screens of mobile phone, but AR / VR / MR and voice. We strongly realize that the change will bring about our capacity expansion.

__Read first harf [2019 Prediction: Post-Mobile, Strike Back Of Edge(1)](https://axion.zone/welcome-to-post-mobile-age-connectivity-and-autonomous-machine/)__

---

Eyecatch image via Qualcomm 

# Refence

機械学習用チップの性能評価 : TPU の研究論文を公開
https://cloudplatform-jp.googleblog.com/2017/04/quantifying-the-performance-of-the-TPU-our-first-machine-learning-chip.html?m=1

New AIY Edge TPU Boards
https://developers.googleblog.com/2018/07/new-aiy-edge-tpu-boards.html

FPGA＋Edge Computing
High-throughput Object Detection on Edge Platforms with FPGA
https://ai.intel.com/high-throughput-object-detection-on-edge-platforms-with-fpga/

Cloud Tensor Processing Units (TPUs)
https://cloud.google.com/tpu/docs/tpus

Dave Patterson, on TPU
https://youtu.be/fhHAArxwzvQ

FPGA
https://www.microsoft.com/en-us/research/blog/clouds-catapults-life-end-moores-law-dr-doug-burger/

Azure Sphere
https://azure.microsoft.com/en-us/blog/introducing-microsoft-azure-sphere-secure-and-power-the-intelligent-edge/
 
---
Thank you so much to read this long blog. If you would like to talk about me over having lunch,or tea etc, please contact @ taxiyoshida (twitter) by all means. I am looking for co-founder now. More details here.

