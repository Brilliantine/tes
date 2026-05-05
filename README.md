Running in system-mode.                            
                                                   
Usage logger disabled                               builds=0 max_builds=1
Configuration loaded                                builds=0 max_builds=1
WARNING: CONFIGURATION: Long polling issues detected.
Issues found:
  - Request bottleneck: 1 runners have request_concurrency=1, causing job delays during long polling
This can cause job delays matching your GitLab instance's long polling timeout.
Recommended solutions:
  1. Increase 'request_concurrency' to 2-4 for 1 runners currently using request_concurrency=1
Note: The 'FF_USE_ADAPTIVE_REQUEST_CONCURRENCY' feature flag can help automatically adjust request_concurrency based on workload.
This message will be printed each time the configuration is reloaded if the issues persist.
See documentation: https://docs.gitlab.com/runner/configuration/advanced-configuration.html#long-polling-issues  builds=0 max_builds=1
listen_address not defined, metrics & debug endpoints disabled  builds=0 max_builds=1
[session_server].listen_address not defined, session endpoints disabled  builds=0 max_builds=1
Initializing executor providers                     builds=0 max_builds=1
ERROR: Checking for jobs... client error            correlation_id=6289dfef951a473dab787a28584db634 runner=y1_rnE34d runner_name=docker-kvm-runner status=get client: new client: only http or https scheme supported
ERROR: Checking for jobs... client error            correlation_id=2d235135025d4051917b31d8f0dd90bb runner=y1_rnE34d runner_name=docker-kvm-runner status=get client: new client: only http or https scheme supported
ERROR: Checking for jobs... client error            correlation_id=e5ee34e621224218bbd88d963f1d3652 runner=y1_rnE34d runner_name=docker-kvm-runner status=get client: new client: only http or https scheme supported
ERROR: Runner "172.18.0.2y1_rnE34d" is unhealthy and will be disabled for 1h0m0s seconds!  unhealthy_requests=3 unhealthy_requests_limit=3
