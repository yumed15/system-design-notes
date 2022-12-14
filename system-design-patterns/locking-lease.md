# Locking Lease

### Motivation

When you have multiple clients updating a file. A client first gets an exclusive (or write) lock associated with the file and then proceeds with updating the file. One problem with locking is that the lock is granted until the locking client explicitly releases it. If the client fails to release the lock due to any reason, e.g., process crash, deadlock, or a software bug, the resource will be locked indefinitely.

### Solution

Use <mark style="background-color:yellow;">**time-bound leases**</mark> to grant clients rights on resources. The client asks for a lease for a limited period of time, after which the lease expires. If the client wants to extend the lease, it can renew the lease before it expires.

\
