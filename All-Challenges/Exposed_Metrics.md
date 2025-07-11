# Exposed Metrics

**Category**: Sensitive Data Exposure  
**Difficulty**: 2  

---

### 🧠 Description

This challenge involved discovering a misconfigured endpoint that exposed internal application metrics — potentially leaking sensitive operational data.

---

### 🛠️ Solution

The challenge was solved by locating an unprotected `/metrics` endpoint, commonly used by tools like Prometheus.

---

### 🔍 Steps

1. While browsing the Juice Shop or running tools like Gobuster or manual fuzzing, I discovered an undocumented endpoint:
   
   ```
   GET /metrics
   ```

2. This endpoint was not listed in the UI and not protected by authentication or role checks.

3. When accessed, it returned plaintext Prometheus-format metrics, such as:
   
   ```
   juice_shop_orders_total{status="delivered"} 42
   juice_shop_users_total 1337
   process_cpu_seconds_total 105.6
   ```

4. These metrics revealed operational details about the app — e.g., number of users, orders, CPU usage — and confirmed that the application was exposing internal data publicly.

---

**Challenge completed** upon visiting `/metrics` and viewing the exposed data.
