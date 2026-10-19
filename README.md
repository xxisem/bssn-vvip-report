# 🛡️ Responsible Disclosure: Mass WordPress Vulnerability on Indonesian Government & Education Domains

This repository contains the documentation of a mass vulnerability disclosure submitted to **BSSN (Badan Siber dan Sandi Negara)** via their VVIP-Program. The report identified multiple Indonesian government (`.go.id`) and education (`.ac.id`) domains vulnerable to **CVE-2026-64638** (WordPress Pre-Auth XSS).

## 📖 Case Summary
- **Target:** 23 Domains (Government & Education)
- **Vulnerability:** Reflected XSS / HTML Injection via WordPress `wp-login.php`
- **CVE ID:** CVE-2026-64638
- **Severity:** High
- **Status:** Reported to BSSN (Aug 8, 2026), successfully patched by domain owners.

## 🔍 Methodology
I performed manual testing on `wp-login.php` using the `redirect_to` parameter. The payload was designed to reflect HTML elements and execute JavaScript if the input was not sanitized. 
*Note: No RCE or sensitive data exfiltration was performed, strictly adhering to ethical research guidelines.*

## 🚨 Confirmed Findings
Out of 23 domains scanned, 11 domains reflected the payload. Below are the strongest pieces of evidence:

### 1. Confirmed XSS Execution (JavaScript Alert)
- **Domain:** `uns.ac.id`
- **Payload Effect:** Successfully executed a JavaScript popup (`[object Object]`), proving the payload is rendered and executed by the browser.
- **Evidence:** [View Screenshot](./assets/01_uns_ac_id_alert_xss.png)

### 2. HTML Injection / UI Manipulation
- **Domains:** `karanganyarkab.go.id`, `tanjungpura.ac.id`
- **Payload Effect:** The payload successfully injected a custom `<button>X</button>` element into the password field area. While the JavaScript didn't execute directly here due to browser protections, it proves the application fails to sanitize user input, allowing UI redressing.
- **Evidence:** 
  - [View Karanganyar Screenshot](./assets/02_karanganyarkab_html_injection.png)
  - [View Tanjungpura Screenshot](./assets/03_tanjungpura_html_injection.png)

## 🤝 Disclosure Timeline & BSSN Response
1. **Aug 8, 2026:** Initial report submitted to BSSN (`bantuan70@bssn.go.id` & `csirt@idsirtii.or.id`).
2. **Aug 9, 2026:** BSSN requested detailed PoCs and impact validation.
3. **Aug 9, 2026:** Submitted manual PoC, payloads, and screenshots proving XSS/HTML Injection.
4. **Aug 9, 2026:** BSSN verified the report and forwarded it to the respective system owners.
5. **Aug 15, 2026:** Follow-up confirmed that most affected domains had been patched.

## 📌 Key Takeaway
This case highlights the importance of manual validation over automated scanners. While a scanner can find the reflection, providing a manual PoC (like the JavaScript execution on `uns.ac.id`) is what validates the true impact of the vulnerability.
