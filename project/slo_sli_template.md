# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability |Total number of successful requests / total number of requests  | 99%                                                                                                         |
| Latency      | Response time of requests in a histogram showing the 90th percentile over the least 30 seconds   | 90% of requests below 100ms                    |
| Error Budget | The percentage of the remaining error budget                  | Error budget is defined at 20%.                |
| Throughput   |Total number of requests over a 1 second period of time    | 5 RPS indicates the application is functioning                                                              |
