---
layout: post
title:  "Grafana Notes"
date:   2020-09-22 16:00:00 +0200
categories: grafana
---

[<img src="{{ site.baseurl }}/assets/img/DNSDashBoard.png">]({{ site.baseurl }}/assets/img/DNSDashBoard.png)


# Number of DNS requests panel

<img src="{{ site.baseurl }}/assets/img/NumberOfDNSRequests.png">

## SQL code:
```sql
SELECT sum("value") FROM "router.k_DNS" WHERE $timeFilter GROUP BY time($interval) fill(linear)
```
## Panel JSON:
```json
{
  "aliasColors": {},
  "dashLength": 10,
  "fieldConfig": {
    "defaults": {
      "custom": {},
      "unit": "none",
      "mappings": [],
      "thresholds": {
        "mode": "absolute",
        "steps": [
          {
            "color": "green",
            "value": null
          },
          {
            "color": "red",
            "value": 80
          }
        ]
      }
    },
    "overrides": []
  },
  "fill": 1,
  "fillGradient": 1,
  "gridPos": {
    "h": 9,
    "w": 14,
    "x": 0,
    "y": 0
  },
  "id": 4,
  "legend": {
    "alignAsTable": true,
    "avg": false,
    "current": false,
    "max": false,
    "min": false,
    "rightSide": true,
    "show": false,
    "total": false,
    "values": false
  },
  "lines": true,
  "linewidth": 2,
  "nullPointMode": "null",
  "pluginVersion": "7.1.5",
  "pointradius": 0.5,
  "renderer": "flot",
  "seriesOverrides": [],
  "spaceLength": 10,
  "targets": [
    {
      "alias": "Sum of DNS requests",
      "groupBy": [
        {
          "params": [
            "$interval"
          ],
          "type": "time"
        },
        {
          "params": [
            "linear"
          ],
          "type": "fill"
        }
      ],
      "measurement": "router.k_DNS",
      "orderByTime": "ASC",
      "policy": "default",
      "refId": "A",
      "resultFormat": "time_series",
      "select": [
        [
          {
            "params": [
              "value"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "sum"
          }
        ]
      ],
      "tags": [],
      "tz": "",
      "query": "SELECT sum(\"value\") FROM \"router.k_DNS\" WHERE $timeFilter GROUP BY time($interval) fill(linear)",
      "rawQuery": false
    }
  ],
  "thresholds": [],
  "timeRegions": [],
  "title": "Number of DNS requests",
  "tooltip": {
    "shared": true,
    "sort": 0,
    "value_type": "individual"
  },
  "type": "graph",
  "xaxis": {
    "buckets": null,
    "mode": "time",
    "name": null,
    "show": true,
    "values": []
  },
  "yaxes": [
    {
      "$$hashKey": "object:457",
      "format": "none",
      "label": null,
      "logBase": 1,
      "max": null,
      "min": null,
      "show": true
    },
    {
      "$$hashKey": "object:458",
      "format": "short",
      "label": null,
      "logBase": 1,
      "max": null,
      "min": null,
      "show": false
    }
  ],
  "yaxis": {
    "align": false,
    "alignLevel": null
  },
  "bars": false,
  "dashes": false,
  "hiddenSeries": false,
  "percentage": false,
  "points": false,
  "stack": false,
  "steppedLine": false,
  "timeFrom": null,
  "timeShift": null,
  "datasource": null
}
```
# DNS Cache Size / Cache Items panel

<img src="{{ site.baseurl }}/assets/img/DNSCache.png">

