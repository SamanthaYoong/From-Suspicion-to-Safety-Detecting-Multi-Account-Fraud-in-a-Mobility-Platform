# 🛡️ From Suspicion to Safety: Detecting Multi-Account Fraud in a Mobility Platform

**Role Target**: Data Analyst – Integrity (Trust, Identity & Safety), Grab  
**Author**: Samantha Yoong  
**Focus**: Behavioral risk detection, fraud mitigation, dashboard reporting  
**Tools**: SQL · Tableau · Excel · Statistical Modeling

---

## 🎯 Objective

Simulate how a Grab Integrity Analyst detects **multi-account fraud** used to exploit referral bonuses, bypass bans, or abuse payment methods — using behavior-driven data signals, anomaly detection, and risk logic.

---

## 📦 Dataset & Assumptions

Mocked data based on typical mobility app logs:

- `users`: account creation time, signup location, device & IP
- `referrals`: who referred whom and when
- `sessions`: login timestamps, locations
- `payments`: payment method type, frequency, and risk score

---

## 🧠 Signals Tracked

| Behavior Pattern | Description |
|------------------|-------------|
| 🔁 Repetitive Referral | Same IP/device referring many users |
| 📍 Location Inconsistency | Sudden geo-switches within hours |
| 💳 Risky Payment Method | Suspicious payment modes (e.g. gift cards) |
| ⏱️ Odd Login Time | Spikes between 2AM–4AM |
| 📱 Device Overlap | Many accounts tied to same device hash |

---

## 🔍 Step-by-Step Analysis

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
