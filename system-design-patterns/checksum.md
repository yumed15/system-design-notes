# Checksum

### Motivation

While moving data between components, it is possible that the data fetched from a node may arrive corrupted.

### Solution

When a system is storing some data, it computes a checksum of the data, and stores the checksum with the data. When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.

### Applications

* **S3** buckets use multipart uploading, where it splits big files into smaller pieces and uploads them one by one. After receiving all the parts, Amazon will stitch them back together. Each file on S3 gets an **ETag**, which is essentially the **md5 checksum** of that file. For multipart upload, instead of calculating the hash of the entire file, Amazon calculates the hash of each part and combines that into a single hash. The algorithm calculates the MD5 checksums corresponding to each part, takes the checksum of their concatenation and adds a hyphen and the number of parts.\
  \
  $$e.g. hexmd5( md5( part1 ) + md5( part2 ) )-{  no.parts }$$\
  \
  The validation function will calculate the ETag of the file the same way as aws's algorithm and compare it with the ETag of the file once uploaded
