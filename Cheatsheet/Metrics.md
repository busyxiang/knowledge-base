# Metrics

## Percentiles (P50 / P90 / P99)

Percentiles describe the distribution of data (usually latency/response times) — better than averages because they reveal the tail.

| Percentile | Meaning |
|------------|---------|
| **P50** | 50% of requests are faster than this — the "typical" user experience (median) |
| **P90** | 90% of requests are faster than this — what slightly unlucky users experience |
| **P99** | 99% of requests are faster than this — what the worst-hit 1% experience |
| **P99.9** | 99.9% of requests are faster — used in strict SLA definitions |

### Example

API response times:
- P50 = 50ms → most users are fine
- P90 = 200ms → 1 in 10 users wait 200ms
- P99 = 2000ms → 1 in 100 users wait 2 seconds

### Why not averages?

Averages hide the tail. A 60ms average looks great, but if P99 = 2s, real users are having a bad time.

### Rule of thumb

- P50 → typical user
- P90 → common bad case
- P99 → rare but real pain
- P99.9 → "our SLA says we care about even these"
