---
sidebar_position: 1
---

# Introduction

Let's discover **go-flowmeter in less than 5 minutes**.

## What is it ?

go-flowmeter is an ethernet traffic flow generator and analyser for anomaly detection.

## Why is it useful ?

When trying to analyse the behavior on an internet traffic, having data to work on which is properly formatted and
represents the network's activity is the most important step.
This tool helps to build those kind of datasets.

## How does in work ?

From a high-level perspective, go-flowmeter pulls data from a network and reshapes it.
From a more technical point of view, it needs data, extracted by a sniffer in a PCAP format, to create flows of
bidirectional traffic that can be used by a machine-learning model to try detecting anomalies.
