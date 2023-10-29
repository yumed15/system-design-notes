# Change Data Capture (CDC)

_= the process of identifying and capturing changes as they are made in a database or source application, then delivering those changes in real time to a downstream process, system, or data lake._

### CDC Patterns

Time-based - Tracks “LAST\_UPDATED” and “DATE\_MODIFIED” columns. This method only retrieves changed rows, and requires significant CPU resources to scan all the tables.

Trigger-based - Triggers are set off before or after commands that indicate a change. This produces a change log. With this method, each table in the source database requires a trigger, straining the system.

Table differencing-based - Executes a diff to compare source and target tables. This will only load the data that differs. This method is more comprehensive than timestamps, but still places a big burden on the CPU.

Log-based - Database logs are constantly scanned to detect changes.
