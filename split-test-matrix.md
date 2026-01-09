# IDGT Fitness - Workout Split Test Matrix

## Test Date: January 8, 2026

---

## Split 1: Body Part Split

### Configuration:
- 5-day rotation: Chest-Tri, Back-Bi, Legs, Shoulders-Arms, Full Body
- Uses: `(idx % 5) + 1` to cycle through workouts

### Test Cases:

**Test 1.1: Select Mon-Fri (5 days)**
- Expected: Mon=Chest-Tri, Tue=Back-Bi, Wed=Legs, Thu=Shoulders, Fri=Full Body
- Status: ✅ PASS (proper 1:1 mapping)

**Test 1.2: Select Mon, Wed, Fri (3 days)**
- Expected: Mon=Chest-Tri, Wed=Back-Bi, Fri=Legs
- Logic: idx 0,1,2 → day1,day2,day3
- Status: ✅ PASS

**Test 1.3: Select Mon-Sat (6 days)**
- Expected: Mon=Chest-Tri, Tue=Back-Bi, Wed=Legs, Thu=Shoulders, Fri=Full Body, Sat=Chest-Tri (repeats)
- Logic: idx 5 % 5 = 0 → day1
- Status: ✅ PASS

**Test 1.4: Knee Injury + Wed leg day**
- Expected: Wednesday gets dual mode (legs/cardio toggle)
- Logic: Checks if muscleGroup includes 'Legs'
- Status: ⚠️ POTENTIAL ISSUE - Only checks if day === wednesday

---

## Split 2: Push/Pull/Legs

### Configuration:
- 3-day rotation: Push, Pull, Legs
- Uses: `(idx % 3)` to cycle through workouts

### Test Cases:

**Test 2.1: Select Mon, Wed, Fri (3 days)**
- Expected: Mon=Push, Wed=Pull, Fri=Legs
- Logic: idx 0,1,2 % 3 = 0,1,2
- Status: ✅ PASS

**Test 2.2: Select Mon-Sat (6 days)**
- Expected: Mon=Push, Tue=Pull, Wed=Legs, Thu=Push, Fri=Pull, Sat=Legs
- Logic: Cycles through push/pull/legs twice
- Status: ✅ PASS

**Test 2.3: Select Tue, Thu (2 days)**
- Expected: Tue=Push, Thu=Pull
- Logic: idx 0,1 % 3 = 0,1
- Status: ✅ PASS

**Test 2.4: Knee Injury**
- Expected: Legs days show "Legs (Modified)" with ACL-safe exercises
- Status: ✅ PASS

---

## Split 3: Upper/Lower

### Configuration:
- 2-day alternation: Upper, Lower, Upper, Lower...
- Uses: `idx % 2 === 0` to alternate

### Test Cases:

**Test 3.1: Select Mon, Wed, Fri, Sat (4 days)**
- Expected: Mon=Upper, Wed=Lower, Fri=Upper, Sat=Lower
- Logic: idx 0,2 are even (Upper), idx 1,3 are odd (Lower)
- Status: ✅ PASS

**Test 3.2: Select Mon-Fri (5 days)**
- Expected: Mon=Upper, Tue=Lower, Wed=Upper, Thu=Lower, Fri=Upper
- Status: ✅ PASS

**Test 3.3: Select Sun (1 day)**
- Expected: Sun=Upper
- Logic: idx 0 is even
- Status: ✅ PASS

---

## Split 4: Full Body

### Configuration:
- Same workout every day

### Test Cases:

**Test 4.1: Any combination of days**
- Expected: All selected days = Full Body workout
- Status: ✅ PASS

---

## Issues Found:

### Issue 1: Body Part Split - Knee Injury Dual Mode
**Location:** Line 2206-2217
**Problem:** Dual mode (legs/cardio) only activates if the day is Wednesday
```javascript
if (data.injury === 'knee' && plan[day].muscleGroup.includes('Legs')) {
```
**Impact:** If user selects a different day (e.g., Thursday) for legs, they don't get the dual mode option
**Severity:** Medium
**Fix Required:** YES

**Suggested Fix:**
Remove the hardcoded Wednesday check. Apply dual mode to ANY day that has legs workout with knee injury.

---

### Issue 2: Wednesday Dual Mode Rendering
**Location:** Line 2447 (renderWeeklySchedule)
**Problem:** Code checks `if (day === 'wednesday' && dayData.mode)`
**Impact:** Even with Issue 1 fixed, the render function still hardcodes Wednesday
**Severity:** Medium
**Fix Required:** YES

**Suggested Fix:**
Change check to: `if (dayData.mode && (dayData.legs || dayData.cardio))`

---

### Issue 3: OpenWorkout Function
**Location:** Line 2491 (openWorkout)
**Problem:** Same Wednesday hardcoding
**Impact:** Modal won't show dual mode for legs on other days
**Severity:** Medium
**Fix Required:** YES

---

## Recommendations:

1. **Remove hardcoded Wednesday checks** - Use data structure instead
2. **Check for `dayData.mode` existence** rather than day name
3. **Test with knee injury + legs on non-Wednesday days**

---

## Overall Status:

- ✅ All splits generate workouts correctly
- ✅ Cycling logic works for all day combinations
- ⚠️ Knee injury dual-mode hardcoded to Wednesday only
- ✅ Exercise functions all exist and work
- ✅ workoutType field added to all splits
- ✅ originalWorkout stored for switching

**Critical Bugs:** 0
**Medium Issues:** 3 (all related to Wednesday hardcoding)
**Low Issues:** 0

**Action Required:** Fix Wednesday hardcoding for knee injury dual-mode
