# FreeTAKHub VideoChecker

This integration allow to use a streaming software like TAK ICU with the Video Server and FTS
![image](https://user-images.githubusercontent.com/60719165/139940405-8e841a98-58e3-431a-8bb6-fce8462b3ef7.png)
It periodically connects to the RTSP-simple server using the API, check for the existence of streams 

the video stream is sent to all the connected TAK Devices

![image](https://user-images.githubusercontent.com/60719165/139935868-59624431-1f17-4503-8c6a-d682f75d97c1.png)

Now you can retrieve it in your video list

## Architecture
![image](https://user-images.githubusercontent.com/60719165/140407685-ce123520-6199-4cc6-ab3f-d07103dc868e.png)
FTS 1.9 requires up-to 5 different nodes (VMs). In this use case it's suggested to use 3 different servers.

_While it's possible to run all on the same machine, performances will be severly affected_

Android Phone for spotter: an android phone with TAK ICu installed. Used by the spotter to send the video stream.

* Video Service: simple RTSP server 0.7 or better with APi activated. 
the video Service checker uses the API to verify if streams are running there and notify FTS
* FTH server: runs other integrations such as Telegram Connector, Video Service Checker, check-in system, SALUTe report  and Global Emergency Checker
* FTS Cloud Server: hosts the core of FTS
* Android Phone(s) for team member(s): this phone has ATAK installed
FTS send a notification with the COT
ATAK shows the video, connecting to the FTS to visualized the COT and to the video server to get the video feed.

## Installation
* install [FTS 1.9 +](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/Linux/Install.md)
* Install [RTSP-simple Server v0.17.0 +](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/Video/Installation.md)
* Install [NodeRed](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/NodeRedinstallation.md)
* import the NodeRed Flow in your FTS hub
* Install the node-red contrib-config 
![image](https://user-images.githubusercontent.com/60719165/143119468-5f86814c-f8a4-4376-92c8-0f4d71873f8f.png)


## Configuration
* API service must be active on FTS 
* API service must be active on RTSP-simple Server
* in the node "Post  Video to FTS" set a valid your Rest API token

![image](https://user-images.githubusercontent.com/60719165/139943631-4c6dd8ef-80fa-439c-be9c-84280ad8103c.png)

* in the "FTH Global Config" node set the value for IPs of the different servers

Here are the names of those global variables and some sample values.

```
 "FTH_FTS_URL": "127.0.0.1"
 "FTH_FTS_API_Port": "19023"
 "FTH_FTS_STREAM_Port": "8554"
 "FTH_FTS_VIDEO_URL": "127.0.0.1"
 "FTH_FTS_VIDEO_API_Port": "9997"
```

## Contents

### `freetakhub_videochecker.json`

Deprecated.

This contains a flow for setting the global context variables.
Using global context variables is not guaranteed to be installed before they are used.
Since v3.1 NodeRED recommends using global environment variables instead.

### `freetakhub_videochecker.json_n3.json`

Updates to use global environment variables.


### `README.md`

This file.

### `LICENSE`

Eclipse Public License.
