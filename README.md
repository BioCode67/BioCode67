# Juhyeong Kim (Curie)

Computer Engineering, Yeungnam University
AI/SW Team, Medical Device Development Center, **KMEDIhub**

Time-critical signals, and whether they reach the person who needs them in time.

---

## Research Interest

Two projects, one question asked in two domains: **a signal exists, a person needs it, and
its value collapses if it arrives late.** A disaster alert a Deaf viewer cannot parse is not
an alert. A deterioration trend that surfaces after the arrest is not a warning.

The work sits at the seam between the model and the person.

- Low-latency transport of structured signals — WebRTC, SFU topologies, research networks
- Client-side 3D reconstruction under bandwidth constraints
- Time-series modeling of physiological signals for early warning
- Operating-point design: precision, alarm fatigue, and what a false positive actually costs
- Network and system measurement as evaluation criteria, not footnotes

---

## Current Work

### SignBridge — real-time sign language interpretation for disaster broadcasts

> **들리지 않아도, 닿습니다.** — *Even if it cannot be heard, it reaches you.*

Built on **KOREN** (Korea Advanced Research Network) under NETCC Season 13, a national
KOREN-based R&D program. Team 닿다 (Danda).

Korean disaster alerts are text- and audio-first. For many Deaf users, written Korean is a
second language — sign language is the first. Human interpreters cannot be dispatched at
the speed and scale disaster broadcasting requires.

A four-agent pipeline converts alert text into a 3D signing avatar:

```
Disaster alert text
      ↓  [Agent 1] disaster judgment & triage
      ↓  [Agent 2] Korean → Gloss reordering → 3D joint generation
      ↓  KOREN low-latency transport  (67 joints · ~96 kbps per channel)
      ↓  Three.js client-side avatar reconstruction
   Signing avatar on the viewer's device
      ↕  [Agent 3] Q&A response   [Agent 4] broadcast control
```

**Keypoints, not video.** Transmitting 67 3D joint coordinates rather than an encoded video
stream cuts the per-channel payload by orders of magnitude, moves rendering cost to the
client, and makes multi-channel simultaneous broadcast tractable. The trade-off is
reconstruction fidelity — which is what the KOREN testbed exists to measure.

**Scope.** 3D rendering pipeline (Three.js), WebRTC transport and SFU deployment, network
performance measurement across KOREN PoPs.

**Infrastructure.** KOREN HPC (V100, Pangyo) for preprocessing and fine-tuning; KOREN VM
instances in Seoul and Daejeon for SFU serving and multi-region latency verification.

**Data.** AI Hub disaster sign language corpus (`dataSetSn=636`) — pre-extracted 2D/3D
keypoints with Gloss labels and non-manual markers, multi-camera quality controlled.
Fine-tuned from the released Transformer + Pointer + Prosody baseline.

🔗 [biocode67.github.io/signbridge](https://biocode67.github.io/signbridge)

> KOREN runs as a closed network, so the public demo is served via GitHub Pages while KOREN
> supplies the measured network performance data behind it.

---

### Vital-sign-based early warning for cardiac arrest

**AI/SW Team, Medical Device Development Center, KMEDIhub** — system design, ongoing.

In-hospital cardiac arrest is rarely instantaneous. It is usually preceded by hours of
subtle physiological deterioration that is recorded but not recognized. Conventional
track-and-trigger scores (MEWS, NEWS) are rule-based, coarsely thresholded, and generate
enough false alarms to induce alarm fatigue — at which point the warning stops functioning
as a warning regardless of its statistical performance.

The design question: can continuous vital-sign time series — heart rate, respiratory rate,
blood pressure, SpO₂, temperature — yield a calibrated risk score with clinically useful
lead time, at an operating point a ward will actually keep switched on?

The hard parts are as much deployment as modeling:

- **Severe class imbalance** — arrest events are rare, accuracy is meaningless, and
  threshold selection is the entire design
- **Irregular, missing, artifact-laden sampling** from bedside monitors
- **Precision at the operating point** — the false-positive budget is set by nursing
  workload, not by a ROC curve
- **Calibration and interpretability** as preconditions for clinical acceptance
- **SaMD constraints** — where inference runs, how it is versioned, how it is validated
  are regulatory questions before they are engineering ones

Both systems are alerting systems, and both live or die on the last hop: where inference
runs, what latency and reliability budget the monitoring path carries, and whether the
alert lands somewhere a human can act on it. Approaching clinical early warning from a
networked-systems background is an angle, not a detour.

---

## Technical Focus

| Area | Applied to |
|---|---|
| **Three.js / WebGL** | Skeletal avatar rigging, joint-driven animation, browser-side reconstruction from sparse keypoints |
| **WebRTC** | Data channel transport, SFU deployment, signaling, multi-region session setup |
| **Time-series / clinical ML** | Physiological signal preprocessing, imbalanced-event modeling, threshold and calibration analysis |
| **Network measurement** | RTT / jitter / packet loss instrumentation, research vs. commercial network benchmarking |
| **Python** | Dataset preprocessing, keypoint normalization, evaluation tooling |

---

## Elsewhere

Accessibility standards, Korean Sign Language linguistics — Gloss ordering and non-manual
markers are genuinely interesting grammar — and the unglamorous discipline of measuring
things properly before claiming them.

---

## Contact

- 📧 curie01@yu.ac.kr
- 🏛 Computer Engineering, Yeungnam University
- 🌏 Gyeongsan, Republic of Korea
