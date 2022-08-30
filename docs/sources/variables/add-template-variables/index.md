---
aliases:
  - /docs/grafana/latest/variables/variable-types/
  - /docs/grafana/latest/variables/add-query-variable/
  - /docs/grafana/latest/variables/variable-types/add-query-variable/
  - /docs/grafana/latest/variables/add-custom-variable/
  - /docs/grafana/latest/variables/variable-types/add-custom-variable/
  - /docs/grafana/latest/variables/add-text-box-variable/
  - /docs/grafana/latest/variables/variable-types/add-text-box-variable/
  - /docs/grafana/latest/variables/add-constant-variable/
  - /docs/grafana/latest/variables/variable-types/add-constant-variable/
  - /docs/grafana/latest/variables/add-data-source-variable/
  - /docs/grafana/latest/variables/variable-types/add-data-source-variable/
  - /docs/grafana/latest/variables/add-interval-variable/
  - /docs/grafana/latest/variables/variable-types/add-interval-variable/
  - /docs/grafana/latest/variables/add-ad-hoc-filters/
  - /docs/grafana/latest/variables/variable-types/add-ad-hoc-filters/
  - /docs/grafana/latest/variables/global-variables/
  - /docs/grafana/latest/variables/variable-types/global-variables/
  - /docs/grafana/latest/variables/chained-variables/
  - /docs/grafana/latest/variables/variable-types/chained-variables/
  - /docs/grafana/latest/variables/add-template-variables/
title: Add template variables
menuTitle: Add template variables
weight: 140
keywords:
  - grafana
  - templating
  - documentation
  - guide
  - template
  - variable
  - global
  - standard
  - nested
  - chained
  - linked
---

# Add template variables

The following table lists the types of variables shipped with Grafana.

| Variable type     | Description                                                                                                                                                                                        |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query             | Query-generated list of values such as metric names, server names, sensor IDs, data centers, and so on. [Add a query variable]({{< relref "#add-a-query-variable" >}}).                            |
| Custom            | Define the variable options manually using a comma-separated list. [Add a custom variable]({{< relref "#add-a-custom-variable" >}}).                                                               |
| Text box          | Display a free text input field with an optional default value. [Add a text box variable]({{< relref "#add-a-text-box-variable" >}}).                                                              |
| Constant          | Define a hidden constant. [Add a constant variable]({{< relref "#add-a-constant-variable" >}}).                                                                                                    |
| Data source       | Quickly change the data source for an entire dashboard. [Add a data source variable]({{< relref "#add-a-data-source-variable" >}}).                                                                |
| Interval          | Interval variables represent time spans. [Add an interval variable]({{< relref "#add-an-interval-variable" >}}).                                                                                   |
| Ad hoc filters    | Key/value filters that are automatically added to all metric queries for a data source (InfluxDB, Prometheus, and Elasticsearch only). [Add ad hoc filters]({{< relref "#add-ad-hoc-filters" >}}). |
| Global variables  | Built-in variables that can be used in expressions in the query editor. Refer to [Global variables]({{< relref "#global-variables" >}}).                                                           |
| Chained variables | Variable queries can contain other variables. Refer to [Chained variables]({{< relref "#chained-variables" >}}).                                                                                   |

## Add a query variable

Query variables enable you to write a data source query that can return a list of metric names, tag values, or keys. For example, a query variable might return a list of server names, sensor IDs, or data centers. The variable values change as they dynamically fetch options with a data source query.

Query variables are generally only supported for strings. If your query returns numbers or any other data type, you might need to convert them to strings in order to use them as variables. For the Azure data source, for example, you can use the [tostring](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/tostringfunction) function for this purpose.

Query expressions can contain references to other variables and in effect create linked variables. Grafana detects this and automatically refreshes a variable when one of its linked variables change.

### Query expressions

Query expressions are different for each data source. For more information, refer to the documentation for your [data source]({{< relref "../../datasources/" >}}).

### Enter General options

