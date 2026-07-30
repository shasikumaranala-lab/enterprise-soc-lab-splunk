# Dashboard Panels

## Authentication Statistics

### Purpose

Displays authentication-related events.

### SPL

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count by EventCode
```

---

## Windows Event Distribution

### Purpose

Displays the distribution of collected Windows event logs.

```spl
index=main
| stats count by sourcetype
```

---

## Investigation Timeline

### Purpose

Visualizes events over time.

```spl
index=main
| timechart span=1h count
```

---

## Top Hosts

### Purpose

Shows hosts generating the highest number of events.

```spl
index=main
| stats count by host
| sort -count
```

---

## Event Types

### Purpose

Displays event frequency by Event ID.

```spl
index=main
| stats count by EventCode
```

---

## Recent Security Events

### Purpose

Displays the latest collected events.

```spl
index=main
| table _time host source sourcetype
| sort -_time
```