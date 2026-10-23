# State Management App

A simple Flutter app that shows how state management works using `setState`.
The app has a counter that changes when the user taps a button.

## Features
- Increase the counter with the green + button
- Decrease the counter with the red - button (it cannot go below 0)
- Reset the counter to 0 with the grey refresh button
- The number is grey when it is 0 and purple when it is higher
- The message changes from "Tap a button to get started" to "Keep counting!"

## How it works
- `CounterScreen` is a `StatefulWidget`
- The counter value is stored in the variable `_counter`
- Each button calls `setState()` so the screen updates right away
- The counter is stored only in memory, so it goes back to 0 when the app is closed and opened again

## How to run
1. Run `flutter pub get`
2. Run `flutter run`

---

# Module 3 - Lesson 2: Local Storage and Database Operations

## Analysis (Activity with in-memory list)

**1. What happened to the task titles when you added them to the list?**
They were added to the list and showed on the screen.

**2. Why could the application display the tasks while it was running?**
The list was stored in memory (RAM), and the app can read memory while it is running.

**3. What happened after the application process ended and the application was relaunched?**
The tasks were gone. The list was empty again.

**4. Would keeping the list inside a StatefulWidget automatically make the tasks persistent?**
No. A StatefulWidget only keeps the data while the app is running. When the app closes, the data is lost.

**5. What would the application need to do to preserve the tasks between sessions?**
It needs to save the tasks to persistent storage, like a SQLite database or a file, and load them again when the app opens.

**6. If the app stored hundreds or thousands of tasks, what problems might arise from managing all the data manually in memory?**
- The app would use more memory and get slower.
- Searching, changing, and deleting tasks by hand would be hard.
- The data would still be lost when the app closes.

**7. How could separating the operations that save and retrieve tasks from the UI make the application easier to maintain?**
The database code would be in one place, so the UI stays clean. If the database changes, you fix it in one file instead of many screens.

## Reflection (Local Task Manager)

**1. Why does the application use SQLite instead of relying only on a Dart list?**
A Dart list is stored in memory, so it is erased when the app closes. SQLite saves the tasks in a file on the device, so they are still there when the app is opened again.

**2. What is the purpose of the primary key in the tasks table?**
The primary key (`id`) gives every task its own unique number. Even if two tasks have the same title, the app can still tell them apart.

**3. How does the repository simplify the UI's interaction with the database?**
The UI only calls simple methods like `create()`, `getAll()`, `markCompleted()`, and `delete()`. It does not need to know any SQL.

**4. What would happen if a task were removed from the displayed list but not deleted from SQLite?**
The task would look deleted, but its record would still be in the database. It would come back when the tasks are loaded again.

**5. If the database schema later needed a new column for task priority, what parts of the application might need to change?**
- The `CREATE TABLE` statement
- The database version and an `onUpgrade` migration
- The repository
- The UI
