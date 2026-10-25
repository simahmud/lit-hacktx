# Leave It To

*Your group chat has been saying "we should" for weeks. Leave it to tech.*

Screenshot a chaotic group chat and get a real, shareable plan: actual events, places, hours, and prices, plus a timeline that respects what everyone said.

Built at HackTX 26.

## How it works

```
Screenshot
    |
    v
Gemini      reads the image, extracts intent, constraints, unresolved questions
    |
    v
SerpApi     turns vague references into real events, places, hours, prices
    |
    v
Meta Muse   resolves conflicts, reasons about the group, writes the final plan
    |
    v
Plan card
```

| Stage | Tool | Job |
|---|---|---|
| Understand | Gemini API | Multimodal read of the screenshot, structured JSON out |
| Ground | SerpApi | Events, local/maps search for real-world data |
| Reason | Meta Muse Spark | Social reasoning, conflict resolution, final plan |

## Example

The chat:

> **Sarah:** wait we should actually go to that concert
> **Maya:** YES but I'm broke 💀
> **Charitha:** isn't it friday
> **Sarah:** I think saturday
> **Maya:** also I don't wanna drive downtown
> **Charitha:** there's that ramen place nearby too

The output:

- Looks like you're planning **Saturday**
- Concert: time, venue, ticket price
- Food nearby: restaurant, distance, hours
- What your group said: keep it cheap, avoid driving downtown, ramen afterward
- Suggested timeline from meetup to ramen

## Data contract

**Stage 1 output (Gemini extraction):**

```json
{
  "intent": "plan",
  "summary": "concert outing",
  "participants": ["Sarah", "Maya", "Charitha"],
  "constraints": ["budget", "avoid_driving"],
  "entities": [
    {"type": "event", "query": "concert"}
}
```