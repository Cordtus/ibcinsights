# ibcinsights
lightweight IBC packet monitoring dashboard

requires [ChainPulse](https://github.com/informalsystems/chainpulse) for database & metrics exporter


prometheus job example
```
- job_name: 'IBC insights'
scrape_interval: 5s
metrics_path: '/metrics'
static_configs:
- targets: ['10.114.28.180:3000']
relabel_configs:
- source_labels: [__name__, chain_id, src_chain, dst_chain, src_channel, dst_ch>
regex: 'ibc_effected_packets;(.+);(.+);(.+);(.+)'
action: keep
- source_labels: [__name__, chain_id, src_chain, dst_chain, src_channel, dst_ch>
regex: 'ibc_uneffected_packets;(.+);(.+);(.+);(.+)'
action: keep
- source_labels: [__name__, chain_id, src_chain, dst_chain, src_channel, dst_ch>
regex: 'ibc_stuck_packets;(.+);(.+);(.+)'
action: keep
- action: labeldrop
regex: 'memo'
```


dashboard baseplate
```
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": {
          "type": "datasource",
          "uid": "grafana"
        },
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "target": {
          "limit": 100,
          "matchAny": false,
          "tags": [],
          "type": "dashboard"
        },
        "type": "dashboard"
      }
    ]
  },
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "id": 76,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "datasource": "${DS_PROMETHEUS}",
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "palette-classic"
          },
          "custom": {
            "axisCenteredZero": false,
            "axisColorMode": "text",
            "axisLabel": "",
            "axisPlacement": "auto",
            "barAlignment": 0,
            "drawStyle": "line",
            "fillOpacity": 10,
            "gradientMode": "none",
            "hideFrom": {
              "legend": false,
              "tooltip": false,
              "viz": false
            },
            "lineInterpolation": "linear",
            "lineWidth": 1,
            "pointSize": 5,
            "scaleDistribution": {
              "type": "linear"
            },
            "showPoints": "never",
            "spanNulls": false,
            "stacking": {
              "group": "A",
              "mode": "none"
            },
            "thresholdsStyle": {
              "mode": "off"
            }
          },
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
          },
          "unit": "short"
        },
        "overrides": []
      },
      "gridPos": {
        "h": 11,
        "w": 18,
        "x": 0,
        "y": 0
      },
      "id": 1,
      "options": {
        "legend": {
          "calcs": [],
          "displayMode": "list",
          "placement": "bottom",
          "showLegend": true
        },
        "tooltip": {
          "mode": "multi",
          "sort": "none"
        }
      },
      "pluginVersion": "9.4.7",
      "targets": [
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"osmosis-1\"}[$__rate_interval])",
          "format": "time_series",
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "A"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"axelar-dojo-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "B"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"celestia\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "C"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"cosmoshub-4\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "D"
        },
        {
          "datasource": {
            "type": "prometheus",
            "uid": "qUro79h4k"
          },
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"dydx-mainnet-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "E"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"gravity-bridge-3\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "F"
        },
        {
          "datasource": {
            "type": "prometheus",
            "uid": "qUro79h4k"
          },
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"juno-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "G"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"kaiyo-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "H"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"neutron-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "I"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"phoenix-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "J"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"secret-4\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "K"
        },
        {
          "datasource": "${DS_PROMETHEUS}",
          "editorMode": "code",
          "expr": "rate(chainpulse_txs{chain_id=\"stride-1\"}[$__rate_interval])",
          "format": "time_series",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{chain_id}}: {{src_channel}} -> {{dst_channel}}",
          "range": true,
          "refId": "L"
        }
      ],
      "title": "Effected IBC Packets",
      "type": "timeseries"
    },
    {
      "circleBackground": false,
      "colorBackground": false,
      "colorValue": false,
      "datasource": {
        "type": "prometheus",
        "uid": "qUro79h4k"
      },
      "defaultColor": "rgb(117, 117, 117)",
      "format": "none",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 6,
        "w": 10,
        "x": 0,
        "y": 11
      },
      "id": 2,
      "links": [],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "math": "",
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sortOrder": "asc",
      "sortOrderOptions": [
        {
          "text": "Ascending",
          "value": "asc"
        },
        {
          "text": "Descending",
          "value": "desc"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "datasource": {
            "type": "prometheus",
            "uid": "qUro79h4k"
          },
          "editorMode": "code",
          "expr": "chainpulse_chains{}",
          "range": true,
          "refId": "A"
        }
      ],
      "thresholds": [],
      "title": "Total Chains Monitored",
      "tooltip": {
        "show": true
      },
      "type": "blackmirror1-singlestat-math-panel",
      "valueFontSize": "80%",
      "valueMappingColorBackground": "#767171",
      "valueMaps": [
        {
          "op": "=",
          "text": "No data",
          "value": "null"
        }
      ],
      "valueName": "avg"
    }
  ],
  "refresh": "5s",
  "revision": 1,
  "schemaVersion": 38,
  "style": "dark",
  "tags": [
    "IBC"
  ],
  "templating": {
    "list": []
  },
  "time": {
    "from": "now-6h",
    "to": "now"
  },
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ],
    "time_options": [
      "5m",
      "15m",
      "1h",
      "6h",
      "12h",
      "24h",
      "2d",
      "7d",
      "30d"
    ]
  },
  "timezone": "",
  "title": "IBC Monitoring",
  "uid": "aF-Do8NIk",
  "version": 5,
  "weekStart": ""
}
```