## SQL code:
```sql
SELECT mean("CacheSize") FROM "router.k_DNS" WHERE $timeFilter GROUP BY time($__interval) fill(previous)
```
## Panel JSON:
```json
{
  "aliasColors": {},
  "bars": false,
  "dashLength": 10,
  "dashes": false,
  "fieldConfig": {
    "defaults": {
      "custom": {}
    },
    "overrides": []
  },
  "fill": 1,
  "fillGradient": 0,
  "gridPos": {
    "h": 8,
    "w": 14,
    "x": 0,
    "y": 9
  },
  "hiddenSeries": false,
  "id": 9,
  "legend": {
    "avg": false,
    "current": false,
    "max": false,
    "min": false,
    "show": true,
    "total": false,
    "values": false
  },
  "lines": true,
  "linewidth": 1,
  "nullPointMode": "null",
  "percentage": false,
  "pluginVersion": "7.1.5",
  "pointradius": 2,
  "points": false,
  "renderer": "flot",
  "seriesOverrides": [],
  "spaceLength": 10,
  "stack": false,
  "steppedLine": false,
  "targets": [
    {
      "alias": "Cache Size in KiB",
      "groupBy": [
        {
          "params": [
            "$__interval"
          ],
          "type": "time"
        },
        {
          "params": [
            "previous"
          ],
          "type": "fill"
        }
      ],
      "measurement": "router.k_DNS",
      "orderByTime": "ASC",
      "policy": "default",
      "refId": "A",
      "resultFormat": "time_series",
      "select": [
        [
          {
            "params": [
              "CacheSize"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "mean"
          }
        ]
      ],
      "tags": []
    },
    {
      "alias": "Cache used in KiB",
      "groupBy": [
        {
          "params": [
            "$__interval"
          ],
          "type": "time"
        },
        {
          "params": [
            "previous"
          ],
          "type": "fill"
        }
      ],
      "measurement": "router.k_DNS",
      "orderByTime": "ASC",
      "policy": "default",
      "refId": "B",
      "resultFormat": "time_series",
      "select": [
        [
          {
            "params": [
              "CacheUsed"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "mean"
          }
        ]
      ],
      "tags": []
    },
    {
      "alias": "Cache Items",
      "groupBy": [
        {
          "params": [
            "$__interval"
          ],
          "type": "time"
        },
        {
          "params": [
            "previous"
          ],
          "type": "fill"
        }
      ],
      "measurement": "router.k_DNS",
      "orderByTime": "ASC",
      "policy": "default",
      "refId": "C",
      "resultFormat": "time_series",
      "select": [
        [
          {
            "params": [
              "CacheItems"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "mean"
          }
        ]
      ],
      "tags": []
    }
  ],
  "thresholds": [],
  "timeFrom": null,
  "timeRegions": [],
  "timeShift": null,
  "title": "DNS Cache Size / Cache Items",
  "tooltip": {
    "shared": true,
    "sort": 0,
    "value_type": "individual"
  },
  "type": "graph",
  "xaxis": {
    "buckets": null,
    "mode": "time",
    "name": null,
    "show": true,
    "values": []
  },
  "yaxes": [
    {
      "format": "short",
      "label": null,
      "logBase": 1,
      "max": null,
      "min": null,
      "show": true
    },
    {
      "format": "short",
      "label": null,
      "logBase": 1,
      "max": null,
      "min": null,
      "show": true
    }
  ],
  "yaxis": {
    "align": false,
    "alignLevel": null
  },
  "datasource": null
}
```
# TOP 50 Domains panel

<img src="{{ site.baseurl }}/assets/img/Top50domains.png">

