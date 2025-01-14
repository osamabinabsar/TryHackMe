# Risk Management(Practical).md

## Assessing Risk

 **Portfolio Project: Quantitative Risk Analysis for IT Assets**

**Executive Summary:**

This project presents a comprehensive quantitative risk analysis for a range of IT assets within an organization. The analysis evaluates the potential risks, calculates the financial impact, and determines the effectiveness of proposed safeguards. The goal is to provide data-driven recommendations for risk mitigation, ensuring that the organization's resources are allocated efficiently.

**Methodology:**

The analysis employs key risk metrics:

- **Asset Value (AV):** Monetary value of the asset.
- **Exposure Factor (EF):** Percentage of asset value lost due to a risk event.
- **Annualized Rate of Occurrence (ARO):** Frequency of the risk event per year.
- **Single Loss Expectancy (SLE):** Loss from a single risk event (AV * EF).
- **Annualized Loss Expectancy (ALE):** Annual expected loss (SLE * ARO).
- **Safeguard Value:** Benefit of implementing a safeguard (ALE before - ALE after - Cost of Safeguard).

**Risk Assessment Table:**

| Asset             | Risk          | Asset Value | Exposure Factor | ARO    | SLE     | ALE     | Safeguard                  | Cost of Safeguard | EF after Safeguard | SLE after Safeguard | ARO after Safeguard | ALE after Safeguard | Annual Cost of Safeguard | Value of Safeguard | Safeguard Status |
|-------------------|---------------|-------------|-----------------|--------|---------|---------|----------------------------|-------------------|--------------------|---------------------|---------------------|---------------------|------------------------|--------------------|------------------|
| Laptop            | Theft         | $2000       | 100%            | 0.1    | $2000   | $200    | Laptop lock and security    | $50               | 0%                 | $0                  | 0.1                 | $0                  | $50                   | $150              | Implement       |
| Smart Phone       | Theft         | $1000       | 100%            | 0.5    | $1000   | $500    | Encryption                  | $20               | 1%                 | $10                 | 0.5                 | $5                  | $20                   | $475              | Implement       |
| Workstation       | Disk Failure  | $3000       | 100%            | 0.35   | $3000   | $1050   | Backup                      | $100              | 80%                | $2400               | 0.35                | $840                | $100                  | $110              | Implement       |
| Workstation       | Screen Failure| $1000       | 10%             | 0.1    | $100    | $10     | Replacement                 | -                 | 0%                 | $0                  | 0.1                 | $0                  | -                      | $10               | Implement       |
| Office            | Intrusion     | $20000      | 100%            | 0.7    | $20000  | $14000  | Preventive measures         | $3000             | 90%                | $18000              | 0.7                 | $12600              | $3000                 | -$1600            | Do not implement  |
| Server            | Cyberattack   | $50000      | 50%             | 0.05   | $25000  | $1250   | Advanced Firewall          | $2000             | 10%                | $5000               | 0.02                | $100                | $2000                 | -$850             | Do not implement  |
| Cloud Storage     | Data Breach   | $15000      | 70%             | 0.02   | $10500  | $210    | Multi-Factor Authentication  | $500              | 30%                | $4500               | 0.01                | $45                 | $500                  | -$335             | Do not implement  |
| Network Infrastructure | DDoS Attack | $40000      | 20%             | 0.1    | $8000   | $800    | DDoS Mitigation Service     | $1200             | 5%                 | $2000               | 0.05                | $100                | $1200                 | -$500             | Do not implement  |

**Safeguard Recommendations:**

- **Implement Laptop Locks and Security:** Provides a positive value of $150, reducing ALE from $200 to $0.
- **Implement Encryption for Smart Phones:** Offers a significant reduction in ALE from $500 to $5, with a value of $475.
- **Implement Backup for Workstations:** Reduces ALE from $1050 to $840, with a value of $110.

**Cost-Benefit Analysis:**

- Safeguards for laptops, smart phones, and workstations provide positive returns, justifying their implementation.
- Safeguards for servers, cloud storage, and network infrastructure do not provide sufficient benefits relative to their costs and should not be implemented.

**Conclusion:**

By implementing the recommended safeguards, the organization can reduce its annualized loss expectancy by over $735 ($150 + $475 + $110). This project demonstrates a structured approach to risk management, ensuring that resources are allocated to the most beneficial controls. The analysis provides a clear framework for decision-making, balancing cost and risk to enhance the organization's security posture.

**Visualizations:**

- **Bar Chart:** Comparing ALE before and after safeguards for each asset.
- **Pie Chart:** Distribution of total ALE across different assets.

**Report Organization:**

- **Introduction:** Purpose and scope of the risk assessment.
- **Methodology:** Definitions and calculations used.
- **Data Analysis:** Detailed table and analysis.
- **Recommendations:** Clear and actionable suggestions.
- **Conclusion:** Summary of benefits and overall risk posture.

This comprehensive project showcases the ability to conduct a quantitative risk analysis, make informed decisions, and communicate findings effectively to stakeholders.
