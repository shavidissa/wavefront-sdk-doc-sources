# RED Metrics

To provide full [3D Observability](https://www.wavefront.com/wavefront-enhances-application-observability-with-distributed-tracing/) for your application, the `WavefrontTracer` collects and reports RED metrics based on the tracing spans it generates from your application. RED metrics are measures of:

* Requests – the number of requests being served per second.
* Errors – the number of failed requests per second.
* Duration – per-minute histogram distributions of the amount of time that each request takes.

The `WavefrontTracer` derives the RED metrics from your spans automatically, with no additional configuration or instrumentation on your part. To visualize the out-of-the-box metrics and histograms in the default Wavefront Service Dashboard:

1. Select **Applications -> Service Dashboard** in the Wavefront taskbar. 
1. Use the filters to find your application and its services.

The Service Dashboard displays the derived RED metrics for a service in these auto-generated charts: Request Rate, Error Rate, Duration (P95), Top Requests, Top Failed Requests, and Slowest Requests.

The following table shows the name and type of the RED metrics that the Wavefront Tracer derives from your spans:

| Metric Name       | Metric Type | Description       |
| ----------------- | ----------- | ----------------- |
| `tracing.derived.<application>.<service>.<operationName>.invocation.count`        | Delta counter            | The number of times that the operation is invoked. |
| `tracing.derived.<application>.<service>.<operationName>.error.count`             | Delta counter            | The number of invocations that are errors (i.e., spans with `error=true`). |
| `tracing.derived.<application>.<service>.<operationName>.duration.micros.m`       | Wavefront histogram | The duration of each operation invocation, in microseconds, aggregated in one-minute intervals. |

Each RED metric name includes values (`<application>`, `<service>`, and `<operationName>`) obtained from the corresponding spans. If necessary, these values are modified to comply with Wavefront's metric name format.

Each RED metric has point tags (`application`, `service`, and `operationName`) with values obtained from the corresponding spans. The span values are  assigned to the point tags without being modified. Consequently, we recommend that you query the derived RED metrics using the point tags instead of metric names. 

## Where to Go Next

To continue, select one of the [Wavefront SDKs](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources#wavefront-sdks).
