# grafana-zabbix-dashboards

Grafana dashboard collection for server infrastructure monitoring using the [Zabbix datasource plugin](https://grafana.com/grafana/plugins/alexanderzobnin-zabbix-datasource/). Includes a base server status dashboard and an extended variant with JVM monitoring.

Both dashboards are based on [Zabbix - Servers Status Table](https://grafana.com/grafana/dashboards/5456-zabbix-servers-status-table/) (Dashboard ID 5456) by the Grafana community, modified to suit a production home lab / sysadmin monitoring setup.

---

## Dashboards

### 1. Zabbix - Servers Status Table (`zabbix_servers_table.json`)

A clean tabular view of server performance across your Zabbix-monitored hosts. Each metric is displayed as a sortable table, ordered by worst performance so problem hosts surface immediately.

**Panels:**
- CPU Utilization %
- Memory Utilization %
- Filesystem Space Utilization %
- CPU I/O Wait Time
- Logged-in Users
- History (Zabbix trigger history)
- Problems (active Zabbix triggers)

**Best for:** General-purpose server fleet monitoring.

---

### 2. Zabbix - Servers Status + JVM Status (`zabbix_with_jvm_status.json`)

Extends the base dashboard with an additional panel to check whether Java is running on monitored hosts. Useful for environments where Java-based services (e.g., Tomcat, Elasticsearch, Jenkins) need to be tracked alongside system resources.

**Panels (all of the above, plus):**
- JVM Status (is Java running?)

**Best for:** Mixed environments with Java-based services.

---

## Prerequisites

| Requirement | Notes |
|---|---|
| Grafana | v7.x or later recommended |
| [Zabbix Plugin for Grafana](https://grafana.com/grafana/plugins/alexanderzobnin-zabbix-datasource/) | Install via `grafana-cli plugins install alexanderzobnin-zabbix-datasource` |
| Zabbix Server | v5.0 or later |
| Zabbix datasource configured in Grafana | Must be named `Zabbix` (or update the datasource name after import) |

---

## Installation

### Step 1 — Install the Zabbix plugin (if not already installed)

```bash
grafana-cli plugins install alexanderzobnin-zabbix-datasource
sudo systemctl restart grafana-server
```

### Step 2 — Configure the Zabbix datasource in Grafana

1. Go to **Configuration → Data Sources → Add data source**
2. Search for and select **Zabbix**
3. Enter your Zabbix server URL (e.g., `http://your-zabbix-server/zabbix/api_jsonrpc.php`)
4. Enter your Zabbix credentials
5. Click **Save & Test**

### Step 3 — Import a dashboard

1. Go to **Dashboards → Import**
2. Click **Upload JSON file**
3. Select the `.json` file from the `dashboards/` folder
4. Select your **Zabbix** datasource when prompted
5. Click **Import**

Repeat for any additional dashboards you want.

---

## Usage

Both dashboards include two template variables at the top:

- **Group** — Filter by Zabbix host group
- **Hosts** — Filter by specific hosts within the selected group

Dashboards auto-refresh every **1 minute** by default. This can be changed in the top-right corner of the Grafana UI.

---

## Repository Structure

```
grafana-zabbix-dashboards/
├── dashboards/
│   ├── zabbix_servers_table.json        # Base server status dashboard
│   └── zabbix_with_jvm_status.json      # Extended dashboard with JVM panel
└── README.md
```

---

## Credits

Based on [Zabbix - Servers Status Table](https://grafana.com/grafana/dashboards/5456-zabbix-servers-status-table/) (ID: 5456), originally published on Grafana Labs dashboards.

---

## License

MIT License — see [LICENSE](./LICENSE) for details.
