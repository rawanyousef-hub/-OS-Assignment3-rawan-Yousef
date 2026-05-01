# Assignment 3 - Complete Documentation

**Student Name**: [Your Full Name]  
**Student ID**: [Your ID]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [ appril 29, 4:00 pm]
**i add my student id in the code and explore the projrct **: 

** i don't nokw where to start the tood**: 

** read the readme file **: 

**run the program to make sure its work **: 

**45min**: 

---

### Entry 2 - [april 29, 5:00]
**add reentratlock to protect shared variable like contextswitchcount**: 

**how use lock and unlock**: 

** see example in readme and use try finally **: 

**test the program without error**: 

**30min**: 

---

### Entry 3 - [april 29, 2:00pm ]
**add semaphore to control cpu access and use it in the process execution method **: 

**i made some mistake  in the name method like acquir eand release**: 

** coorect the syntax error **: 

**run the simulation h**: 

**40 min**: 

---

### Entry 4 - [Date, Time]
**What I implemented**: 

**Challenges encountered**: 

**How I solved it**: 

**Testing approach**: 

**Time spent**: 

---

### Entry 5 - [Date, Time]
**What I implemented**: 

**Challenges encountered**: 

**How I solved it**: 

**Testing approach**: 

**Time spent**: 

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:

[ race condition hapen with share counter like contextswitchcount and completedprocesscount the variable are share between threads and if two threads update them at the same time one update may be lost for example if two processes execute cntextswitchcounter++ at the same time the final value may increase 1 of 2 another race condition can hapen with executionlog because arraylist and multiple thread may add messages at the same time it can be incorrect log]

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:

[reentrantlock used to protect critical section  only one thread can update share data at time i use reentranlock to protect the counter and execution  log because this share resource should't modified by multiple thread at the same time ,semaphore control how manny threads can access resource i use binary semaphore with one permit to control cpu  access , onlyonly one proceess can execute on yhe cpu at the time .]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

[[Deadlock happen  when the  threads waiting for each other forever and none of them can continue One prevention technique is using try-finally blocks, because the lock or semaphore always be released even if error happens Another technique is avoid holding multiple locks at the same time  In my code, I used finally to call unlock() or release() after the critical section. This helps prevent deadlock because resources are not left locked..]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

[For Task 1 I use separate locks for each counter  is fine-grained locking. I use contextSwitchLock, completedProcessLock, and waitingTimeLock because the three counters are independent. This means updating one counter doesn't need to block another counter. Fine-grained locking gives better concurrency because different threads can update different counters at the same time. Coarse-grained locking uses one lock for all counters, and it is simpler, but it reduces concurrency. The trade-off is that fine-grained locking needs more code, while coarse-grained locking is easier to manage. Since the counters are independent, fine-grained locking is the better choice here..]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 

**Why they need protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #2: Execution Log

**What resource**: 

**Why it needs protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 

**Number of permits and why**: 

**Where implemented**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Effect on program behavior**: 

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)

**Conclusion**: 

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
