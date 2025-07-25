# From Suspicion to Safety: Detecting Multi-Account Fraud in a Mobility Platform

**Role Target**: Data Analyst – Integrity (Trust, Identity & Safety), Grab  
**Author**: Samantha Yoong  
**Focus**: Behavioural risk detection, fraud mitigation, dashboard reporting  
**Tools**: SQL · Tableau · Excel · Statistical Modeling

🔗 [View the Interactive Tableau Dashboard](https://public.tableau.com/views/FromSuspiciontoSafetyDetectingMulti-AccountFraudinaMobilityPlatform/ExecutiveOverview?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 📊 Dashboard Preview

![Dashboard Preview](Executive-Overview.png)
---

## 🌐 Objective

Simulate how a Grab Integrity Analyst detects **multi-account fraud** used to exploit referral bonuses, bypass bans, or abuse payment methods — using behaviour-driven data signals, anomaly detection, and risk logic.

---

## 🌐 Dataset & Assumptions

Mocked data based on typical mobility app logs:

- `users`: account creation time, signup location, device & IP
- `referrals`: who referred whom and when
- `sessions`: login timestamps, locations
- `payments`: payment method type, frequency, and risk score

---

## 🌐 Signals Tracked

| Behavior Pattern | Description |
|------------------|-------------|
| 💡 Repetitive Referral | Same IP/device referring many users |
| 💡 Location Inconsistency | Sudden geo-switches within hours |
| 💡 Risky Payment Method | Suspicious payment modes (e.g. gift cards) |
| 💡 Odd Login Time | Spikes between 2 AM–4 AM |
| 💡 Device Overlap | Many accounts tied to same device hash |

---

## 🌐 Step-by-Step Analysis

### 1. Segment Referrers

```sql
SELECT 
  user_id, 
  COUNT(DISTINCT referred_user_id) AS referral_count,
  COUNT(DISTINCT device_id) AS device_count,
  COUNT(DISTINCT ip_address) AS ip_count
FROM referrals
GROUP BY user_id
HAVING referral_count > 10 AND (device_count = 1 OR ip_count = 1);
```
---

### 2. Time Series Anomaly Detection

To detect behavioral anomalies, I used **z-score analysis** to flag users who show excessive login activity between **2AM–4AM** — a typical signal for bot-like or mass abuse patterns.

> 💡 Result: Over **45%** of flagged accounts showed consistent **night-time login bursts**, a pattern almost absent in regular users.

---

### 🌐 Fraud Analyst Dashboard (Tableau)

Key components built in Tableau:

- 💡 **Risky Referral Clusters**  
  Highlight users who referred 10+ accounts with shared device/IP info

- 💡 **IP & Device Overlap Heatmap**  
  Visualize shared usage across flagged accounts

- 💡 **Login Time Distribution Chart**  
  Compare flagged vs. non-flagged login patterns across 24 hours

- 💡 **Detection Efficacy Tracker**  
  % flagged, % true positives, % false positives — updated weekly

---

### 🌐 Recommendations to Grab Integrity Team

| Action | Why |
|--------|-----|
| 💡 Block referral if IP/device match exceeds X threshold | Limits mass abuse |
| 💡 Require phone verification + device hash on sign-up | Reduces multi-account creation |
| 💡 Create alerts on “suspicious behavior clusters” | Enables early fraud detection |
| 💡 Track detection rule impact via dashboards | Ensures balance between false positives and coverage |

---

### 🌐 Strategic Impact

> “By applying behavioral and device-level data to uncover fraud signals, Grab can significantly reduce financial leakage, while reinforcing user trust.  
>  
> Integrity becomes not just a defensive function — but a strategic moat, proactively protecting growth.”

---


