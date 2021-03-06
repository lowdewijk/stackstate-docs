---
title: STML Tags
kind: Documentation
---

# tags

## Tag: `auto-widget`

Data queried on the [analytics](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/use/topology_selection_advanced/README.md) page can often times show a preview. Data that is of some known format, like telemetry or topology, will therefore _automatically_ be shown in a chart of topology visualization. This tag renders data exactly the way the analytics preview of the analytics would render data.

It looks at the shape of the `data`, and if it is of some recognizable type \(determined by inspecting the `_type`\) it automatically renders the data in an appropriate format.

**Attributes:**

* `data` - any type of json data.

**Examples:**

This is an example of a script that uses the `auto-widget` to render a telemetry chart:

```text
Telemetry
  .query("StackState Metrics", "name='system.load.norm' and host='host1'")
  .metricField("value")
  .start("-2h")
  .aggregation("99th percentile", "5m")
  .then { host1Load ->
    UI.showReport(
        "My report",
        // STML starts below
        """
        |# Host 1 load
        |
        | The last two hours of load on host1, aggregated per 5 minutes and by 99th percentile looks like:
        |
        |<auto-widget data={metrics}></auto-widget>
        |
        | Thank you for watching!
        |""".stripMargin(),
        // end of STML
        [ metrics: host1Load ]
    )
  }
```

## Tag: `heatmap`

Shows a table of size `rows x columns` with color coded `CLEAR`, `DEVIATING`, and `CRITICAL` states. This is useful for showing multiple states over time or in combinations.

**Attributes:**

* `rows` - array of the labels placed on the rows. The number of rows is determined by the size of the array.
* `cols` - array of the labels placed on the columns. The number of cells is determined by the size of the array.
* `cells` - two-dimensional array of state elements. Each element in the two dimensional array can either be `CLEAR` \(green\), `DEVIATING` \(warning\) or `CRITICAL` \(red\).

**Examples:**

The following heatmap renders a table of 2x2 with all three colors.

```text
<heatmap cols='["col1", "col2"]' rows='["row1", "row2"]' cells='[["CLEAR", "DEVIATING"], ["DEVIATING", "CRITICAL"]]'></heatmap>
```

