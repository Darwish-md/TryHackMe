SPL stands for Search Processing Language. 

> Remember: KQL => Kusto Query Language used for Microsoft. & AQL => Advanced Query Language used for Qradar.

### Filtering results
- `fields` command is used to add or remove mentioned fields from the search results. To remove the field, minus sign ( - ) is used before the fieldname and plus ( + ) is used before the fields which we want to display: `index=windowslogs | fields + HostName - EventID`.
- `search` command is used to search for the raw text while using the chaining command |: `index=windowslogs | search Powershell`.
- `dedup` is the command used to remove duplicate fields from the search results to show the unique values: `index=windowslogs | dedup EventID`.
- `rename` allows us to change the name of the field in the search results: `| rename User as Employees`

### Structuring results
- `reverse` is used to reverse the order of the results.
- `table`
- `head` command returns the first 10 events if no number is specified: `| head 20`.
- `tail` command returns the last 10 events if no number is specified. `| tail 5`.
- `| sort Hostname` will sort the result in Ascending order.

### Transformational commands
- The highlight command shows the results in raw events mode with fields highlighted: `index=windowslogs | highlight User, host, EventID, Image`.
- `top` command returns frequent values for the top 10 events: `index=windowslogs | top limit=7 Image`, limit here shows only 7 instead of top 10, so it displays the top 7 Image (Processes) captured.
- `rare` does the opposite of top command: `index=windowslogs | top limit=7 Image`limit here shows only 7 instead of rare 10, so it displays the rare 7 Image (Processes) captured.
- `stats` and is used to calcualte different statistics like `max(field_name)`, `min(field_name)`, `avg(field_name)`, `sum(field_name)`, `count(field_name)`: `stats avg(x)`. It can be used as this as well where it will display each image and the corresponding count: `index=windowslogs | stats count by Image`.
- The chart command is used to transform the data into tables or visualizations: `index=windowslogs | chart count by User`
- The timechart command returns the time series chart covering the field following the function mentioned: `index=windowslogs | timechart count by Image`.
- 
