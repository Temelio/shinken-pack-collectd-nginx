# shinken-pack-collectd-nginx

## Description

This Shinken monitoring pack is used to manage nginx services with our standard
deployment of Collectd.

We request Collectd data using unixsock plugin and collectd-nagios script from
collecd-utils package.

This pack depends to shinken-pack-collectd-base to work

## Objects

### Templates

#### Host templates

* collectd-nginx: Manage all default thresholds and values for services

### Services

| Service name                | Description                       | Value specification             | DS        | Consolidation | Warning variable                           | Critical variable                          | Duplicate_foreach variable |
|-----------------------------|-----------------------------------|---------------------------------|-----------|---------------|--------------------------------------------|--------------------------------------------|----------------------------|
| Nginx - waiting connections | Check current waiting connections | nginx/nginx_connections-waiting | value     | none          | $_COLLECTD_NGINX_CONNECTIONS_WAITING_WARN$ | $_COLLECTD_NGINX_CONNECTIONS_WAITING_CRIT$ | N/A                        |
| Nginx - requests            | Check current requests            | nginx/nginx_requests            | value     | none          | $_COLLECTD_NGINX_REQUESTS_WARN$            | $_COLLECTD_NGINX_REQUESTS_CRIT$            | N/A                        |
| $KEY processes              | Check Nginx processes             | processes-$VALUE1$/ps_count     | processes | None          | $VALUE2$                                   | $VALUE3$                                   | _nginx_processes           |

## Default values

    _COLLECTD_NGINX_CONNECTIONS_WAITING_WARN    50
    _COLLECTD_NGINX_CONNECTIONS_WAITING_CRIT    100
    _COLLECTD_NGINX_REQUESTS_WARN               100:
    _COLLECTD_NGINX_REQUESTS_CRIT               50:

    _nginx_processes                            nginx-master $(nginx-master)$$(1:1)$$(1:1)$,nginx-worker $(nginx-worker)$$(1:)$$(1:)$
