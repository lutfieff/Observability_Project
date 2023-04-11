## Main steps

1. Deploy and setting up Observability (Helm 3.x, Grafana, Prometheus, Jaeger, Cluster Wide Jaeger).
2. Deploy a sample application in Kubernetes cluster.
3. Document the project in a README.

## Verify the monitoring installation

![Cluster resources](./docs/images/monitoringinstallation1.png)
![Cluster resources](./docs/images/monitoringinstallation2.png)

## Setup the Jaeger and Prometheus source

![Grafana](./docs/images/grafana.png)

## Create a basic dashboard

![Prometheus Dashboard](./docs/images/prometheusdashboard.png)

## Describe SLO/SLI

Suppose that these are our SLOs for *monthly uptime* and *request response time*:
1. 99.99% uptime in the year.
2. 95% of requests completed in < 100 ms.

We can describe SLIs as:
1. We got 99.98% uptime in the current year.
2. 94% of the requests were completed in < 100 ms.

## Creating SLI metrics

1. **Number of error responses in a period of time** - This metric could help us to identify possible bootlenecks and bugs.
2. **The average time taken to return a response** - This metric could help us to identify opportunities to tune our services performance.
3. **The average time taken recover a service if it goes down** - This metric could help us to measure our capacity to recover possible failovers.
4. **Total uptime in a period of time** - This metric could help us to measure the health of our services.
5. **Average percentage of memory or CPU used by a service in a period of time** - This metric could help us to measure the impact of our services in the costs of maintaining a system and look for efficient services.

## Create a dashboard to measure our SLIs

![SLIs panel](./docs/images/panel1.png)
![SLIs panel](./docs/images/panel2.png)

## Tracing our Flask app

![Jaeger UI](./docs/images/backendtracing.png)

## Jaeger in dashboards

![Grafana tracing panel](./docs/images/tracingpanel.png)

## Report error

```markdown
**TROUBLE TICKET**

**Name**: Franky River
**Date**: 09/27/2021 5:15:10 PM
**Subject**: Front-end service is creating many 40x and 50x errors
**Affected Area**: API requests
**Severity**: High

**Description**:
The `static/js/click.js` file is not handling clicks correctly and requests can not be processed because the
fetch url are not right.
```

## Creating SLIs and SLOs

SLIs:
1. We got less than 10 error responses in the last 24 hours.
2. We got an average response time of < 2000ms per minute.
3. We got 75% more successful responses than errors.
4. 99% of our responses had the right data format.

SLO:
1. 99.9% uptime per month.
2. 99.9% of responses to our front-service will return 2xx, 3xx or 4xx HTTP code within 2000 ms.
3. 99.99% of transaction requests will succeed over any calendar month.
4. 99.9% of backend service requests will succeed on their first attempt.

## Building KPIs for our plan

1. We got less than 10 error responses in the last 24 hours.
    + Successful requests per minute:  this KPI indicates how well is performed our system.
    + Error requests per minute: this KPI is an analogous of this SLI.
    + Uptime - this KPI indicates if errors are comming from downtime or not.
2. We got an average response time of < 2000ms in the las 24 hours.
    + Average response time:  this KPI is an analogous of this SLI.
    + Uptime - this KPI will help us to determine if response time is affected by downtime of a service.
3. We got 75% more successful responses than errors.
    + Successful requests per minute:  this KPI indicates the number of successful request.
    + Error requests per minute: this KPI indicates the number of error requests.

## Final dashboard

![KPI monitoring dashboard](./docs/images/finaldashboard1.png)
![KPI monitoring dashboard](./docs/images/finaldashboard2.png)

+ Application stats panel - This panel shows information about the application services.
+ Successful requests per minute - This panel shows the total number of successful requests per service.
+ Error requests per minute - This panel shows the total number of 40x and 50x error requests per service.
+ Average response time per minute - This panel shows the average response time successful requests (status 200) per service.
+ Average memory used per minute - This panel shows the average memory used by each service.
+ Average CPU used per minute - This panel shows the average CPU used by each service.
+ Network I/O Pressure - This panel shows the amount of I/O operations per minute in the node.