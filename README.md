# 🍝 Philosophers - Eat, Sleep, Die, Repeat

This project is a training exercise for multi-threading and process synchronization. It explores the **Dining Philosophers Problem**, focusing on resource sharing and avoiding deadlocks.

---

## 🧐 The Problem

Philosophers sit around a circular table with a bowl of spaghetti in the center.
- **Mandatory (Threads & Mutexes):** Each philosopher is a thread. Forks are protected by individual mutexes.
- **Bonus (Processes & Semaphores):** Each philosopher is a process. Forks are represented by a global semaphore.

The challenge is to ensure that no philosopher starves by carefully managing the timing and access to forks.

---

## 🛠️ Key Concepts

- **Threads/Processes:** Managing concurrent execution.
- **Mutexes/Semaphores:** Synchronizing access to shared resources and preventing Data Races.
- **Deadlocks:** Preventing the state where everyone is waiting and no one can act.
- **Memory Safety:** Ensuring clean exits and no leaks using `pthread_join` or `sem_close`.

---

## 📊 Parameters

The program accepts the following arguments:

1. `number_of_philosophers`: The number of philosophers and forks.
2. `time_to_die` (ms): Time limit to start eating before starving.
3. `time_to_eat` (ms): Duration of the eating action.
4. `time_to_sleep` (ms): Duration of the sleeping action.
5. `[number_of_times_each_philosopher_must_eat]`: (Optional) Target meal count to stop simulation.

---

## 💻 Usage

### Mandatory Part (Threads)
```bash
cd philo && make
./philo 5 800 200 200
```

### Bonus Part (Processes)
```bash
cd philo_bonus && make bonus
./philo_bonus 5 800 200 200
```
---

## 🛡️ Debugging & Safety (Thread Sanitizer)
To ensure there are no Data Races or Deadlocks, the project must be tested with the Thread Sanitizer. This is a crucial step for the 42 evaluation.

Add the following flag to your `CFLAGS` in the `Makefile`:

```Makefile

CFLAGS += -fsanitize=thread -g3
```
*Note: You can also use `-fsanitize=address` to check for memory leaks and buffer overflows.*

---

## ⚠️ Important Rules
No global variables allowed in the mandatory part.

**Time Precision**: Standard `usleep` can be imprecise. Implementing a custom accurate sleep function is highly recommended.

**Clean Exit**: All mutexes must be destroyed and semaphores unlinked upon termination.
