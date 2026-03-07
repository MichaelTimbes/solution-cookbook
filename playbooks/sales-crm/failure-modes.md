# Sales CRM Failure Modes

- Duplicate lead conversion -> duplicate opportunities -> enforce dedupe keys.
- Stage updates outside policy -> forecast distortion -> versioned transition rules.
- Notification overload -> missed high-priority tasks -> routing and throttle policy.
- Stale billing sync -> inaccurate account status -> reconciliation and idempotent updates.
