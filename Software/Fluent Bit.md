*[Fluent Bit](https://fluentbit.io/) is an open-source telemetry agent specifically designed to efficiently handle the challenges of collecting and processing telemetry data across a wide range of environments, from constrained systems to complex cloud infrastructures*

Telemetry data processing in general can be complex, and at scale a bit more, that's why [Fluentd](https://www.fluentd.org/) was born. Fluentd has become more than a simple tool, it has grown into a fullscale ecosystem that contains SDKs for different languages and sub-projects like [Fluent Bit](https://fluentbit.io/).


# Key Concepts

There are a few key concepts that are really important to understand how Fluent Bit operates.

- Event or Record
    Every incoming piece of data that belongs to a log or a metric that is retrieved by Fluent Bit is considered an Event or a Record.

- Filtering
    In some cases it is required to perform modifications on the Events content, the process to alter, enrich or drop Events is called Filtering.

- Tag
    Every Event that gets into Fluent Bit gets assigned a Tag. This tag is an internal string that is used in a later stage by the Router to decide which Filter or Output phase it must go through. Most of the tags are assigned manually in the configuration. If a tag is not specified, Fluent Bit will assign the name of the Input plugin instance from where that Event was generated from.

- Timestamp
    
- Match
    Fluent Bit allows to deliver your collected and processed Events to one or multiple destinations, this is done through a routing phase. A Match represent a simple rule to select Events where it Tags matches a defined rule.

- Structured Message


## Config 
Example Systemd Config 
```
[INPUT]
    Name            systemd
    Tag             systemd.*
    Systemd_Filter  _SYSTEMD_UNIT=cultivator-vision.service
    Systemd_Filter  _SYSTEMD_UNIT=metadata-client.service
    Systemd_Filter  _SYSTEMD_UNIT=x90-simulator.service
    Systemd_Filter_Type Or
    Read_From_Tail  On


[FILTER]
    Name             modify
    Match            systemd*
    Remove_regex     ^_

[FILTER]
    Name          grep
    Match         systemd*
    Regex         MESSAGE \bERROR\b

[FILTER]
    Name     throttle
    Match    *
    Rate     10
    Window   10
    Interval 1s

[OUTPUT]
    Name cloudwatch_logs
    Match systemd*
    region us-west-2
    log_group_name /machine-logs/datacart-6
    log_stream_prefix camera-0-
    auto_create_group On
    workers 1
    net.dns.resolver LEGACY

[OUTPUT]
    name  stdout
    match systemd*
```