1. Navigate to the dashboard you want to make a variable for and click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for the variable.
1. In the **Type** list, select **Query**.
1. (Optional) In **Label**, enter the display name of the variable dropdown.

   If you don't enter a display name, then the dropdown label is the variable name.

1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Query Options

1. In the **Data source** list, select the target data source for the query. For more information about data sources, refer to [Add a data source]({{< relref "../../datasources/add-a-data-source/" >}}).
1. In the **Refresh** list, select when the variable should update options.
   - **On Dashboard Load:** Queries the data source every time the dashboard loads. This slows down dashboard loading, because the variable query needs to be completed before dashboard can be initialized.
   - **On Time Range Change:** Queries the data source when the dashboard time range changes. Only use this option if your variable options query contains a time range filter or is dependent on the dashboard time range.
1. In the **Query** field, enter a query.
   - The query field varies according to your data source. Some data sources have custom query editors.
   - If you need more room in a single input field query editor, then hover your cursor over the lines in the lower right corner of the field and drag downward to expand.
1. (Optional) In the **Regex** field, type a regex expression to filter or capture specific parts of the names returned by your data source query. To see examples, refer to [Filter variables with regex]({{< relref "../filter-variables-with-regex/" >}}).
1. In the **Sort** list, select the sort order for values to be displayed in the dropdown list. The default option, **Disabled**, means that the order of options returned by your data source query will be used.
1. (Optional) Enter [Selection Options]({{< relref "../variable-selection-options/" >}}).
1. In **Preview of values**, Grafana displays a list of the current variable values. Review them to ensure they match what you expect.
1. Click **Add** to add the variable to the dashboard.

## Add a custom variable

Use a _custom_ variable for a value that does not change, such as a number or a string.

