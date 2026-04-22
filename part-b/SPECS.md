# IRCTC Feature Specifications — Part B

---

## Feature Spec 1: Tatkal Virtual Queue System

### Problem Statement
From Part A (Problem 1), users face server crashes and session failures at 10:00 AM during Tatkal booking, affecting 20–40 lakh users daily. Users receive no feedback, leading to panic-clicking and failed bookings.

### Current State (from Part A)
At 10:00 AM, booking freezes, sessions expire, and users are logged out without feedback. No queue or progress indicator exists.

### Proposed Solution
Introduce a virtual queue system with queue position, wait time, and session locking.

### Proposed User Flow
1. User completes booking before 10:00
2. At 10:00 → enters queue
3. Sees queue position + wait time
4. Gets turn → redirected to payment
5. Session locked for 2 minutes
6. Completes booking

### Technical Implementation Plan
**System components:**
- Booking service, session manager

**New data:**
- queue_id, position, timestamp

**API:**
- /join-queue
- /queue-status

**Frontend:**
- Queue screen UI

**Third-party:**
- Redis, WebSockets

### Success Metrics
- Success rate: 30% → 70%
- Server crashes ↓ 80%

### Edge Cases
- Refresh → queue persists
- Payment fail → retry allowed

### Wireframe
![Tatkal Queue](../assets/wireframes/tatkal-queue.png)

---

## Feature Spec 2: Reliable Search Filters

### Problem Statement
From Part A (Problem 2), filters fail or reset, affecting all users and causing incorrect bookings.

### Current State
Filters reset on navigation and show incorrect results.

### Proposed Solution
Server-side filtering with persistent filter state.

### User Flow
1. User applies filters
2. Filters saved in URL/session
3. Results always match filters
4. Back navigation retains filters

### Technical Plan
- Server-side filtering API
- Store filters in URL params

### Metrics
- Filter failure: 40% → <5%

### Edge Cases
- Availability changes dynamically

### Wireframe
![Filters](../assets/wireframes/filters.png)

---

## Feature Spec 3: Seat Locking System

### Problem Statement
From Part A (Problem 3), seat selection resets, affecting 54K–90K users daily.

### Current State
Seat selection lost due to client-side state issues.

### Proposed Solution
Server-side seat locking for 2 minutes.

### User Flow
1. User selects seat
2. Seat locked
3. Moves to payment
4. Seat persists

### Technical Plan
- Seat lock API
- Lock expiry system

### Metrics
- Seat reset rate: 30% → <5%

### Edge Cases
- Lock expires

### Wireframe
![Seat Lock](../assets/wireframes/seat-lock.png)

---

## Feature Spec 4: PNR Journey Dashboard

### Problem Statement
From Part A (Problem 4), PNR page lacks real-time info.

### Current State
Shows only static booking data.

### Proposed Solution
Convert into full journey dashboard.

### User Flow
1. User enters PNR
2. Sees:
   - train status
   - platform
   - chart status
   - coach position

### Technical Plan
- NTES API integration

### Metrics
- Reduce external site usage by 70%

### Edge Cases
- Data unavailable → fallback message

### Wireframe
![PNR Dashboard](../assets/wireframes/pnr-dashboard.png)

---

## Feature Spec 5: Real-Time UPI Payment Status

### Problem Statement
From Part A (Problem 5), UPI payments hang or show false failure.

### Current State
No real-time update after payment approval.

### Proposed Solution
Polling + webhook-based payment status updates.

### User Flow
1. User pays via UPI
2. Page shows "Checking payment"
3. Auto updates to success/failure

### Technical Plan
- Payment status polling API

### Metrics
- False failures: 8% → <1%

### Edge Cases
- Payment delayed

### Wireframe
![Payment](../assets/wireframes/payment-status.png)

---

## Feature Spec 6: Smart Cancellation + TDR Assistant

### Problem Statement
From Part A (Problem 6), users lose money due to TDR confusion.

### Current State
Cancellation and TDR flows are separate.

### Proposed Solution
Smart modal suggesting TDR when eligible.

### User Flow
1. User clicks cancel
2. System detects delay
3. Suggests TDR
4. Shows refund comparison

### Technical Plan
- Train delay API integration

### Metrics
- Wrong cancellations ↓ 50%

### Edge Cases
- Delay data unavailable

### Wireframe
![TDR](../assets/wireframes/cancellation-tdr.png)
