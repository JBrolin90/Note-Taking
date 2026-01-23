---
Note-Type: Permanent
tags:
  - Permanent
Date: 2026-01-23
Topic:
  - "[[Home Lab]]"
  - "[[rclone]]"
  - "[[sync]]"
---
I use rclone to synchronize the lab folder structure . It makes use of the encrypted "secret" remote.  the secret remote is stored in the OneDrive/secret directory.

Both my desktop and my laptop synchronize bidirectionally against the secret remote. This happens in an asynchronous fashion.

It might be better if that synch of both computers happened from only one machine, in which case it would be synchronous, one after the other..


