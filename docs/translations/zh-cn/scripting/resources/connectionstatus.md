---
title: Connection status
description: Connection status used by NetStats_ConnectionStatus.
---

## Description

This page contains the connection statuses used by [NetStats_ConnectionStatus](../functions/NetStats_ConnectionStatus). These constants are used internally by RakNet (the networking library SA-MP uses).

## Often used

| ID       | State                                                                                     | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0        | CONNECTION_STATUS_NO_ACTION **/** CONNSTAT_NO_ACTION                                      | Whenever a packet has to be sent to the client, it will be processed by a separate thread. As this thread is sending a packet, it is possible for the server to say... receive a disconnection packet, which may get processed in the meantime. This would result in data racing (and thus the behavior is undefined). To solve this problem, the connection state will change to CONNECTION_STATUS_NO_ACTION, and any changes to the player ID will not occur until the update thread has given the main thread the "green light". Now, as a server developer, this connection state is not really relevant to you, so you probably won't ever need it. |
| 1        | CONNECTION_STATUS_DISCONNECT_ASAP **/** CONNSTAT_DISCONNECT_ASAP                          | The client is to be disconnected as soon as possible. It is possible for NetStats_ConnectionStatus to return this value during the disconnect process, specifically when a player is not yet "truely" disconnected, yet [OnPlayerDisconnect](../callbacks/OnPlayerDisconnect) may have fired already for this player.                                                                                                                                                                                                                                                                                                                                    |
| 2        | CONNECTION_STATUS_DISCONNECT_ASAP_SILENTLY **/** CONNSTAT_DISCONNECT_ASAP_SILNT           | The client is to be disconnected as soon as possible, but without sending the ID_DISCONNECTION_NOTIFICATION packet to the client. SA-MP sends this in several cases (however SA-MP itself most likely doesn't, RakNet definitely does), for example when the server password is entered incorrectly.                                                                                                                                                                                                                                                                                                                                                     |
| 3        | CONNECTION_STATUS_DISCONNECT_ON_NO_ACK **/** CONNSTAT_DISCONNECT_ON_NO_ACK                | Unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 4        | CONNECTION_STATUS_REQUESTED_CONNECTION **/** CONNSTAT_REQUESTED_CONNECTION                | The client has requested a connection with the server.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 5        | CONNECTION_STATUS_HANDLING_CONNECTION_REQUEST **/** CONNSTAT_HANDLING_CONN_REQ            | The server is currently handling the connection request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 6        | CONNECTION_STATUS_UNVERIFIED_SENDER **/** CONNSTAT_UNVERIFIED_SENDER                      | Initially, incoming connection requests appear to use UNVERIFIED_SENDER. While the client-server connection is in this state, only ID_CONNECTION_REQUEST packets are read. The server will automatically close the connection and add the client IP to a temporary blacklist if anything else is sent. Whether or not it is possible for [NetStats_ConnectionStatus](../functions/NetStats_ConnectionStatus) to return this status is doubtful.                                                                                                                                                                                                          |
| 7        | CONNECTION_STATUS_SET_ENCRYPTION_ON_MULTIPLE_16_BYTE_PACKET **/** CONNSTAT_SET_ENCRYPTION |
| Unknown. |
| 8        | CONNECTION_STATUS_CONNECTED **/** CONNSTAT_CONNECTED                                      | The client is connected to the server.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |