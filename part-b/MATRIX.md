# Impact vs Effort Matrix

## Matrix

|                   | Low Effort                | High Effort                |
|-------------------|---------------------------|----------------------------|
| High Impact       | Filters, Cancellation     | Tatkal Queue, Payments     |
| Low Impact        | Seat Lock                 | PNR Dashboard              |

---

## Scoring

Impact based on:
- Users affected
- Booking flow importance

Effort based on:
- Backend complexity
- API dependencies

---

## Justifications

### Tatkal Queue — High Impact, High Effort
Affects millions daily. Requires backend queue system. Must be prioritised despite effort.

### Filters — High Impact, Low Effort
Affects all users. Mostly frontend + API fix. Quick win.

### Seat Lock — Low Impact, Low Effort
Affects fewer users. Simple backend lock system.

### PNR Dashboard — Low Impact, High Effort
Useful but not core booking. Requires multiple integrations.

### Payment — High Impact, High Effort
Financial trust issue. Complex gateway integration.

### Cancellation — High Impact, Low Effort
Prevents monetary loss. Simple UI + logic improvement.

---

## Recommended Order
1. Filters
2. Cancellation
3. Seat Lock
4. Payment
5. Tatkal Queue
6. PNR Dashboard
