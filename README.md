# PingOne-Connectors-JMLAutomation

# PingOne Connectors – Hands‑On IAM Lab

## Lab Overview

This lab is designed to give hands‑on experience with **PingOne Connectors** in a real‑world IAM scenario. You’ll design, configure, and test identity lifecycle automation using PingOne + a target application.

**Audience:** IAM Engineers / PingOne learners
**Difficulty:** Intermediate
**Estimated Time:** 2–3 hours

---

## Learning Objectives

By the end of this lab, you will be able to:

* Explain what PingOne Connectors are and when to use them
* Configure a PingOne Connector (SCIM‑based)
* Automate Joiner–Mover–Leaver (JML) workflows
* Troubleshoot provisioning failures
* Validate identity lifecycle events end‑to‑end

---

## Architecture Diagram (Conceptual)

**PingOne**

* Directory (Users & Groups)
* Provisioning Engine
* Workflows / Rules

⬇

**PingOne Connector**

* SCIM 2.0 or REST
* Attribute mappings
* Event triggers

⬇

**Target Application**

* SaaS app (mock HR, CRM, or Ticketing system)
* Supports SCIM or REST API

---

## Lab Prerequisites

* PingOne tenant (trial or sandbox)
* Admin access to PingOne
* Sample target application (choose one):

  * SCIM test app (Postman Mock / SCIM playground)
  * Okta SCIM test app
  * Custom REST mock endpoint
* Basic knowledge of IAM concepts

---

## Lab 1: Explore PingOne Connectors

### Goal

Understand connector types and capabilities.

### Steps

1. Log in to **PingOne Admin Console**
2. Navigate to:
   **Connections → Provisioning → Connectors**
3. Review available connectors:

   * SCIM 2.0
   * REST‑based
   * App‑specific connectors
4. Identify:

   * Supported operations (Create, Update, Disable, Delete)
   * Authentication methods (OAuth, API Key, Basic Auth)

### Expected Outcome

You can explain when to use **SCIM vs REST connectors**.

---

## Lab 2: Create a SCIM Connector

### Goal

Provision users automatically to a target app.

### Steps

1. Go to **Connections → Provisioning → Connectors**
2. Click **Add Connector**
3. Select **SCIM 2.0**
4. Configure connection details:

   * Base URL
   * Authentication token
   * Test connection
5. Save the connector

### Validation

* Connection test passes
* Connector status shows **Active**

---

## Lab 3: Attribute Mapping

### Goal

Map PingOne attributes to the target system.

### Steps

1. Open the newly created connector
2. Navigate to **Mappings**
3. Map attributes:

   * `username → userName`
   * `email → emails[type=work].value`
   * `firstName → name.givenName`
   * `lastName → name.familyName`
4. Add a custom attribute (e.g., department)

### Expected Outcome

Attributes sync correctly during provisioning.

---

## Lab 4: Automated Joiner Flow

### Goal

Automatically provision new hires.

### Scenario

When a new employee is added to PingOne, their account is created in the target app.

### Steps

1. Create a **test user** in PingOne Directory
2. Assign the user to a **Provisioning Group**
3. Trigger provisioning
4. Monitor:

   * Provisioning logs
   * Connector activity

### Validation

* User appears in the target application
* Attributes match expected values

---

## Lab 5: Mover Scenario

### Goal

Update access when a user changes roles.

### Scenario

User moves from Engineering → IT.

### Steps

1. Update the user’s department attribute
2. Re‑provision the user
3. Verify updates in target app

### Expected Outcome

User attributes update without account recreation.

---

## Lab 6: Leaver (De‑Provisioning)

### Goal

Remove access automatically when a user leaves.

### Steps

1. Disable or delete the user in PingOne
2. Observe connector action:

   * Disable account
   * Or delete account
3. Confirm status in target app

### Validation

* User no longer has access
* Provisioning event logged

---

## Lab 7: Troubleshooting & Logs

### Goal

Diagnose provisioning issues.

### Common Issues

* Attribute mismatch
* Authentication failure
* SCIM schema errors

### Steps

1. Navigate to **Reports → Provisioning Logs**
2. Identify failed events
3. Fix mapping or connector config
4. Retry provisioning

---

## Lab 8: Bonus – CI/CD & Automation (Advanced)

### Goal

Automate connector deployment.

### Concepts

* PingOne APIs
* Terraform (if supported)
* GitHub Actions

### Example Use Cases

* Promote connectors from Dev → Prod
* Version control attribute mappings

---

## Lab Deliverables

* Working PingOne Connector
* Successful JML lifecycle demo
* Screenshots of logs & provisioning events

---

## Interview Tie‑In (Why This Lab Matters)

After completing this lab, you can confidently explain:

* How PingOne Connectors enable lifecycle automation
* How SCIM improves security & efficiency
* How IAM engineers reduce manual provisioning risks

---

## Optional Extensions

* Add group‑based access control
* Integrate Ping DaVinci workflow triggers
* Connect multiple target apps

---

**You now have a production‑style PingOne Connectors lab.**
