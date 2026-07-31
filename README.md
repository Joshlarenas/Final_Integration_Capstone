# Final_Integration_Capstone

# App 2 scaffold — multi-task scheduling

Scaffold level: **~70% complete**.

## What you implement

1. **Theme rename** — replace `YOURTHEME` everywhere
2. **Four task bodies** — see the comments in each `task_X()` for suggested workloads
3. **WCET measurement** — fill in `task_d` to log all four WCETs to serial periodically
4. **README defense** — see below

## README defense (graded)

Your README must include:

### Task table (mandatory)

Mean:

(over 100 iterations)

A: 36.63
B: 322.95
C: 4560.86
D: 28292.77


| Task |      Function     | Period (ms) | WCET measured (µs) | WCET + 30% margin (µs) | Deadline | Priority | Core |
|------|---------- --------|------------:|-------------------:|----------------------:|---------:|---------:|-----:|
| A    |ECG_Sample         | 10          |   37               |        48             | 10 ms    | 15       | 1    |
| B    |Arrhythmia_Detector| 20          |   324              |        421            | 20 ms    | 10       | 1    |
| C    |Alarm_Dispatch     | 40          |   4563             |        5932           | 40 ms    | 5        | 1    |
| D    | Logging           | 100         |    28687           |        37293          | 100 ms   | 2        | 1    |

### Schedulability defense

- Total utilization U = ∑ Cᵢ/Tᵢ
      A: 37/10000 = 0.0037
      B: 324/20000 = 0.0162
      C: 4563/40000 = 0.1141
      D: 28687/100000 = 0.2869
      A+B+C+D = 0.421 <= 1 

- Liu-Layland bound for n=4: U ≤ 4(2^(1/4) − 1) = 0.7568
      0.421 < 0.75 
      Therefore feasible

- If U > Liu-Layland: run response-time analysis on task D (lowest priority)
      U < Liu-Layland
      Therefore not needed

- Conclusion: feasible / infeasible / borderline. State which.

In conclusion, the tasks were feasill. This was concluded due to the total utilization being
less than the caluclated Liu-Layland value deried from the amount of tasks (n=4).

### Preemption evidence

For preemptive evidence, I actually took a different route, since I already had a limiter for the 
amount of prints I had per tick, I had the values edited to demonstrate A and D more closley. Doing this, I had
more accurate start and stop times, demonstrating preemption. In the immage I have within the files and such,
task D has a range/ time of 9967245-9995779 while task A had a time/range of 9991782-9991832. These values show
task A starting after task D started but ending before task D did, having its range completely within task D's
time/range.


### Engineering analysis

1. **Priority defense** — explain each priority. RMS says shortest period &rarr; highest priority. Did you follow it?
      For my 4 tasks, I set their priorities as A: 15, B: 10, C: 5, and D: 2 as directed by the instructions to 
      keep the logic of lowest period=highest prioritiy. This follows RMS, by keeping this rule and staying monotinic.Task A Is
      the highest prioritiy because it has the shortet period of just 10-50us. Task B is the 10 to stay behind Task
      A, but to keep its priority over task C and D, allowing for A to keep its consistency without taking away
      B's data/starving. With a period of 40ms, it allows for B and A to remain as top priorities. And finally,
      task D had the lowest priority due to it having the largest period.

2. **3× WCET stress** — if your highest-priority task's WCET tripled, what's the new U? Is the set still feasible?

      37us * 3 = 111us
      111us/10000 = 0.0111
      B: 324/20000 = 0.0162
      C: 4563/40000 = 0.1141
      D: 28687/100000 = 0.2869
      A+B+C+D = 0.425

      0.425 is still less than 0.7568, therefore YES, the set is still feasible.

3. **Preemption proof** — quote the two timestamps showing preemption.

    "I (9970) app2: ECG_sample: Start_Time=9991782 End_Time=9991832 elapsed 50us
    I (9970) app2: Logging: Start_Time=9967245 End_Time=9995779 elapsed=28534"


Source:
https://claude.ai/chat/d6245ad9-d9af-4659-8863-2087f54356cf
https://chatgpt.com/g/g-6a29682f0aec819182c6c3cef119f302-plus/c/6a2d80dc-30c0-83ea-94d9-4b4fd18b0f07

(Used old chatgpt chat to go over the calculations for utilization)
I mainly used just a single chat to build off of each question I had along with clarification.

IMAGES IN FOLDER (CONCURENCY DIAGRAM AND OUTPUT proof)
