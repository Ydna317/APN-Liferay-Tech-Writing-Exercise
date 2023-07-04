<div style="width: 100%; max-width: 700px;">
<div align="center">
<h3>APN-Liferay-Tech-Writing-Exercise</h3>
<h1><b>Andy P. Nguyen</b><br />
<a href="https://github.com/Ydna317/APN-Liferay-Tech-Writing-Exercise/blob/main/README.md#introduction"><img style="width: 25px;" src="github.svg"></a> | <a href="https://www.linkedin.com/in/andyphuocnguyen/"><img style="width: 25px;" src="linkedin.svg"></a></h1>
<img style="border-radius: 10px; background: white"; src="https://upload.wikimedia.org/wikipedia/commons/b/b2/Liferay-logo-full-color-2x.png?20180821104041">
</div>

___

# **Table of Contents**

[Technical Writing Exercise 1:](#tech-writing-exercise-1)
1. [Introduction](#introduction)
2. [DVR Playback](#dvr-playback)
3. [TV Recording](#tv-recording)

[Technical Writing Exercise 2:](#tech-writing-exercise-2)
1. [Original Prompt](#original-prompt)
2. [Edited Prompt](#edited-prompt)

[Technical Writing Exercise 3:](#tech-writing-exercise-3)
1. [Original Method](#original-method)
2. [Edited Method](#edited-method)

___

## **_Tech Writing Exercise 1:_**
Write part of a tutorial that includes an introduction and two sections for a manual on how to
use a DVR. Instructions should be well-organized and clear. Since reading instruction manuals
can be boring, try to liven things up through good organization, enthusiasm, or maybe even
humor.

- Introduction: Summarize the content in the sections that follow.
- Section 1: Explain DVR playback (including play, stop, pause, fast-forward, and rewind).
- Section 2: Explain how to record a TV show.

___

## **Introduction**

Ever thought of being able to record your favorite shows and watch them on demand?! Well, welcome to the age
of technology with your brand new Thisknee Plus DVR! 

Your DVR or, "Digital Video Recorder," is an electronic device that records your favorite tv broadcasts and films and stores them within its built-in hard drive. Set up your DVR at home and you will have the power and promise of recording your favorite superhero, royalty romance, galactic war, and Graphical Neogeography films with the touch of a button!

Below you will find your quick start instructions on using your new DVR: 

<div align="center"><img style="background: white; width: 200px;" src="svgdigitalvideorecorder.png"><img style="background: white; width: 200px;" src="svgremotecontrol.png"></div>

___

## **DVR Playback**
Play, stop, fast-forward, and rewind video content at your convenience!

Locate the buttons pictured below and see your DVR in action:

> ___
><img style="background: white; width: 100px;" src="svgplay.png">
>
>**PLAY:**
>Select from multiple sources of video content by using the directional pad of your remote control and sift through hours and hours of digital content.
>Press the 'play' button on any active title and your selection will be played at its current running time.
>___
><img style="background: white; width: 100px;" src="svgstop.png">
>
>**STOP:**
>Stop the playback of your selected video by pressing the 'stop' button on your controller.
>This will pause your video at its current running time.
>The playback of your video can be resumed by pressing play.
>___
><img style="background: white; width: 100px;" src="svgfastforward.png">
>
>**FAST-FORWARD:**
>Fast-forward and speed up the running time of your video by pressing the 'fast-forward' button to quickly reach your desired video designation.
>___
><img style="background: white; width: 100px;" src="svgrewind.png">
>
>**REWIND:**
>Missed a crucial or exciting part of your video because life gets in the way? Rewind your video and rewatch any part of the content on your own time!
>___

___

## **TV Recording**
Again... life gets in the way and you just cannot afford to sit comfortably and enjoy the latest and greatest on your huge 10" TV that's heavier than the stand you placed it on. With our new DVR technology, you'll be able to simply 'set & forget' and your DVR will record for you!

> ___
><img style="background: white; width: 100px;" src="svgrecord.png">
>
>**RECORD:**
>Highlight the video content you would like to record. Press the 'record button' and follow the on-screen instructions to choose how and when you want to record!
>___

___
<div align="center"><b><a style="font-size: 16px;" href="#table-of-contents">Back To Table Of Contents</a></b></div>

___

## **_Tech Writing Exercise 2:_**
Sometimes, documentation is submitted by those for whom English is a challenging
communication medium. You may also be called upon to edit a peer’s documentation. We call
this “wordsmithing.”
Below is a real-world example of documentation submitted by a non-native English speaking
writer. To the best of your ability, please wordsmith this documentation so that it is clear,
concise, and understandable. Hint: your word count when finished should be lower than the
original text.

___

## **Original Prompt**
> 2010's benchmark and optimization is reaching the end, it is time to write something about
what we did in last few months.
>
> Today we will talk about an EE-only feature, a new ehcache cluster replication mechanism.
Since this is only available in EE version portal, i won't talk about impl detail too much. Just
some general concepts about what is the problem and how we fix it.
>
> Ehcache supports cluster, by default it uses RMI replication mechanism, which is a point to
point communication graph. As you can guess this kind of structure can not scale for large
cluster with many nodes. Because each node has to send out N-1 same event to other nodes,
when N is too big, this will become a network traffic disaster.
>
> To make things even more worse, ehcache creates a replication thread for each cache entity. In
a large system like Liferay Portal, it is very easy to have more than 100 cache entities, this
means 100+ cache replication threads. Threads are expensive, because they take
resource(memory and cpu power). But these threads are most likely sleeping over 99% time,
since they only start to work when a cache entity needs to talk to remote peers. Without regard
to thread heap memory(Because this is application depended), just consider stack memory
footprint of that 100+ threads. By default on most platform, the thread stack size is 2MB, that
means 200+MB. If you include the heap memory size, this number may even reach
500MB(This is just for one node!). Even memory chips are cheap today, we still should not
waste them! And massive threads can also cause frequent context switch overhead.
>
> We need to fix both the 1 to N-1 network communication and massive threads
bottleneck.Liferay Portal has a facility called
>
> ClusterLink which is basicly an abstract communication channel, and the default impl is using
JGroups' UDP multicast to communicate.
>
> By using ClusterLink we can fix the 1 to N-1 network communication easily.
>
> To reduce the replication thread number, we provide a small group of dispatching threads. The
are dedicated fory delivering cache cluster event to remote peers. Since all cache enities' cluster
event will go through one place to network, this gives us a chance to do coalesce, if two
modification to the same cache object are close enough, we only need to notify remote peers
once to save some network traffic.
>
> (Newer version ehcache supports JGroups replicator, it can also fix the 1 to N-1 network
communication, itbut cannot fix the massive threads problem and cannot do coalesce.)
For EE customer who is in interested in this feature, you can contact our support engineers for
more detail info.

___

## **Edited Prompt**

>As 2010's benchmark and optimization reach its end, we reflect on our recent work. 
>
>Today's discussion focuses on a new Ehcache cluster replication mechanism exclusive to the EE version portal, providing an overview of our areas of opportunity and possible solutions. Defaultly, Ehcache uses RMI replication for cluster support operating on a point-to-point communication model that cannot scale for large clusters with high node counts.
>
>With each model having to send out the same N-1 event to multiple nodes, if N is too large, this results in high network latency. Ehcache creates a replication thread for each cache entity resulting in expensive resource-intensive consumption of memory and CPU power. Given how easily a large system like Liferay Portal can have more than 100 cache entities at a time, the output of threads would be equivalent. These threads only activate when a cached entity needs to communicate with remote peers, spending over 99% of their time idle otherwise. With a stack memory footprint of 100+ threads and how most platforms allocate 2MB per stack, the output becomes 200+MB. If we consider the application-dependent thread heap memory, the output may even reach 500MB for a single node. Even with memory chips becoming more affordable, our goal is to avoid the frequent context switch overhead caused by massive threads.
>
>To address both the 1-to-N-1 network communication issue and the bottleneck caused by excessive threads, we look to Liferay Portal's "ClusterLink." ClusterLink serves as an abstract communication channel with the default implementation using JGroups' UDP multicast for communication purposes. By leveraging ClusterLink, we can easily resolve the 1-to-N-1 network communication problem by providing a small group of dispatching threads, reducing the replication thread number. These threads are responsible for delivering cache cluster events to remote peers through a centralized location in the network. This allows us to combine nearly identical cache objects allowing us to notify remote peers only once helping keep latency low.
>
>Although a newer version of Ehcache supports the JGroups replicator and can also fix the 1-to-N-1 network communication, it does not allow for the consolidation of cache objects to solve our bottleneck issue.
>
>For EE customers who are interested in this feature, please contact our support engineers for more information.


___
<div align="center"><b><a style="font-size: 16px;" href="#table-of-contents">Back To Table Of Contents</a></b></div>

___

## **_Tech Writing Exercise 3:_**
The insert(...) method below needs Javadoc. The behavior of the method is demonstrated as
follows ...

          String s = "happy day";
          System.out.println(StringUtil.insert(s, " birth", 6)); // prints
     "happy birthday"
          System.out.println(StringUtil.insert(null, " birth", 6)); //
     prints "null"

Fill in the Javadoc for the insert(...) method. Use the <a href="https://github.com/liferay/liferay-portal/blob/master/readme/JAVADOC_GUIDELINES.markdown">Liferay Javadoc Guidelines as a reference.</a>
___

## Original Method

     /**
     *
     *
     *
     * @param s
     *
     * @param insert
     *
     * @param offset
     *
     * @return
     *
     */
     public static String insert(String s, String insert, int offset)
     {
     
     ...
     }

___

## Edited Method

     /**
     * Method takes String s = "happy day" and displays "happy birthday"
     * when String s is inserted by replacing index 6 of String s with
     * " birth" or displaying "null" when value is unknown or missing.
     * @param s contains the value of "happy day"
     * 
     * @param insert inserts String s or null value into the method
     * value of s = "happy day" / unknown or missing value = "null"
     * @param offset replaces index 6 with value "birth"
     * 1:h 2:a 3:p 4:p 5:y 6:_ 7:d 8:a 9:y
     * @return displays "Happy Birthday" if String s is inserted and "null" if value is missing or unknown
     *
     */
     public static String insert(String s, String insert, int offset)
     {
     
     ...
     }

___

<div align="center"><b><a style="font-size: 16px;" href="#table-of-contents">Back To Table Of Contents</a></b></div>

</div>
