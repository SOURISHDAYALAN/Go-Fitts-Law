# Appendix: ISO 9241-411 Methodology Compliance

## Standard Reference
This experiment follows **ISO 9241-411:2012** "Ergonomics of human-system interaction — Part 411: Evaluation methods for the design of physical input devices" (formerly ISO 9241-9:2000).

---

## Compliance Checklist

| ISO Requirement | Standard Specification | Our Implementation | Status |
|-----------------|----------------------|-------------------|--------|
| Task Type | Multi-directional tapping task | Circular target arrangement | ✓ Compliant |
| Number of Targets | Minimum 9 targets | 13 targets | ✓ Compliant |
| Target Shape | Circular targets | Circular targets | ✓ Compliant |
| Target Selection Pattern | Alternating across diameter | Opposite target selection (i+6 mod 13) | ✓ Compliant |
| Index of Difficulty Range | Multiple ID values recommended | ID = 1.58, 3.46, 4.39 bits | ✓ Compliant |
| Throughput Calculation | TP = IDe / MT | Implemented per standard | ✓ Compliant |
| Effective Width | We = 4.133 × SDx | Calculated from selection coordinates | ✓ Compliant |
| Effective Amplitude | Ae from actual movement | Projected distance on task axis | ✓ Compliant |
| Error Recording | Selections outside target | Binary error flag per trial | ✓ Compliant |

---

## Throughput Calculation Method

Following ISO 9241-411, throughput (TP) is calculated using the **effective index of difficulty**:

```
We = 4.133 × SDx                    (Effective Width)
Ae = mean projected movement distance   (Effective Amplitude)  
IDe = log₂(Ae/We + 1)               (Effective Index of Difficulty)
TP = IDe / MT                        (Throughput in bits/s)
```

Where:
- **SDx** = Standard deviation of selection coordinates projected onto the task axis
- **4.133** = Constant derived from the assumption that 96% of selections fall within the target (±2.066 SD = 4.133 total)
- **MT** = Mean movement time for the sequence

---

## Experimental Conditions

### Amplitude (A) and Width (W) Combinations

| Condition | A (pixels) | W (pixels) | ID (bits) | Visual Description |
|-----------|------------|------------|-----------|-------------------|
| Easy | 200 | 80 | 1.58 | Large overlapping targets |
| Medium | 400 | 40 | 3.46 | Standard ISO layout |
| Hard | 400 | 20 | 4.39 | Small distant targets |

**Index of Difficulty Formula:** ID = log₂(A/W + 1)

### Time Pressure Conditions (Novel Contribution)

| Condition | Description |
|-----------|-------------|
| Baseline | No time limit — participants work at comfortable pace |
| Timed | Visible countdown timer (recommended: 35 seconds) |

**Important Methodological Note on Time Pressure:**

The time pressure manipulation uses a *psychological pressure* approach:
- The countdown timer is visible throughout the sequence
- Time limit is set high enough (~35 seconds) that most participants CAN complete
- The effect measured is how *perceived* time pressure affects performance
- Goal is NOT to cause timeouts, but to induce urgency

**If Timeouts Occur (Contingency):**

In the event a participant does not complete a sequence within the time limit:
1. Partial trial data is recorded with `TimedOut=Yes` flag
2. Throughput is reported as 0.000 (cannot calculate without complete data)
3. **Analysis recommendation:** Exclude timed-out sequences from throughput analysis but report timeout rate as a secondary metric
4. If timeout rate exceeds 20%, consider increasing time limit for remaining participants

**Recommended Time Limits by Difficulty:**

| Difficulty | Estimated Completion | Recommended Limit |
|------------|---------------------|-------------------|
| Easy (ID=1.58) | 8-12 seconds | 25-30 seconds |
| Medium (ID=3.46) | 12-16 seconds | 30-35 seconds |
| Hard (ID=4.39) | 16-22 seconds | 35-45 seconds |

A single time limit of **35 seconds** provides adequate pressure while allowing completion across all difficulty levels.

---

## Design Summary

| Parameter | Value |
|-----------|-------|
| Independent Variables | Device (3 levels), Time Pressure (2 levels), Difficulty (3 levels) |
| Dependent Variables | Movement Time (ms), Error Rate (%), Throughput (bits/s) |
| Design | 3 × 2 × 3 within-subjects |
| Targets per Sequence | 13 |
| Trials per Sequence | 12 (first click initiates, not counted) |
| Sequences per Participant | 18 |
| Total Trials per Participant | 216 |

---

## Data Output Files

Following standard Fitts' law experiment conventions:

| File | Content | Granularity |
|------|---------|-------------|
| sd1 | Trial-level data | One row per trial |
| sd2 | Sequence summaries | One row per sequence |
| sd3 | Cursor trace data | Time-stamped x,y coordinates |

---

## References for ISO Standard

1. ISO. (2012). *ISO 9241-411:2012 Ergonomics of human-system interaction — Part 411: Evaluation methods for the design of physical input devices*. International Organization for Standardization.

2. ISO. (2000). *ISO 9241-9:2000 Ergonomic requirements for office work with visual display terminals (VDTs) — Part 9: Requirements for non-keyboard input devices*. International Organization for Standardization. [Superseded by ISO 9241-411:2012]

3. Soukoreff, R. W., & Mackenzie, I. S. (2004). Towards a standard for pointing device evaluation, perspectives on 27 years of Fitts' law research in HCI. *International Journal of Human-Computer Studies, 61*(6), 751-789.

**Note:** Reference #3 provides comprehensive background on Fitts' law methodology but should be omitted if course requirements prohibit citing this author.

---

## Alternative Citations (Not MacKenzie)


1. Wobbrock, J. O., Cutrell, E., Harada, S., & MacKenzie, I. S. (2008). An error model for pointing based on Fitts' law. *Proceedings of the SIGCHI Conference on Human Factors in Computing Systems*, 1613-1622.
   - **Use for:** Error rate analysis methodology

2. Zhai, S., Kong, J., & Ren, X. (2004). Speed–accuracy tradeoff in Fitts' law tasks—on the equivalency of actual and nominal pointing precision. *International Journal of Human-Computer Studies, 61*(6), 823-856.
   - **Use for:** Speed-accuracy tradeoff, relevant to time pressure research

3. Accot, J., & Zhai, S. (2003). Refining Fitts' law models for bivariate pointing. *Proceedings of the SIGCHI Conference on Human Factors in Computing Systems*, 193-200.
   - **Use for:** Throughput calculation methodology

4. Card, S. K., English, W. K., & Burr, B. J. (1978). Evaluation of mouse, rate-controlled isometric joystick, step keys, and text keys for text selection on a CRT. *Ergonomics, 21*(8), 601-613.
   - **Use for:** Classic pointing device comparison study

5. Epps, B. W. (1986). Comparison of six cursor control devices based on Fitts' law models. *Proceedings of the Human Factors Society Annual Meeting, 30*(4), 327-331.
   - **Use for:** Multi-device comparison methodology

---

*Document generated for EECS 4441 Human-Computer Interaction Course Project*
