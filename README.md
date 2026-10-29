# Philosophers

A project from the 42 curriculum. The goal of this project is to learn the basics of threading a process and using mutexes to prevent race conditions. You will solve the classic "Dining Philosophers" problem.

## About the implementation

This implementation models the dining philosophers using threads and mutexes:

* Each philosopher is represented by a separate POSIX thread.
* The forks are represented by mutexes to prevent data races and deadlocks when multiple philosophers try to eat simultaneously.
* The simulation includes a dedicated monitor thread that continuously checks the state of the philosophers. It verifies if any philosopher has exceeded the `time_to_die` since their last meal, or if all philosophers have reached the optional required number of meals.
* A custom sleep function is implemented to ensure precise timing across different systems, avoiding the inaccuracies of standard `usleep`.

## Compilation and Usage

### 1. Compilation

To compile the project, run the `make` command in the root directory of the repository. This will generate the `philo` executable.

```bash
make
```

### 2. Usage

Run the program with the following arguments:

```bash
./philo number_of_philosophers time_to_die time_to_eat time_to_sleep [number_of_times_each_philosopher_must_eat]
```

* `number_of_philosophers`: The number of philosophers and also the number of forks.
* `time_to_die` (in milliseconds): If a philosopher didn't start eating `time_to_die` milliseconds since the beginning of their last meal or the beginning of the simulation, they die.
* `time_to_eat` (in milliseconds): The time it takes for a philosopher to eat. During that time, they will need to hold two forks.
* `time_to_sleep` (in milliseconds): The time a philosopher will spend sleeping.
* `number_of_times_each_philosopher_must_eat` (optional argument): If all philosophers have eaten at least this many times, the simulation stops. If not specified, the simulation stops when a philosopher dies.

Example:
```bash
./philo 5 800 200 200
```

## Structure

* `main.c` - Entry point, handles argument parsing and initializes the simulation structures.
* `routine.c` - Contains the lifecycle loop for each philosopher thread (eating, sleeping, thinking, and taking forks).
* `monitor.c` - Contains the logic for the separate supervisor thread that checks for death or meal fulfillment conditions.
* `run.c` - Manages the creation and joining of the philosopher threads and the monitor thread.
* `init.c` - Handles the initialization of the table, philosophers, and fork mutexes.
* `utils.c` - Provides utility functions for time management (timestamp fetching) and thread-safe console output.

## Author

* **joschmun** - *42 Student*