For example, if you have server names or region names that never change, then you might want to create them as custom variables rather than query variables. Because they do not change, you might use them in [chained variables]({{< relref "#chained-variables" >}}) rather than other query variables. That would reduce the number of queries Grafana must send when chained variables are updated.

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Custom**.
1. (Optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Custom Options

1. In the **Values separated by comma** list, enter the values for this variable in a comma-separated list. You can include numbers, strings, or key/value pairs separated by a space and a colon. For example, `key1 : value1,key2 : value2`.
1. (Optional) Enter [Selection Options]({{< relref "../variable-selection-options/" >}}).
1. In **Preview of values**, Grafana displays a list of the current variable values. Review them to ensure they match what you expect.
1. Click **Add** to add the variable to the dashboard.

## Add a text box variable

_Text box_ variables display a free text input field with an optional default value. This is the most flexible variable, because you can enter any value. Use this type of variable if you have metrics with high cardinality or if you want to update multiple panels in a dashboard at the same time.

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Text box**.
1. (optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Text options

1. (Optional) In the **Default value** field, select the default value for the variable. If you do not enter anything in this field, then Grafana displays an empty text box for users to type text into.
1. In **Preview of values**, Grafana displays a list of the current variable values. Review them to ensure they match what you expect.
1. Click **Add** to add the variable to the dashboard.

## Add a constant variable

_Constant_ variables enable you to define a hidden constant. This is useful for metric path prefixes for dashboards you want to share. When you export a dashboard, constant variables are converted to import options.

Constant variables are _not_ flexible. Each constant variable only holds one value, and it cannot be updated unless you update the variable settings.

Constant variables are useful when you have complex values that you need to include in queries but don't want to retype in every query. For example, if you had a server path called `i-0b6a61efe2ab843gg`, then you could replace it with a variable called `$path_gg`.

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Constant**.
1. (optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **Variable:** No variable dropdown is displayed on the dashboard. This is the default.
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.

### Enter Constant options

1. In the **Value** field, enter the variable value. You can enter letters, numbers, and symbols. You can even use wildcards if you use [raw format]({{< relref "../advanced-variable-format-options/#raw" >}}).
1. In **Preview of values**, Grafana displays the current variable value. Review it to ensure it matches what you expect.
1. Click **Add** to add the variable to the dashboard.

## Add a data source variable

_Data source_ variables enable you to quickly change the data source for an entire dashboard. They are useful if you have multiple instances of a data source, perhaps in different environments.

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Datasource**.
1. (Optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Data source options

1. In the **Type** list, select the target data source for the variable. For more information about data sources, refer to [Add a data source]({{< relref "../../datasources/add-a-data-source/" >}}).
1. (Optional) In **Instance name filter**, enter a regex filter for which data source instances to choose from in the variable value drop-down list. Leave this field empty to display all instances.
1. (Optional) Enter [Selection Options]({{< relref "../variable-selection-options/" >}}).
1. In **Preview of values**, Grafana displays a list of the current variable values. Review them to ensure they match what you expect.
1. Click **Add** to add the variable to the dashboard.

## Add an interval variable

Use an _interval_ variable to represents time spans such as `1m`,`1h`, `1d`. You can think of them as a dashboard-wide "group by time" command. Interval variables change how the data is grouped in the visualization. You can also use the Auto Option to return a set number of data points per time span.

You can use an interval variable as a parameter to group by time (for InfluxDB), date histogram interval (for Elasticsearch), or as a summarize function parameter (for Graphite).

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Interval**.
1. (Optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Interval Options

1. In the **Values** field, enter the time range intervals that you want to appear in the variable drop-down list. The following time units are supported: `s (seconds)`, `m (minutes)`, `h (hours)`, `d (days)`, `w (weeks)`, `M (months)`, and `y (years)`. You can also accept or edit the default values: `1m,10m,30m,1h,6h,12h,1d,7d,14d,30d`.
1. (Optional) Turn on the **Auto Option** if you want to add the `auto` option to the list. This option allows you to specify how many times the current time range should be divided to calculate the current `auto` time span. If you turn it on, then two more options appear:
   - **Step count -** Select the number of times the current time range will be divided to calculate the value, similar to the **Max data points** query option. For example, if the current visible time range is 30 minutes, then the `auto` interval groups the data into 30 one-minute increments. The default value is 30 steps.
   - **Min Interval -** The minimum threshold below which the step count intervals will not divide the time. To continue the 30 minute example, if the minimum interval is set to 2m, then Grafana would group the data into 15 two-minute increments.
1. In **Preview of values**, Grafana displays a list of the current variable values. Review them to ensure they match what you expect.
1. Click **Add** to add the variable to the dashboard.

### Interval variable examples

The following example shows a template variable `myinterval` in a Graphite function:

```
summarize($myinterval, sum, false)
```

The following example shows a more complex Graphite example, from the [Graphite Template Nested Requests panel](https://play.grafana.org/d/000000056/graphite-templated-nested?editPanel=2&orgId=1):

```
groupByNode(summarize(movingAverage(apps.$app.$server.counters.requests.count, 5), '$interval', 'sum', false), 2, 'sum')
```

## Add ad hoc filters

_Ad hoc filters_ enable you to add key/value filters that are automatically added to all metric queries that use the specified data source. Unlike other variables, you do not use ad hoc filters in queries. Instead, you use ad hoc filters to write filters for existing queries.

> **Note:** Ad hoc filter variables only work with Prometheus, Loki, InfluxDB, and Elasticsearch data sources.

### Enter General options

1. Navigate to the dashboard you want to make a variable for and then click the **Dashboard settings** (gear) icon at the top of the page.
1. On the **Variables** tab, click **New**.
1. Enter a **Name** for your variable.
1. In the **Type** list, select **Ad hoc filters**.
1. (Optional) In **Label**, enter the display name of the variable dropdown. If you don't enter a display name, then the dropdown label will be the variable name.
1. Choose a **Hide** option:
   - **No selection (blank):** The variable dropdown displays the variable **Name** or **Label** value. This is the default.
   - **Label:** The variable dropdown only displays the selected variable value and a down arrow.
   - **Variable:** No variable dropdown is displayed on the dashboard.

### Enter Options

1. In the **Data source** list, select the target data source. For more information about data sources, refer to [Add a data source]({{< relref "../../datasources/add-a-data-source/" >}}).
1. Click **Add** to add the variable to the dashboard.

### Create ad hoc filters

Ad hoc filters are one of the most complex and flexible variable options available. Instead of a regular list of variable options, this variable allows you to build a dashboard-wide ad hoc query. Filters you apply in this manner are applied to all panels on the dashboard.

## Global variables

Grafana has global built-in variables that can be used in expressions in the query editor. This topic lists them in alphabetical order and defines them. These variables are useful in queries, dashboard links, panel links, and data links.

### $\_\_dashboard

> Only available in Grafana v6.7+. In Grafana 7.1, the variable changed from showing the UID of the current dashboard to the name of the current dashboard.

This variable is the name of the current dashboard.

### $\_\_from and $\_\_to

Grafana has two built-in time range variables: `$__from` and `$__to`. They are currently always interpolated as epoch milliseconds by default, but you can control date formatting.

> **Note:** This special formatting syntax is only available in Grafana 7.1.2+

| Syntax                   | Example result           | Description                                                                                               |
| ------------------------ | ------------------------ | --------------------------------------------------------------------------------------------------------- |
| `${__from}`              | 1594671549254            | Unix millisecond epoch                                                                                    |
| `${__from:date}`         | 2020-07-13T20:19:09.254Z | No args, defaults to ISO 8601/RFC 3339                                                                    |
| `${__from:date:iso}`     | 2020-07-13T20:19:09.254Z | ISO 8601/RFC 3339                                                                                         |
| `${__from:date:seconds}` | 1594671549               | Unix seconds epoch                                                                                        |
| `${__from:date:YYYY-MM}` | 2020-07                  | Any custom [date format](https://momentjs.com/docs/#/displaying/) that does not include the `:` character |

The syntax above also works with `${__to}`.

You can use this variable in URLs, as well. For example, you can send a user to a dashboard that shows a time range from six hours ago until now: https://play.grafana.org/d/000000012/grafana-play-home?viewPanel=2&orgId=1?from=now-6h&to=now

### $\_\_interval

You can use the `$__interval` variable as a parameter to group by time (for InfluxDB, MySQL, Postgres, MSSQL), Date histogram interval (for Elasticsearch), or as a _summarize_ function parameter (for Graphite).

Grafana automatically calculates an interval that can be used to group by time in queries. When there are more data points than can be shown on a graph, then queries can be made more efficient by grouping by a larger interval. It is more efficient to group by 1 day than by 10s when looking at 3 months of data and the graph will look the same and the query will be faster. The `$__interval` is calculated using the time range and the width of the graph (the number of pixels).

Approximate Calculation: `(to - from) / resolution`

For example, when the time range is 1 hour and the graph is full screen, then the interval might be calculated to `2m` - points are grouped in 2 minute intervals. If the time range is 6 months and the graph is full screen, then the interval might be `1d` (1 day) - points are grouped by day.

In the InfluxDB data source, the legacy variable `$interval` is the same variable. `$__interval` should be used instead.

The InfluxDB and Elasticsearch data sources have `Group by time interval` fields that are used to hard code the interval or to set the minimum limit for the `$__interval` variable (by using the `>` syntax -> `>10m`).

### $\_\_interval_ms

This variable is the `$__interval` variable in milliseconds, not a time interval formatted string. For example, if the `$__interval` is `20m` then the `$__interval_ms` is `1200000`.

### $\_\_name

This variable is only available in the Singlestat panel and can be used in the prefix or suffix fields on the Options tab. The variable will be replaced with the series name or alias.

### $\_\_org

This variable is the ID of the current organization.
`${__org.name}` is the name of the current organization.

### $\_\_user

> Only available in Grafana v7.1+

`${__user.id}` is the ID of the current user.
`${__user.login}` is the login handle of the current user.
`${__user.email}` is the email for the current user.

### $\_\_range

Currently only supported for Prometheus and Loki data sources. This variable represents the range for the current dashboard. It is calculated by `to - from`. It has a millisecond and a second representation called `$__range_ms` and `$__range_s`.

### $\_\_rate_interval

Currently only supported for Prometheus data sources. The `$__rate_interval` variable is meant to be used in the rate function. Refer to [Prometheus query variables]({{< relref "../../datasources/prometheus.md#using-__rate_interval">}}) for details.

### $timeFilter or $\_\_timeFilter

The `$timeFilter` variable returns the currently selected time range as an expression. For example, the time range interval `Last 7 days` expression is `time > now() - 7d`.

This is used in several places, including:

- The WHERE clause for the InfluxDB data source. Grafana adds it automatically to InfluxDB queries when in Query Editor mode. You can add it manually in Text Editor mode: `WHERE $timeFilter`.
- Log Analytics queries in the Azure Monitor data source.
- SQL queries in MySQL, Postgres, and MSSQL.
- The `$__timeFilter` variable is used in the MySQL data source.

## Chained variables

_Chained variables_, also called _linked variables_ or _nested variables_, are query variables with one or more other variables in their variable query. This section explains how chained variables work and provides links to example dashboards that use chained variables.

Chained variable queries are different for every data source, but the premise is the same for all. You can use chained variable queries in any data source that allows them.

Extremely complex linked templated dashboards are possible, 5 or 10 levels deep. Technically, there is no limit to how deep or complex you can go, but the more links you have, the greater the query load.

### Grafana Play dashboard examples

The following Grafana Play dashboards contain fairly simple chained variables, only two layers deep. To view the variables and their settings, click **Dashboard settings** (gear icon) and then click **Variables**. Both examples are expanded in the following section.

- [Graphite Templated Nested](https://play.grafana.org/d/000000056/graphite-templated-nested?orgId=1&var-app=country&var-server=All&var-interval=1h)
- [InfluxDB Templated](https://play.grafana.org/d/000000002/influxdb-templated?orgId=1)

### Examples explained

Variables are useful to reuse dashboards and dynamically change what is shown in dashboards. Chained variables are especially useful to filter what you see.

Create parent/child relationship in a variable, sort of a tree structure where you can select different levels of filters.

The following sections explain the linked examples in the dashboards above in depth and builds on them. While the examples are data source-specific, the concepts can be applied broadly.

#### Graphite example

In this example, there are several applications. Each application has a different subset of servers. It is based on the [Graphite Templated Nested](https://play.grafana.org/d/000000056/graphite-templated-nested?orgId=1&var-app=country&var-server=All&var-interval=1h).

Now, you could make separate variables for each metric source, but then you have to know which server goes with which app. A better solution is to use one variable to filter another. In this example, when the user changes the value of the `app` variable, it changes the dropdown options returned by the `server` variable. Both variables use the **Multi-value** option and **Include all option**, enabling users to select some or all options presented at any time.

##### app variable

The query for this variable basically says, "Give me all the applications that exist."

```
apps.*
```

The values returned are `backend`, `country`, `fakesite`, and `All`.

##### server variable

The query for this variable basically says, "Give me all servers for the currently chosen application."

```
apps.$app.*
```

If the user selects `backend`, then the query changes to:

```
apps.backend.*
```

The query returns all servers associated with `backend`, including `backend_01`, `backend_02`, and so on.

If the user selects `fakesite`, then the query changes to:

```
apps.fakesite.*
```

The query returns all servers associated with `fakesite`, including `web_server_01`, `web_server_02`, and so on.

##### More variables

> **Note:** This example is theoretical. The Graphite server used in the example does not contain CPU metrics.

The dashboard stops at two levels, but you could keep going. For example, if you wanted to get CPU metrics for selected servers, you could copy the `server` variable and extend the query so that it reads:

```
apps.$app.$server.cpu.*
```

This query basically says, "Show me the CPU metrics for the selected server."

Depending on what variable options the user selects, you could get queries like:

```
apps.backend.backend_01.cpu.*
apps.{backend.backend_02,backend_03}.cpu.*
apps.fakesite.web_server_01.cpu.*
```

#### InfluxDB example

In this example, you have several data centers. Each data center has a different subset of hosts. It is based on the [InfluxDB Templated](https://play.grafana.org/d/000000002/influxdb-templated?orgId=1).

In this example, when the user changes the value of the `datacenter` variable, it changes the dropdown options returned by the `host` variable. The `host` variable uses the **Multi-value** option and **Include all option**, allowing users to select some or all options presented at any time. The `datacenter` does not use either option, so you can only select one data center at a time.

##### datacenter variable

The query for this variable basically says, "Give me all the data centers that exist."

```
SHOW TAG VALUES  WITH KEY = "datacenter"
```

The values returned are `America`, `Africa`, `Asia`, and `Europe`.

##### host variable

The query for this variable basically says, "Give me all hosts for the currently chosen data center."

```
SHOW TAG VALUES WITH KEY = "hostname" WHERE "datacenter" =~ /^$datacenter$/
```

If the user selects `America`, then the query changes to:

```
SHOW TAG VALUES WITH KEY = "hostname" WHERE "datacenter" =~ /^America/
```

The query returns all servers associated with `America`, including `server1`, `server2`, and so on.

If the user selects `Europe`, then the query changes to:

```
SHOW TAG VALUES WITH KEY = "hostname" WHERE "datacenter" =~ /^Europe/
```

The query returns all servers associated with `Europe`, including `server3`, `server4`, and so on.

##### More variables

> **Note:** This example is theoretical. The InfluxDB server used in the example does not contain CPU metrics.

The dashboard stops at two levels, but you could keep going. For example, if you wanted to get CPU metrics for selected hosts, you could copy the `host` variable and extend the query so that it reads:

```
SHOW TAG VALUES WITH KEY = "cpu" WHERE "datacenter" =~ /^$datacenter$/ AND "host" =~ /^$host$/
```

This query basically says, "Show me the CPU metrics for the selected host."

Depending on what variable options the user selects, you could get queries like:

```bash
SHOW TAG VALUES WITH KEY = "cpu" WHERE "datacenter" =~ /^America/ AND "host" =~ /^server2/
SHOW TAG VALUES WITH KEY = "cpu" WHERE "datacenter" =~ /^Africa/ AND "host" =~ /^server/7/
SHOW TAG VALUES WITH KEY = "cpu" WHERE "datacenter" =~ /^Europe/ AND "host" =~ /^server3+server4/
```

### Best practices and tips

The following practices will make your dashboards and variables easier to use.

#### Creating new linked variables

- Chaining variables create parent/child dependencies. You can envision them as a ladder or a tree.
- The easiest way to create a new chained variable is to copy the variable that you want to base the new one on. In the variable list, click the **Duplicate variable** icon to the right of the variable entry to create a copy. You can then add on to the query for the parent variable.
- New variables created this way appear at the bottom of the list. You might need to drag it to a different position in the list to get it into a logical order.

#### Variable order

You can change the orders of variables in the dashboard variable list by clicking the up and down arrows on the right side of each entry. Grafana lists variable dropdowns left to right according to this list, with the variable at the top on the far left.

- List variables that do not have dependencies at the top, before their child variables.
- Each variable should follow the one it is dependent on.
- Remember there is no indication in the UI of which variables have dependency relationships. List the variables in a logical order to make it easy on other users (and yourself).

#### Complexity consideration

The more layers of dependency you have in variables, the longer it will take to update dashboards after you change variables.

For example, if you have a series of four linked variables (country, region, server, metric) and you change a root variable value (country), then Grafana must run queries for all the dependent variables before it updates the visualizations in the dashboard.