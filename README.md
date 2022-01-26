## Overview
**NOTE:** This project is just starting out. The information below is mostly conceptual and are my plans for this project that I have sketched out. These are subject to change and will likely change. The central idea, however, will stay the same.

Nexus is a wrapper for [left-right](https://github.com/jonhoo/left-right) that allows for multiple writers while maintaining the original reader-centric functionalities. As with any concurrency primitive that allows for many writers, nexus has to make some concessions around what a writer can do.

Nexus makes two primary concessions. Writers ought not read the values stored in the left-right primitive. Changes from different writers are not guaranteed to be ordered chronologically; however, the changes from any given writer will be chronologically ordered.

## How it Works
A nexus takes a left-right writer and dispatches "workers" which act as writers.
Each worker maintains a left-right-esque pair of operations logs to allow for lock-free reading and writing between the worker and the writer.
Each worker publishes its changes for the left-right writer to read and apply to the stored structure.
