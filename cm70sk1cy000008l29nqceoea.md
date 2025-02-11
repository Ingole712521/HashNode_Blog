---
title: "HLS Adaptive Bitrate Streaming"
seoTitle: " HLS Adaptive Bitrate Streaming"
seoDescription: "HLS (HTTP Live Streaming) has emerged as a leading protocol, revolutionizing the way content is delivered over the internet"
datePublished: Tue Feb 11 2025 18:04:10 GMT+0000 (Coordinated Universal Time)
cuid: cm70sk1cy000008l29nqceoea
slug: hls-adaptive-bitrate-streaming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739296924742/fcbf4d36-c2a8-4540-bcff-d42e2f6f4d18.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1739296969122/7f7806d8-0cf0-418f-bacc-ae5d79521b25.png
tags: aws, streaming, s3, hls, youtube-channel

---

## Introduction

In the ever-evolving landscape of online video streaming, HLS (HTTP Live Streaming) has emerged as a leading protocol, revolutionizing the way content is delivered over the internet. Let's delve into what HLS is and why it's become a cornerstone of modern streaming technology.

## **What is HLS?**

HLS, or HTTP Live Streaming, is a streaming protocol developed by Apple Inc. as part of its QuickTime, Safari, and iOS software. It enables the delivery of multimedia content, primarily video and audio, over the internet in a highly adaptable and efficient manner.

## **How Does HLS Work?**

HLS breaks down multimedia content into small, manageable chunks, typically lasting a few seconds each. These chunks are encoded at multiple bitrates and resolutions, allowing for adaptive bitrate streaming. A manifest file, known as the M3U8 playlist, provides the client device with information about the available chunks and their characteristics. The client device dynamically selects the appropriate chunks based on network conditions and device capabilities, ensuring a smooth and uninterrupted streaming experience.

---

## Know about docker in Deep

Reference of Docker blog :- [https://teckbakers.hashnode.dev/getting-into-the-world-of-containers](https://teckbakers.hashnode.dev/getting-into-the-world-of-containers)

---

## Demo

At the first install docker in your local machine

Step 1:- Create an Empty folder for storing all the code

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364470907/7a4007bc-3b1c-467b-82f1-d72790db103f.png align="center")

Step 2: Build a docker image with the help of Dockerfile

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364508532/ea32925e-40e3-4533-b783-8d5706e60cc0.png align="center")

Step3: Check whether the docker image was created so not

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364439736/5dfd8387-4641-46de-ac4f-a922fecbb495.png align="center")

Step4: For storing your Video from the local machine to docker images mount volume to the docker image from the local machine

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363099046/a0ed92fc-bea2-42a2-8959-a03e79a002f5.png align="center")

Step5:- Use the command to start the video processing

```plaintext
ffmpeg -i sample.mp4 -codec:v libx264 -codec:a aac -hls_time 10 -hls_playlist_type vod -hls_segment_filename outputs/segment%03d.ts" -start_number 0 outputs/index.m3u8
```

---

## Command Breakdown

1. `ffmpeg`:
    
    * This is the command-line tool used for processing video and audio files.
        
2. `-i` [`sample.mp`](http://sample.mp)`4`:
    
    * `-i` specifies the input file. In this case, it is [`sample.mp`](http://sample.mp)`4`.
        
3. `-codec:v libx264`:
    
    * `-codec:v` specifies the video codec to be used.
        
    * `libx264` is a widely used codec for encoding video in H.264 format.
        
4. `-codec:a aac`:
    
    * `-codec:a` specifies the audio codec to be used.
        
    * `aac` (Advanced Audio Codec) is a popular audio codec known for its efficiency and quality.
        
5. `-hls_time 10`:
    
    * This sets the target duration of each segment to 10 seconds. The actual duration might vary slightly to fit the video frames properly.
        
6. `-hls_playlist_type vod`:
    
    * This specifies the type of HLS (HTTP Live Streaming) playlist.
        
    * `vod` (Video on Demand) indicates that the playlist is for on-demand content rather than live streaming.
        
7. `-hls_segment_filename outputs/segment%03d.ts`:
    
    * This defines the naming pattern for the output segments.
        
    * `outputs/segment%03d.ts` means the segments will be saved in the `outputs` directory with filenames like `segment001.ts`, `segment002.ts`, and so on (`%03d` is a placeholder for a three-digit number).
        
8. `-start_number 0`:
    
    * This sets the starting number for the segment files to 0.
        
9. `outputs/index.m3u8`:
    
    * This specifies the output file for the HLS playlist, which will be named `index.m3u8`.
        

---

## What the Command Does

* **Input File**: Takes [`sample.mp`](http://sample.mp)`4` as the input file.
    
* **Video and Audio Encoding**: Encodes the video using the H.264 codec (`libx264`) and the audio using the AAC codec (`aac`).
    
* **Segment Duration**: Splits the video into segments of approximately 10 seconds each.
    
* **Playlist Type**: Generates an HLS playlist suitable for Video on Demand.
    
* **Segment Naming**: Names the segments sequentially starting from `segment000.ts`.
    
* **Playlist File**: Outputs an `index.m3u8` playlist file that references all the created segments.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363178866/f0ea92f1-1b76-4493-8192-7f82e3641ee0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363196172/1adee575-7799-450b-b3eb-a7cfca21cfba.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363214593/81269356-f3e2-4d81-b22d-bd7583340db2.png align="center")

Step6:- After running the command you will get the output in your local machine in folder outputs

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363233825/6f00544c-13dd-4edc-98c6-3bba740124a1.png align="center")

Step7: Uploading in Output in s3 bucket so that we can use it to process video in our application

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718363264321/95e81bbc-72a8-485b-a15d-4f01ee2a11bb.png align="center")

Step8:- check whether aws configure or not

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718365510856/604c275f-c058-445a-b5a4-ef7ba255e94d.png align="center")

Step9:- Upload all the outputs folder into the s3 bucket

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364381058/42308adc-088a-4174-87f3-e6738e5ce5ed.png align="center")

Step10: Copy index file s3 url it use in index.html file as a source of video

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364402051/e2b4e04f-9f51-44fe-a541-48899846ccf2.png align="center")

Step10: Copy IP address and paste it into the browser

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718364349765/85b89587-c87b-4ea7-b028-c081a53c3a63.png align="center")

---

## Conclusion

Following this step-by-step guide, you have successfully created an HLS Adaptive Streaming pipeline using Docker and FFmpeg. We built a Docker image, mounted a volume for storing video files, and processed a sample video into HLS format. The segmented video files were then uploaded to an S3 bucket, making them accessible for streaming. Finally, linking the playlist URL in an HTML file allows the processed video to be streamed seamlessly through a browser. This workflow ensures efficient, scalable, and adaptive video streaming for various applications.

For the complete source code, visit the GitHub repository: [HLS Adaptive Streaming](https://github.com/Ingole712521/HLS_Adaptive_Streaming.git).