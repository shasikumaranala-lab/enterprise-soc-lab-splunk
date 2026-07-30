# Dashboard Queries

These SPL queries are used to populate the Enterprise SOC Dashboard.

---

## Authentication Statistics

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count by EventCode
```

---

## Windows Event Distribution

```spl
index=main
| stats count by sourcetype
```

---

## Top Hosts

```spl
index=main
| stats count by host
| sort -count
```

---

## Investigation Timeline

```spl
index=main
| timechart span=1h count
```

---

## Recent Security Events

```spl
index=main
| table _time host sourcetype source
| sort -_time
```

---

## Event Type Summary

```spl
index=main
| stats count by EventCode
```