# Change Data Capture (CDC)

_= the process of identifying and capturing changes as they are made in a database or source application, then delivering those changes in real time to a downstream process, system, or data lake._

### CDC Patterns

**Time-based** - Tracks “LAST\_UPDATED” and “DATE\_MODIFIED” columns. This method only retrieves changed rows, and requires significant CPU resources to scan all the tables.

**Trigger-based** - Triggers are set off before or after commands that indicate a change. This produces a change log. With this method, each table in the source database requires a trigger, straining the system.

<figure><img src="../.gitbook/assets/image (7).png" alt="" width="375"><figcaption></figcaption></figure>

**Table differencing-based** - Executes a diff to compare source and target tables. This will only load the data that differs. This method is more comprehensive than timestamps, but still places a big burden on the CPU.

**Log-based** - Database logs are constantly scanned to detect changes.



### Log Based CDC Flow

1. **Transaction Logs:** In a database management system (DBMS), transaction logs are used to record every change made to the database. These logs include records of insertions, updates, deletions, and other changes.
2. **Capture Agent:** The Log-Based CDC process starts with a Capture Agent. This agent connects to the transaction logs of the source database. It reads the logs continuously or periodically, depending on the system's configuration.
3. **Log Parsing:** The Capture Agent parses the transaction logs to extract information about the changes that occurred. This includes details such as the table affected, the type of operation (insert, update, delete), the affected rows, and the data values before and after the change.
4. **Change Events:** Once the changes are parsed and identified, they are converted into change events. Each change event represents a single data modification operation.
5. **Propagation:** These change events are then propagated to a target system or downstream consumers. This can include data warehouses, data lakes, other databases, or applications. The propagation can happen in real-time, near real-time, or in batch, depending on the use case and requirements.
6. **Data Transformation:** In some cases, the captured change events may need to be transformed before they are applied to the target system. For example, the format of data may need to be modified, or certain columns may need to be filtered or enriched.
7. **Target System:** In the target system, the captured changes are applied. The data in the target system is updated to reflect the changes that occurred in the source system.
8. **Conflict Resolution:** Depending on the configuration and system requirements, Log-Based CDC solutions may implement conflict resolution mechanisms to handle situations where the same data is updated simultaneously in the source and target systems.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Log Based CDC Flow</p></figcaption></figure>

Key Advantages of Log-Based CDC:

1. **Near Real-Time**: Log-Based CDC provides near real-time data replication. As soon as a change is committed to the source system, it can be captured and propagated to the target system.
2. **Low Overhead**: Reading transaction logs is a low-impact operation on the source database. It doesn't place a heavy load on the system compared to other methods like polling for changes.
3. **Supports All Data Types**: Log-Based CDC can capture changes to all data types, including structured and unstructured data.
4. **Complete History**: Transaction logs store a complete history of changes, enabling accurate and comprehensive replication of data.
5. **Data Integrity**: Because Log-Based CDC captures changes at the database level, it ensures data integrity and consistency in the target system.
6. **Minimal Latency**: There is minimal latency in data replication because change events are captured as soon as they occur.



Resources:

* [Change Data Capture (CDC): What it is and How it Works?](https://dbconvert.com/blog/change-data-capture-cdc-what-it-is-and-how-it-works/)
