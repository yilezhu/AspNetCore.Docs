---
title: Automatically reconnect with ASP.NET Core SignalR
author: bradygaster
description: Learn how to handle disconnections and automatically reconnect with the ASP.NET Core SignalR clients.
monikerRange: '>= aspnetcore-3.0'
ms.author: shalter
ms.date: 2/26/2019
uid: signalr/auto-reconnect
---

# Automatically reconnect with ASP.NET Core SignalR

By [Stephen Halter](https://github.com/halter73)

## JavaScript client

### Opt in to automatic reconnects

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/myHub")
    .enableAutomaticReconnects()
    .build();
```

### Automatic reconnect configuration

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/myHub")
    .enableAutomaticReconnects({
        reconnectTimeout: 60000
    })
    .build();
```

| Option | Default Value | Description |
| ------ | ------------- | ----------- |
| `reconnectTimeout` | 30000 milliseconds (30 seconds) | The client will stop attempting to reconnect to the server if it fails to reestablish a connection within this timeout. At this point, the client will transition from the reconnecting to connected state. |
| `maxReconnectDelay` | 5000 milliseconds (5 seconds) | The client will wait a random interval up to the `maxReconnectDelay` after observing a connection failure before attempting to establish a new connection. This is designed to prevent a flood of simultaneous connections from reconnecting SignalR clients after a server restart.

## .NET client

### Opt in to automatic reconnects

```csharp
var connection = new HubConnectionBuilder()
    .EnableAutomaticReconnects()
    .Build();
```

### Automatic reconnect configuration

```csharp
var connection = new HubConnectionBuilder()
    .EnableAutomaticReconnects(options =>
    {
        ReconnectTimeout = TimeSpan.FromMinutes(1)
    })
    .Build();
```