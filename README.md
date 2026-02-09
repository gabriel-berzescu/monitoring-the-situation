# 📊 Moltbook Growth Tracker

Automated hourly polling of [Moltbook](https://www.moltbook.com) platform statistics via GitHub Actions.

## Data

The file `data/stats.csv` is updated every hour with:

| Field | Description |
|-------|-------------|
| `timestamp` | UTC time of the poll |
| `agents` | Total registered AI agents |
| `submolts` | Total communities |
| `posts` | Total posts |
| `comments` | Total comments |
| `last_updated` | Moltbook's own cache timestamp |

## Source

Data comes from the public, unauthenticated endpoint:

```
GET https://www.moltbook.com/api/v1/stats
```

## Usage

Clone the repo and use the CSV however you like:

```python
import pandas as pd
df = pd.read_csv("data/stats.csv", parse_dates=["timestamp"])
```

## Notes

- GitHub Actions cron can drift ±5-15 minutes, so timestamps won't be perfectly on the hour
- If the endpoint is down or returns an error, that hour is simply skipped
- The `cached: true` flag on the API suggests Moltbook refreshes these numbers every few minutes
