# Elliott Robert

Electrical and Computer Engineering at Purdue, on the concurrent BS/MS track,
concentrating in Automatic Control and Machine Learning. I build systems where
correctness is measurable, and I try to prove my own results wrong before anyone
else does.

---

### Does financial news predict stock returns?

I built a research pipeline to find out. The honest answer is mostly no.

```
251K headlines scored with FinBERT      2,510 out-of-sample sessions
5 pre-registered hypotheses, all reported     62 mutation-checked tests
```

**What it found.** No cross-sectional directional signal above IC 0.011, which is
the sample's own detection floor. News *coverage* does predict forward
**volatility** at t = +4.50 after within-stock controls, and sentiment tracks the
return that has *already happened* (t = +5.47) far more closely than the one still
to come (t = +1.33). The news says a lot about risk and almost nothing about
direction.

**The part I keep coming back to.** A backtest reported a Sharpe of +0.50 and I
didn't believe it. The information coefficient disagreed, and one quarter turned
out to account for the entire return. Later a hypothesis cleared the significance
threshold, so I added 49% more data and watched it regress from t = 2.54 to 2.05.
Twice a positive result was available. Twice the evidence said no.

→ **[nlp-alpha-engine](https://github.com/ElliottPurdue/nlp-alpha-engine)**, with
the full writeup and the controls that bound every claim.

---

### How accurate is an attitude estimate, really?

A quaternion EKF in dependency-free C99, validated against simulated trajectories
where ground truth actually exists. On hardware you can watch an estimate look
plausible; you cannot say it was accurate to 0.13°, because nothing tells you the
true attitude.

```
0.13° tilt RMS, 3x a tuned complementary filter    47 tests, no framework
4.0 us/update, 204 B state, 7.2 KB flash           runs on an ESP32-S3
```

**The interesting failure.** A covariance filter can become *confident about a
state it cannot observe.* A 6-DOF IMU carries no yaw information, and the EKF's
z-axis gyro bias estimate converged to 3.4x its true value while its stated
variance shrank. The complementary filter, having no covariance to be confident
with, simply left the state alone. That is the better failure mode. Adding a
magnetometer fixed it: same estimator, same tuning, bias recovered to within 1%.

**Where I went wrong.** My first magnetometer Jacobian was incorrect. Heading is a
rotation about the *world* vertical, but the error state lives in the *body*
frame. The two are identical while level, so nine unit tests passed against the
broken version. The simulator caught it in one run. The regression test has to
*move*, because at a fixed attitude even a wrong gain direction eventually
converges and reports success.

→ **[attitude-estimation](https://github.com/ElliottPurdue/attitude-estimation)**,
with the filters and the simulator that measured them.

---

### Can you write a transformer without autograd?

A GPT trained from scratch in dependency-free C99: forward pass *and* hand-derived
backward pass, with PyTorch used as a numerical oracle rather than as a framework.

```
30,144 gradients verified against autograd    38 mutations, 38 caught
loss 4.64 -> 2.00, starting at ln(vocab)      training bit-for-bit reproducible
```

**Why an oracle.** An incorrect gradient almost never announces itself. It usually
still decreases the loss, just more slowly, so "it trains" is the failure mode
rather than the evidence. Every operation is pinned against `torch.autograd`
before any of it is assembled, and separately against finite differences, which
know nothing about transformers and so cannot share a misreading of the
architecture.

**Two bugs the tests missed.** Both were buffers the forward pass must overwrite.
My tests handed them over freshly `calloc`'d: clean zeroed memory, which a
training loop never provides, since those buffers get reused every step. PyTorch
agreed with the broken code, because the oracle harness shared the same
assumption. Only breaking the code on purpose found them.

Then there was an assertion failure that looked trivial. `grads[0] == 0.3f` was
false while the bytes were provably unchanged, which turned out to be x87 excess
precision: the build was evaluating in 80 bits and calling itself float32, quietly
making the library more accurate than the embedded targets it is written for.
Pinned to real single-precision, every gradient still matches.

→ **[gpt-in-c](https://github.com/ElliottPurdue/gpt-in-c)**, where CI reruns the
whole mutation table on every push.

---

### What I work on

**Quantitative research and data engineering.** Walk-forward validation,
point-in-time correctness, statistical power analysis, idempotent ETL, and schema
design with database-level integrity constraints.

**Low-latency backend systems.** Node.js services processing >1M events/day at
deterministic sub-50 ms latency, with distributed telemetry and fault-tolerant
WebSocket clients.

**Embedded and control systems.** Bare-metal C and FreeRTOS on STM32 and ESP32,
custom peripheral drivers, sensor fusion, PID attitude control, and TinyML at the
edge.

---

### Tools

`Python` `C` `C++` `Node.js` `SQL` `MATLAB` `ARM Assembly`
`PyTorch` `HuggingFace Transformers` `XGBoost` `scikit-learn` `pandas`
`SQLite` `InfluxDB` `AWS` `Docker` `Grafana` `FreeRTOS` `Linux` `Git`

---

West Lafayette, IN &nbsp;·&nbsp;
[erobert.ch@gmail.com](mailto:erobert.ch@gmail.com) &nbsp;·&nbsp;
[LinkedIn](https://linkedin.com/in/elliott-robert)