## SQL code:
```sql
SELECT TOP(sum,domain,50) FROM(SELECT sum("value")  FROM "router.k_DNS" WHERE $timeFilter GROUP BY "domain")
```
## Panel JSON:
```json
{
  "datasource": "InfluxDB",
  "fieldConfig": {
    "defaults": {
      "custom": {
        "align": "left",
        "displayMode": "auto"
      },
      "thresholds": {
        "mode": "absolute",
        "steps": [
          {
            "color": "green",
            "value": null
          },
          {
            "color": "red",
            "value": 80
          }
        ]
      },
      "mappings": [],
      "links": [
        {
          "title": "",
          "url": "/d/fs0iPJiRk/dns-specific-domain?orgId=1&var-domain=${__value.raw}"
        }
      ]
    },
    "overrides": [
      {
        "matcher": {
          "id": "byName",
          "options": "Total DNS requests"
        },
        "properties": [
          {
            "id": "custom.displayMode",
            "value": "gradient-gauge"
          }
        ]
      }
    ]
  },
  "gridPos": {
    "h": 22,
    "w": 5,
    "x": 14,
    "y": 0
  },
  "id": 2,
  "links": [],
  "options": {
    "showHeader": false
  },
  "pluginVersion": "7.1.5",
  "targets": [
    {
      "groupBy": [
        {
          "params": [
            "domain"
          ],
          "type": "tag"
        }
      ],
      "measurement": "dns",
      "orderByTime": "ASC",
      "policy": "default",
      "query": "SELECT TOP(sum,domain,50) FROM(SELECT sum(\"value\")  FROM \"router.k_DNS\" WHERE $timeFilter GROUP BY \"domain\")",
      "rawQuery": true,
      "refId": "A",
      "resultFormat": "table",
      "select": [
        [
          {
            "params": [
              "value"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "sum"
          }
        ]
      ],
      "tags": []
    }
  ],
  "timeFrom": null,
  "timeShift": null,
  "title": "TOP 50 Domains",
  "transformations": [
    {
      "id": "organize",
      "options": {
        "excludeByName": {
          "Time": true
        },
        "indexByName": {
          "Time": 0,
          "dest": 1,
          "top": 2
        },
        "renameByName": {
          "dest": "Top 3 hosts",
          "top": "Total DNS requests"
        }
      }
    }
  ],
  "type": "table"
}
```
# TOP 50 Local IPs panel

<img src="{{ site.baseurl }}/assets/img/Top50IPs.png">

## SQL code:
```sql
SELECT TOP(sum,localIP,50) FROM(SELECT sum("value")  FROM "router.k_DNS" WHERE $timeFilter GROUP BY "localIP")
```
## Panel JSON:
```json
{
  "datasource": "InfluxDB",
  "fieldConfig": {
    "defaults": {
      "custom": {
        "align": "left",
        "displayMode": "auto"
      },
      "thresholds": {
        "mode": "absolute",
        "steps": [
          {
            "color": "green",
            "value": null
          },
          {
            "color": "red",
            "value": 80
          }
        ]
      },
      "mappings": [],
      "links": [
        {
          "title": "",
          "url": "d/FFtYVamRk/dns-specific-localip?orgId=1&var-localIP=${__value.raw}"
        }
      ]
    },
    "overrides": [
      {
        "matcher": {
          "id": "byName",
          "options": "Total DNS requests"
        },
        "properties": [
          {
            "id": "custom.displayMode",
            "value": "gradient-gauge"
          }
        ]
      }
    ]
  },
  "gridPos": {
    "h": 22,
    "w": 5,
    "x": 19,
    "y": 0
  },
  "id": 7,
  "options": {
    "showHeader": false
  },
  "pluginVersion": "7.1.5",
  "targets": [
    {
      "groupBy": [
        {
          "params": [
            "domain"
          ],
          "type": "tag"
        }
      ],
      "measurement": "dns",
      "orderByTime": "ASC",
      "policy": "default",
      "query": "SELECT TOP(sum,localIP,50) FROM(SELECT sum(\"value\")  FROM \"router.k_DNS\" WHERE $timeFilter GROUP BY \"localIP\")",
      "rawQuery": true,
      "refId": "A",
      "resultFormat": "table",
      "select": [
        [
          {
            "params": [
              "value"
            ],
            "type": "field"
          },
          {
            "params": [],
            "type": "sum"
          }
        ]
      ],
      "tags": []
    }
  ],
  "timeFrom": null,
  "timeShift": null,
  "title": "TOP 50 Local IPs",
  "transformations": [
    {
      "id": "organize",
      "options": {
        "excludeByName": {
          "Time": true
        },
        "indexByName": {
          "Time": 0,
          "dest": 1,
          "top": 2
        },
        "renameByName": {
          "dest": "Top 3 hosts",
          "top": "Total DNS requests"
        }
      }
    }
  ],
  "type": "table"
}
```
