# What’s the Difference Between Latency and Response Time?

- Latency is the duration that a request is waiting to be handled – during which it is latent, awaiting service. Latency measurements are used for diagnostic purposes, for example, latency spikes.
- Response time is the time between a client sending a request and receiving a response. It is the sum of round trip latency and service time. It is used to describe the performance of an application.

**Latency refers to the delay in the system, while response time includes both the delays and the actual processing time**. There are many types of latency. Network latency measures the time it takes for a request to reach the server, plus the time it takes for the response to return to the client. Storage latency includes the time it takes to write the data into a database or SSD. In general, response time measures the end-to-end network transaction from the perspective of a client application, while latency is the ‘travel time’, which excludes processing time.

## How To Measure API Latency vs. Response Time?

API latency is the time the data spends in transit between computers. That time has a lot to do with the physical distance between computers, the bandwidth, and the connection quality. Response Time includes latency, of course, but it also includes the time that the server takes to fulfill the request. The response time of an API can be measured from the client and averaged to compute an average response time latency. To measure network latency from the client side, ping an endpoint to eliminate the processing time delay. Subtracting the average ping response time from the average response time gives the average processing time.

Latency is typically calculated in the 50th, 90th, 95th, and 99th percentiles. These are commonly referred to as p50, p90, p95, and p99. Percentile-based metrics can be used to expose the outliers that constitute the ‘long-tail’ of performance. Measurements of 99th (“p99”) and above are considered measurements of ‘long-tail latency’.

A p50 measurement, for example, measures the median performance of a system. Imagine 10 latency measurements: 1, 2, 5, 5, 18, 25, 33, 36, 122, and 1000 milliseconds (ms). The p50 measurement is 18 ms. 50% of users experienced that latency or less. The p90 measurement is 122, meaning that 9 of the 10 latencies measured less than 122.

Percentile-based measurements can easily be misinterpreted. For example, it is a mistake to assume that ‘p99” means that only 1% of users experience that set of latencies. In fact, p99 latencies can easily be experienced by 50% or more end users interacting with the system. So p99 (and higher) outlier latencies can actually have a disproportionate effect on the system as a whole.
