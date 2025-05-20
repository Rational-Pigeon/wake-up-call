# wake-up-call

# 🛏️ Problem & Opportunity

- **Snooze epidemic** – 1 in 3 adults hit snooze 2-plus times every morning  
- **Alarms get muted / ignored** → lateness, missed productivity  
- **Solution:**  
  1. Phone *calls* you at the exact alarm time  
  2. AI voice chats until you’re verbally awake  
  3. Keeps redialing if you don’t answer  
- **Why it’s exciting for us:** simple concept, real revenue, rich streaming data to engineer

---

# 📞 Solution in one diagram

flowchart TD
    A[User] -->|Outbound call| B[Twilio<br>/Calls API]
    B -- Media&nbsp;Stream --> C[Our WebSocket]

    C --> D[Whisper&nbsp;STT]
    D --> E[GPT-4o&nbsp;LLM]
    E --> F[Google&nbsp;TTS]
    
    F -- audio&nbsp;chunks --> B
    B -- RTP --> A



1. Scheduler triggers **Twilio /Calls** API  
2. TwiML `<Start><Stream>` pipes audio to us  
3. We stream STT ➜ LLM ➜ TTS (≤ 1 s)  
4. Twilio plays the reply; loop until done

---


# 💰 Economics at a glance

| Component | Cost / minute |
|-----------|---------------|
| Twilio voice | **$0.013** |
| Streaming STT | **$0.026** |
| Streaming TTS | **$0.002** |
| GPT-4o tokens | **$0.001** |
| **Total COGS** | **≈ $0.04** |

**Plan:** $12 / month → 60 min calls  
> Gross margin ≈ 76 %  
Break-even price per call ≈ $0.13 (at 70 % target margin)

---


# 🔧 Data-engineering playground

- **Real-time streaming** – WS framing, back-pressure, sub-second SLA  
- **Multi-modal pipeline** – audio → text → tokens → audio  
- **Event analytics** – Twilio webhooks → Kafka / warehouse → Grafana wake-rate & latency dashboards  
- **Cost telemetry** – per-utterance token + second metering  
- **Compliance logging** – consent, opt-outs, call recordings, retention policies

Perfect chance to flex everything we learned in boot-camp.

---


# 🚀 Execution & Ask

### 6-week weekend roadmap  
1. **W1:** hello-world call plays greeting  
2. **W2:** STT → GPT → TTS round-trip < 1 s  
3. **W3:** alarm scheduler + redial logic  
4. **W4:** Stripe metered billing & dashboard  
5. **W5:** Voice Insights + Grafana metrics  
6. **W6:** closed alpha with 10 real users

### Roles (rotating)
- Voice Ops · AI Pipeline · Data & Observability  
- Web/Billing · PM/Compliance  

**Commitment:** one sprint demo each Friday night.  
If we’re still pumped after 6 weeks → public launch!

*Who’s in?* ✋
