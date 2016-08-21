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

| Service name                | Description                       | Value specification                         | DS        | Consolidation | Warning variable                           | Critical variable                          | Duplicate_foreach variable |
|-----------------------------|-----------------------------------|---------------------------------------------|-----------|---------------|--------------------------------------------|--------------------------------------------|----------------------------|
| Nginx - Waiting connections | Check current waiting connections | nginx/nginx_connections-waiting             | value     | none          | $_COLLECTD_NGINX_CONNECTIONS_WAITING_WARN$ | $_COLLECTD_NGINX_CONNECTIONS_WAITING_CRIT$ | N/A                        |
| Nginx - Requests            | Check current requests            | nginx/nginx_requests                        | value     | none          | $_COLLECTD_NGINX_REQUESTS_WARN$            | $_COLLECTD_NGINX_REQUESTS_CRIT$            | N/A                        |
| Nginx - $KEY$ processes     | Check Nginx processes             | processes-$VALUE1$/ps_count                 | processes | none          | $VALUE2$                                   | $VALUE3$                                   | _nginx_processes           |
| Nginx - Listen $KEY$        | Check listening ports             | tcpconns-$KEY$-local/tcp_connections-LISTEN | value     | none          | $VALUE1$                                   | $VALUE2$                                   | _nginx_listen              |

## Default values

    _COLLECTD_NGINX_CONNECTIONS_WAITING_WARN    50
    _COLLECTD_NGINX_CONNECTIONS_WAITING_CRIT    100
    _COLLECTD_NGINX_REQUESTS_WARN               100:
    _COLLECTD_NGINX_REQUESTS_CRIT               50:

    _nginx_listen                               80 $(1:)$$(1:)$,443 $(1:)$$(1:)$
    _nginx_processes                            Master $(nginx-master)$$(1:1)$$(1:1)$,Worker $(nginx-worker)$$(1:)$$(1:)$
