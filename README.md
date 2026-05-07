# Apache Spark: Lazy Evaluation & Partitioning

Talk materials and live demo notebook for a 60-minute session on writing performant PySpark code.

📄 **[Slides (PDF)](./spark-presentation.pdf)**

---

## What's covered

| Demo | Concepts |
|------|----------|
| **Demo 1 — Lazy Evaluation & Catalyst** | Transformations vs actions, Catalyst optimizer, `explain()` as validation |
| **Demo 2 — Partitioning** | On-disk partitioning, partition pruning, `repartition` vs `coalesce`, shuffle tuning |
| **Demo 3 — Caching & UDFs** | Caching, `explain()` as diagnostic tool, UDFs vs built-in functions |

---

## Running the demo notebook

The only requirement is [Docker](https://www.docker.com/products/docker-desktop).

```bash
# 1. Start the environment
docker compose up

# 2. Open Jupyter in your browser
#    http://localhost:8888
```

Open `notebooks/nsch_sleep_demo.ipynb` and run cells from the top.

**First run:** cell 4 generates the synthetic dataset (~1 min). It is skipped automatically on reruns.

**Spark UI** is available at `http://localhost:4040` while a job is running.

---

## Memory

Default is 4 GB driver memory. Lower it in `docker-compose.yml` if needed:

```yaml
environment:
  - SPARK_DRIVER_MEMORY=2g
  - SPARK_EXECUTOR_MEMORY=2g
```

---

## Troubleshooting

**Port 8888 already in use** — change to `"8889:8888"` in `docker-compose.yml`, then open `http://localhost:8889`.

**Data not found** — run cell 4 first. The `data/` folder is gitignored and won't be present after a fresh clone.

**Spark UI not loading** — it only appears while a job is running. Trigger a cell with `.count()` or `.collect()` first.
