# 🛡️ Erlang Fault-Tolerant Actor Model Simulation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]
[![Language: Erlang](https://img.shields.io/badge/Language-Erlang-red.svg)](https://www.erlang.org/)

## 📌 Project Overview
This project is an advanced systems architecture demonstration built in **Erlang** and hosted via Google Colab. It steps away from standard data science notebooks to showcase backend infrastructure concepts: the **Actor Model of Concurrency** and **Self-Healing Fault Tolerance**.

The application simulates an IoT Sensor Hub. It spins up multiple isolated, concurrent processes (sensors) governed by a central Supervisor. To prove the resiliency of Erlang's architecture, the script intentionally injects a fatal error into a running process to demonstrate the famous "Let it crash" philosophy in action.

## 🛠️ Concepts & Technologies Demonstrated
* **Environment Configuration:** Provisioning a native Python environment (Google Colab) via Linux subsystems to compile and execute Erlang (`.beam`) binaries.
* **The Actor Model:** Creating isolated, lightweight processes that share no memory and communicate strictly via message passing (`!` operator).
* **Fault Tolerance & Supervision Trees:** Utilizing `spawn_link` and `trap_exit` to monitor process heartbeats. When a sensor process suffers a simulated hardware failure, the supervisor catches the death signal and instantly resurrects the process without disrupting the rest of the system.

## 🏗️ Execution Flow
1. **Boot:** The master process initializes a Supervisor.
2. **Spawn:** The Supervisor spins up three distinct IoT Sensor processes, saving their Process IDs (PIDs).
3. **Telemetry:** The sensors run concurrently, transmitting telemetry data every second.
4. **Chaos Injection:** A fatal `exit(Pid, kill)` signal is sent to `Temp_Zone_B`.
5. **Recovery:** The Supervisor intercepts the crash, logs the failure, and automatically spins up a new instance of the failed sensor, returning the system to full capacity.

## 🚀 How to Run the Project
1. Open the `.ipynb` file in **Google Colab**.
2. Run **Cell 1** to install the Erlang backend via `apt-get`.
3. Run **Cell 2** to write the `sensor_hub.erl` code to the local filesystem.
4. Run **Cell 3** to compile the code (`erlc`) and execute the actor simulation (`erl -noshell`). Watch the terminal output as the system survives the injected crash!
