---
 title: include file
 description: include file
 ms.topic: include
 ms.custom: include file
 services: time-series-insights
 ms.service: time-series-insights
 author: kingdomofends
 ms.author: adgera
 ms.date: 04/29/2019
---

## Business disaster recovery

This section describes features of Azure Time Series Insights that keep apps and services running even if a disaster occurs (**business disaster recovery**).

### High availability

As an Azure service, Time Series Insights provides certain **high availability** features using redundancies at the Azure region level. For instance, Microsoft Azure supports disaster recovery capabilities through Azure's **cross-region availability** feature.

Additional high availability features provided through Azure (and also available to any Time Series Insights instance) include:

1. **Failover**: Azure provides [geo-replication and loading balancing](https://docs.microsoft.com/azure/architecture/resiliency/recovery-loss-azure-region).
1. **Data restoration** and **storage recovery**: Azure provides [several options to preserve and recover data](https://docs.microsoft.com/azure/architecture/resiliency/recovery-data-corruption).
1. **Site Recovery** features through [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/).

Make sure to enable these Azure features to provide global, cross-region, high availability for your devices and users.

> [!NOTE]
> If Azure is configured to enable **cross-region availability**, no additional cross-region availability configuration is required within Azure Time Series Insights.

### IoT and Event hubs

Some Azure IoT services also include built-in business disaster recovery features:

1. [IoT Hub high-availability disaster recovery](https://docs.microsoft.com/azure/iot-hub/iot-hub-ha-dr) including intra-region redundancy.
1. [Event Hub policies](https://docs.microsoft.com/azure/event-hubs/event-hubs-geo-dr).
1. [Azure Storage redundancy](https://docs.microsoft.com/azure/storage/common/storage-redundancy).

Integrating Time Series Insights with these other services provides additional disaster recovery opportunities. For instance, telemetry sent to your Event Hub might be persisted to a backup Azure Blob Storage database.

### Time Series Insights

There are several ways to keep your Time Series Insights data, apps, and services running even if they're disrupted. You might also determine that a complete, duplicate, backup copy of your Azure Time Series environment is required:

1. As a Time Series Insights-specific **failover instance** to redirect data and traffic to.
1. For auditing and data preservation purposes.

In general, the best way to duplicate a Time Series Insights environment is to create a second Time Series Insights environment in a backup Azure region. Events are also sent to this secondary environment from your primary event source. Make sure to use a second, dedicated, consumer group and to follow that source's business disaster recovery guidelines (provided above).

Specifically, to create a duplicate environment:

1. Create an environment in a second region ([Create a new Time Series Insights environment in the Azure portal](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-get-started)).
1. Create a second dedicated consumer group for your event source.
1. Connect that event source to the new environment making sure to designate the second, dedicated consumer group.
1. Review the Time Series Insights [IoT Hub](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-how-to-add-an-event-source-iothub) and [Event hub](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-data-access) documentation.

Finally:

* If your primary region is affected during a disaster incident, reroute operations to the backup Time Series Insights environment.
* Use your second region to back up and recover all Time Series Insights telemetry and query data.

> [!IMPORTANT]
> * Note that a delay might be experienced in the event of a failover.
> * Failover might also cause a momentary spike in message processing as operations are rerouted.
> * For more information, see [Mitigate latency in Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-environment-mitigate-latency).