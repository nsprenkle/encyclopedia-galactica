# Disaster Recovery

From <https://en.wikipedia.org/wiki/Disaster_recovery>

The topic of determining ways to prevent, detect, or corrrect from disasters

1. **Preventive measures** aim to preventing an event from occurring
2. **Detective measures** aim to detect or discover unwanted events
3. **Corrective measures** aim to correct or restore a system after a disaster or event

## Preventative

First, need to know what types of disasters you're protecting against. They often involve corruption or loss of data, in which case backups are a good strategy.

Ask if backups are in place, how frequently they are taken and retained, and where they are stored.

> Storage locality is important because while local backups can protect against loss of data, they can't protect against problems like loss of the entire site.

Game day drills should also be performed to confirm that all the pieces of the data recovery process work.

## Detective

Ideally, preventative measures keep most disasters from happening. In the case that they do, detective measures should automatically alert us to a disaster event.

Again, it helps to know the type of disasters to determine what types of detection should be implemented.

## Corrective

When a disaster is detected, how do we start the recovery process and what is the service level agreement (SLA) or expected time to recover?