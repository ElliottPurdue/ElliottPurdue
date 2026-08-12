# Elliott Robert

**Electrical & Computer Engineering at Purdue** — concurrent BS/MS, concentrating in
Automatic Control and Machine Learning. I build systems where correctness is
measurable, and I try to prove my own results wrong before anyone else does.

---

### Currently: does financial news predict stock returns?

I built a research pipeline to find out, and the honest answer is mostly no.

```
251K headlines scored with FinBERT      2,510 out-of-sample sessions
5 pre-registered hypotheses, all reported     62 mutation-checked tests
```

**What it found.** No cross-sectional directional signal above IC 0.011 — the
sample's own detection floor. But news *coverage* predicts forward **volatility**
at t = +4.50 after within-stock controls, and sentiment correlates with the return
that has *already happened* (t = +5.47) far more than the one to come (t = +1.33).
The news says a lot about risk and almost nothing about direction.

**What it taught me.** A backtest reported a Sharpe of +0.50 and I didn't believe
it — the information coefficient disagreed, and one quarter turned out to account
for the entire return. Later a hypothesis cleared the significance threshold, so I
added 49% more data and watched it regress from t = 2.54 to 2.05. Twice a positive
result was available; twice the evidence said no.

→ **[nlp-alpha-engine](https://github.com/ElliottPurdue/nlp-alpha-engine)** — the
pipeline, the findings, and the controls that bound them.

---

### What I work on

**Quantitative research & data engineering** — walk-forward validation,
point-in-time correctness, statistical power analysis, idempotent ETL, schema
design with database-level integrity constraints.

**Low-latency backend systems** — Node.js services processing >1M events/day at
deterministic sub-50 ms latency, with distributed telemetry and fault-tolerant
WebSocket clients.

**Embedded & control systems** — bare-metal C and FreeRTOS on STM32 and ESP32,
custom peripheral drivers, PID attitude control, and TinyML at the edge.

---

### Tools

`Python` `C` `C++` `Node.js` `SQL` `MATLAB` `ARM Assembly`
`PyTorch` `HuggingFace Transformers` `XGBoost` `scikit-learn` `pandas`
`SQLite` `InfluxDB` `AWS` `Docker` `Grafana` `FreeRTOS` `Linux` `Git`

---

📍 West Lafayette, IN &nbsp;·&nbsp;
✉️ [erobert.ch@gmail.com](mailto:erobert.ch@gmail.com) &nbsp;·&nbsp;
💼 [LinkedIn](https://linkedin.com/in/elliott-robert)
