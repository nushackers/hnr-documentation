---
layout: default
title: Volunteer Guide
permalink: /usage-guide/volunteer-guide
nav_order: 2
parent: Usage Guide
---

## Check in

Indicate participant ID, fetch, and then enter given tag number.

If cannot enter tag number, ensure 'Fetch' button is pressed.

Tied to `"Users"`, `"Quests"`, `"QuestCompletionCodes"`, `"QuestCompletionCodeUsers"`

If there's an error that

- Task id not valid
- Task not open
- Anything else

Contact ops team to resolve (likely `ValidFrom` issue or pointing to `"QuestCompletionCodes"."Id"` instead of the `"QuestId"`)

## Collecting items

Scan OR enter the participant's tag number and select the item for them to collect.

Tied to `"Users"`, `"Collectible"`, `"CollectedCollectible"`

If the QR code scanner is not working, just manually enter (but contact ops to resolve).

Items are only populated when they open for collection. The timing schedule will be sent to the Telegram channel.
