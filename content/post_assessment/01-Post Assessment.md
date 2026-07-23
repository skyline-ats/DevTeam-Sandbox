<AssessmentQG>

<QuestionMC>

::: Enabling Objective "Understand how ACPs function within the traffic flow and manage Layer 3-7 decisions."

Which Secure Firewall Threat Defense component performs the initial packet handling before traffic is inspected by the Access Control Policy?

::: Answers

- [ ] Intrusion Policy

- [x] LINA engine

- [ ] Security Intelligence

- [ ] Network Discovery

::: Feedback

The correct answer is: **LINA engine**. The LINA engine performs VPN processing, NAT, and Layer 3/Layer 4 inspection before forwarding permitted traffic to the Snort engine for Access Control Policy evaluation.

</QuestionMC>

<QuestionMC>

::: Enabling Objective "Examine how to create rules using various matching criteria."

Which two criteria can be combined within a single Access Control Policy rule to provide more granular traffic matching? (Choose two.)

::: Answers

- [x] Security Zones

- [ ] Device Serial Number

- [x] Network Objects

- [ ] Software Version

- [ ] Interface Speed

::: Feedback

The correct answer is: **Security Zones** and **Network Objects**. Access Control Policy rules commonly combine Security Zones with Network Objects and other Layer 3–Layer 7 criteria. Traffic must satisfy all configured conditions before the rule matches.

</QuestionMC>

<QuestionMC>

::: Enabling Objective "Configure actions and apply inspection policies."

Which Access Control Policy action allows traffic to bypass Snort inspection while still permitting the connection?

::: Answers

- [ ] Allow

- [ ] Monitor

- [x] Trust

- [ ] Block with Reset

::: Feedback

The correct answer is: **Trust**. The Trust action immediately returns the allowed decision to the LINA engine, bypassing Snort inspection and Network Discovery. It should only be used for traffic that does not require security inspection.

</QuestionMC>

<QuestionMC>

::: Enabling Objective "Demonstrate how to verify, save, and deploy configuration changes to managed devices."

What happens after changes are saved to an Access Control Policy in Secure Firewall Management Center?

::: Answers

- [ ] Managed devices begin enforcing the new policy.

- [x] The policy is stored in the management center database.

- [ ] Firewall services restart automatically.

- [ ] Existing connections are re-evaluated immediately.

::: Feedback

The correct answer is: **The policy is stored in the management center database**. Saving updates only the management center database. The changes are not applied to managed devices until the policy is deployed.

</QuestionMC>

<QuestionMC>

Which two practices help reduce risk when implementing significant Access Control Policy changes? (Choose two.)

::: Answers

- [x] Clone the current policy.

- [x] Review deployment status.

- [ ] Disable connection logging.

- [ ] Reorder every rule.

- [ ] Change the default action.

::: Feedback

The correct answer is: **Clone the current policy** and **Review deployment status**. Cloning provides a quick recovery option if changes cause issues, while verifying deployment confirms that managed devices successfully received and applied the intended configuration.

</QuestionMC>

<QuestionMC>

::: Enabling Objective "Introduce best practices for rule ordering, categories, and logging."

Why should specific Access Control Policy rules be placed above broader rules?

::: Answers

- [ ] To reduce deployment time.

- [ ] To simplify device assignments.

- [x] To ensure that the intended rule matches first.

- [ ] To improve SSL decryption performance.

::: Feedback

The correct answer is: **To ensure that the intended rule matches first**. Access Control Policy rules are evaluated from the top down. Once traffic matches an Allow or Block rule, no additional rules are evaluated.

</QuestionMC>

<QuestionMC>

Which practice best improves both the security and maintainability of an Access Control Policy?

::: Answers

- [x] Group related rules into categories.

- [ ] Configure every rule as Trust.

- [ ] Move application rules to the top.

- [ ] Disable logging for allowed traffic.

::: Feedback

The correct answer is: **Group related rules into categories**. Organizing rules into categories improves readability and administration, while placing specific rules before broader rules ensures that traffic matches the intended policy and prevents unintended rule matches.

</QuestionMC>

</AssessmentQG>