# Network Intrusion Detection Case Study: InterOptic Saves the Planet

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/c87ffeea-467b-4ad2-aa19-6b45e19c4584)

## Description

This project documents the analysis of a network intrusion detected within MacDaddy Payment Processor's network. We delve into a Snort IDS alert involving the transmission of potential shellcode to an internal host.

## Table of Contents

- [Introduction](#introduction)
- [Tools Used](#tools-used)
- [Alert Details](#alert-details)
- [Analysis](#analysis)
  - [Snort Alert Analysis](#snort-alert-analysis)
  - [Initial Packet Analysis](#initial-packet-analysis)
  - [Snort Rule Analysis](#snort-rule-analysis)
  - [Carving a Suspicious File from Snort Capture](#carving-a-suspicious-file-from-snort-capture)
  - [INFO WEB BUG Alert](#info-web-bug-alert)
  - [TCP Window Scale Option Alert](#tcp-window-scale-option-alert)
- [Findings](#findings)
- [Theory of the Case](#theory-of-the-case)
- [Conclusion](#conclusion)



## Introduction

In response to a "SHELLCODE x86 NOOP" alert generated by Snort IDS, a thorough investigation was initiated to verify the alert and understand the extent of the intrusion attempt on an internal host with IP 192.168.1.169.

## Tools Used

- `**Snort IDS**`
- `**tcpdump**`
- `**Wireshark**`
- `**grep**`

## Alert Details

The alert was raised by Snort IDS when a potential shellcode was detected in traffic sent to an internal host within the network.

## Analysis

### Snort Alert Analysis

A detailed examination of the "SHELLCODE x86 NOOP" alert and its context within the network traffic was conducted to verify its authenticity.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/667bf65c-7ab6-48cd-a11e-696153c0ec06)

### Initial Packet Analysis

The corresponding network packet identified by the alert was extracted using `tcpdump` and further analyzed to scrutinize its content.


![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/3c0f7798-e588-4557-9648-4f81bf3c4374)


![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/918bf63b-966d-4249-8d58-3e4a956d1e1c)

### Snort Rule Analysis

The Snort rule that resulted in the alert was analyzed to understand the criteria for detection of such threats.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/883bb660-39e3-47b9-9648-e4a877036920)

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/d5f8fbd8-959e-4d44-93c9-1737be394533)

### Carving a Suspicious File from Snort Capture

A suspicious JPEG file, which may have contained executable code, was carved out from the packet capture for deeper examination.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/db26cce5-8205-489c-9365-850997ffbe43)

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/51e13f74-4e2a-4ac9-8dc7-955d2b8ef9fa)

### INFO WEB BUG Alert

Additional alerts related to web bugs were analyzed to understand their relation to the initial SHELLCODE alert.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/78a2761c-e7f6-4920-a708-3e2a3ff62493)

### TCP Window Scale Option Alert

Alerts related to TCP Window Scale options were examined to assess potential reconnaissance activities following the initial exploit.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/9ec4da97-126b-4368-8369-e0bb43afa0a4)

## Findings

The investigation revealed a series of network events that could be indicative of a drive-by exploit followed by reconnaissance within the network.

![image](https://github.com/anvithalolla/Network-Intrusion-Detection/assets/55392153/6a5673c5-8305-40b3-b4b5-5b8b5ec28a32)

## Theory of the Case

Based on the analysis, we have formulated the following theory:

- From 07:45:09 to at least 08:15:08 on 5/18/11, the internal host 192.168.1.169 was engaged in web browsing, during which it encountered web bugs.
- At 08:01:45, an external server delivered a JPEG image that contained a suspicious binary sequence.
- By 08:04:28, the internal host began sending crafted packets to other hosts on the local network, suggesting a scanning and fingerprinting operation.

The "SHELLCODE x86 NOOP" alert and subsequent reconnaissance packets strongly suggest a drive-by exploit, potentially compromising the internal host.

## Conclusion

The events suggest that the internal host was compromised via a drive-by exploit and then used to perform reconnaissance within the internal network.
