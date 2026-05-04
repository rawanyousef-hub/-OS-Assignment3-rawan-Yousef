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
For Task 1, I used separate locks for each counter, which is considered fine-grained locking. I used different locks such as contextSwitchLock, completedProcessLock, and waitingTimeLock because the counters are independent. This means updating one counter does not block other counters. Fine-grained locking provides better concurrency since multiple threads can update different counters at the same time. However, it requires more code and careful management. In contrast, coarse-grained locking uses one lock for all counters, which is simpler but reduces concurrency. Since the counters are independent, fine-grained locking is the better choice in this cas.

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contextSwitchCount, completedProcessCount, and totalWaitingTime.
**Why they need protection**: 
variables are shared between multiple threads, so they need protection to avoid race conditions and incorrect values when multiple threads try to update them at the same time.
**Synchronization mechanism used**: 
 used ReentrantLock to protect each counter separately, ensuring that only one thread can update a counter at a time.
**Code snippet**:
contextSwitchLock.lock();
try {
    SharedResources.contextSwitchCount++;
} finally {
    contextSwitchLock.unlock();
}

**Justification**: 

---

### Critical Section #2: Execution Log

**What resource**: 
shared resoure is executionlog list 
**Why it needs protection**: 
because multiple threads may try to add log message at same time 
**Synchronization mechanism used**: 
i used reentrantlock to protect the execution log 
**Code snippet**:
executionLogLock.lock();
try {
    SharedResources.executionLog.add(message);
} finally {
    executionLogLock.unlock();
}
**Justification**: 
Use lock protects the shared execution log from being modified by multiple threads at the same time. This makes the logging safer and keeps the output more organized.
---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
purpose of semaphore is to control access to the resource
**Number of permits and why**: 
i use one permit because only one process should acesss the cpu 
**Where implemented**: 
the process execution method before the process start
**Code snippet**:
cpuSemaphore.acquire();
try {
    // process uses the CPU here
} finally {
    cpuSemaphore.release();
}

**Effect on program behavior**: 
The CPU semaphore prevents more than one process from using the CPU at the same time. This ensures mutual exclusion and makes the simulation behave like a single CPU system.
---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
I run the program multiple times (at least 5 times) to check if the results remain consistent in each run.

**Results**: 
The results were consistent across all runs. The number of completed processes, context switches, and waiting times remained correct and stable.

**Why synchronization is necessary**: 
(Synchronization is necessary to prevent race conditions when multiple threads access shared resources such as counters and execution logs. Without synchronization, the values could become incorrect or inconsistent because multiple threads may update the same variable at the same time.

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 
I test the program to check for possible ConcurrentModificationException by running multiple threads and updating shared data structures.
**Results**: 
No exceptions occurred during the execution of the program, which indicates that the synchronization is properly implemented.
**What this proves**: 
This prove that shared resources are safely accessed and modified, and the program avoids concurrency-related errors.
---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 
are correct total burst time, correct number of context switches, and accurate waiting time for each process.
**Actual values**: 
produced by the program matched the expected values, including total burst time, context switches, and waiting times.
**Analysis**: 
The matching results between expected and actual values confirm that the scheduling logic and synchronization mechanisms are implemented correctly.
---

### Test 4: Different Scenarios
**Scenario tested**: I test different scenarios like changing the time quantum and increasing the number of processes.
**Purpose**: 
The purpose of this test is to evaluate how the system behaves under different conditions and ensure that it still produces correct and stable results.
**Results**: 
 system handled different scenarios correctly, and the results remained consistent and logical under all tested conditions.
**What I learned**: 
I learn that changing system parameters like time quantum and number of processes can affect performance, but proper synchronization ensures that the system remains stable and correct.

## Part 5: Reflection and Learning

### What I learned about synchronization:

[I learned that synchronization is very important in multi-threaded programs to prevent race conditions and ensure data consistency. Using locks and semaphores helps control access to shared resources and avoid conflicts between threads. I also learned how improper synchronization can lead to errors such as incorrect values or program crashes.]

---

### Real-world applications:



**Example 1**: 
One real-world example is banking systems, where multiple users access and update account balances at the same time. Synchronization is needed to prevent incorrect balance updates.
**Example 2**: 
flight or hotel reservations, where multiple users try to book the same seat or room at the same time. Synchronization ensures that only one booking is processed correctly.
---

### How I would explain synchronization to others:

[ would explain synchronization as a way to organize how multiple threads access shared resources so they do not interfere with each other. For example, it is like a queue where each person waits for their turn to use something. This ensures that the system works correctly and avoids errors.
---

## Part 6: GitHub Repository Information

**Repository URL**: 
https://github.com/rawanyousef-hub/-OS-Assignment3-rawan-Yousef
**Number of commits**: 
21 commits
**Commit messages**: 
1 answer Q
2 first commit
3 Fix typo in total waiting time variable

---

## Summary

**Total time spent on assignment**: 
4 hours
**Key takeaways**: 
1. Learned how to use locks and semaphores for synchronization
2. Understood how to prevent race conditions in multi-threaded programs
3. Improved my understanding of thread coordination and resource sharing

**Most challenging aspect**: 
Understanding how to correctly use synchronization without causing errors or deadlocks
**What I'm most proud of**: 
Successfully implementing synchronization and making the program run correctly without errors
---

**End of Documentation**
