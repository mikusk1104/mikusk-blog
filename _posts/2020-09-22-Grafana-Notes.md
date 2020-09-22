---
layout: post
title:  "Grafana Notes"
date:   2020-09-22 16:00:00 +0200
categories: grafana
---
# Number of DNS requests panel

<img src="{{ site.baseurl }}/assets/img/NumberOfDNSRequests.png">

## SQL code:
```SQL
SELECT sum("value") FROM "router.k_DNS" WHERE $timeFilter GROUP BY time($interval) fill(linear)
```
## Panel JSON:
```JSON
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