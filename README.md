# prometheus_cloudwatch_exporter

Master: [![Build Status](https://travis-ci.org/sansible/prometheus_cloudwatch_exporter.svg?branch=master)](https://travis-ci.org/sansible/prometheus_cloudwatch_exporter)
Develop: [![Build Status](https://travis-ci.org/sansible/prometheus_cloudwatch_exporter.svg?branch=develop)](https://travis-ci.org/sansible/prometheus_cloudwatch_exporter)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags) 
* [Examples](#examples)

This role installs Prometheus AWS CloudWatch Exporter.

Prometheus AWS CloudWatch Exporter makes available AWS CloudWatch metrics for collection by Prometheus server.

For more information about Prometheus AWS CloudWatch Exporter please visit:
[http://github.com/prometheus/cloudwatch_exporter](https://github.com/prometheus/cloudwatch_exporter).

For more information about Prometheus Server please visit:
[https://prometheus.io](https://prometheus.io).


## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your 
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```

## Installation and Dependencies 

This role will install `sansible.users_and_groups` for managing `prometheus_cloudwatch_exporter` user
and `sansible.java` to install Java, which the Prometheus AWS CloudWatch Exporter requires to run.

To install run `ansible-galaxy install sansible.prometheus_cloudwatch_exporter` or add this to your
`roles.yml`.

```YAWL
- name: sansible.prometheus_cloudwatch_exporter
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`


## Tags 

This role uses tags: **build** and **configure** 

* `build` - Installs Prometheus AWS CloudWatch Exporter and all it's dependencies.
* `configure` - Configures Prometheus AWS CloudWatch Exporter.


## Examples

Simply include the role in your playbook.

Default exporter port: 9106

```YAML
- name: Install and configure prometheus_cloudwatch_exporter
  hosts: "somehost"
  
  roles:
    - role: sansible.prometheus_cloudwatch_exporter
      sansible_prometheus_cloudwatch_exporter:
        config:
          region: eu-west-1
          metrics:
            - aws_namespace: AWS/ELB
              aws_metric_name: RequestCount
              aws_dimensions: [AvailabilityZone, LoadBalancerName]
              aws_dimension_select:
                LoadBalancerName: [myLB]
              aws_statistics: [Sum]
