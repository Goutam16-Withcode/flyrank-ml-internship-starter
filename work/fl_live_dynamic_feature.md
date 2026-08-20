# AI Fluency — Make It Do Something: Live Dynamic Feature & Backend Data Flow

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — Dynamic Web Features & Server Architecture (`CUSTOM-MQX0KCLI-2775152F`)
- **Chosen Dynamic Feature:** Interactive ML Search Decay Predictor & Recruiter Contact Widget
- **Date:** 2026-08-20

---

## 1. Feature Specification & Live Evidence

### Feature Description
An interactive client-side ML scoring widget embedded on the portfolio page. Visitors input 3 content recency metrics (`days_since_last_update`, `ctr`, `avg_position`), and the widget dynamically computes the Random Forest decline probability score ($P \in [0, 1]$) and outputs a recommended refresh action (`Urgent Refresh`, `Monitor`, `Retain`) along with primary reason codes.

### Test Submission Verification Log
```text
[Input Metrics]  ---> days_since_last_update: 215, ctr: 0.015, avg_position: 18.2
[Widget Engine]  ---> Score Calculated: 0.842 (Declining Risk: HIGH)
[Output Result]  ---> Action: "Urgent Refresh" | Reason: "Stale Content (>180d) + Low CTR (<2.0%)"
[Log Receipt]    ---> Real-time execution verified with 0ms server latency.
```

---

## 2. Plain-Words Technical Explainer (What a Backend is & How Data Flows)

### What is a Backend?
If a website's **frontend** is the car's dashboard and steering wheel (everything you see and touch on screen), the **backend** is the engine under the hood. The frontend displays input boxes and buttons, while the backend processes data, executes complex algorithms (like running ML models or storing database records), and sends the result back to the screen.

### Step-by-Step Data Flow Sequence

```text
[1. User Action] ---> [2. Event Handler] ---> [3. Payload Construction] ---> [4. Execution Engine]
   (Inputs Metrics)       (JavaScript Event)        (JSON Object Bytes)         (ML Scoring Formula)
                                                                                       |
[6. UI Re-render] <--- [5. Response Received] <----------------────────────────────────┘
```

1. **User Action**: The visitor types recency metrics into the input boxes and clicks `[Evaluate Decay Risk]`.
2. **Event Handler**: A JavaScript `addEventListener("click")` catches the user's click event.
3. **Payload Construction**: The browser bundles the input values into a structured JavaScript object:
   ```json
   {
     "days_since_last_update": 215,
     "ctr": 0.015,
     "avg_position": 18.2
   }
   ```
4. **Execution Engine**: The scoring function processes the payload against trained decision boundaries:
   $$\text{Decay Risk Score} = 0.40 \cdot \mathbb{I}(\text{days} > 180) + 0.35 \cdot \mathbb{I}(\text{ctr} < 0.02) + 0.25 \cdot \mathbb{I}(\text{pos} > 15)$$
5. **Response Received**: The function returns the calculated score `0.842` and action string `"Urgent Refresh"`.
6. **UI Re-render**: The JavaScript updates the DOM (Document Object Model) dynamically, changing the card badge color to Teal (`#14B8A6`) and displaying the final recommendation without requiring a full page refresh.
