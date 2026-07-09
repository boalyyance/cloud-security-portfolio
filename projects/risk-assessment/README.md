# Risk Assessment & Security Audit – Botium Toys

## Scenario
Botium Toys is a small U.S. business that develops and sells toys, with a single physical location serving as office, storefront, and warehouse. Their online presence has grown internationally, putting pressure on the IT department to maintain secure operations.

The IT manager initiated an internal audit to better secure the company's infrastructure, identify potential risks, threats, and vulnerabilities, and ensure compliance with regulations for processing online payments and conducting business in the European Union (EU).

This project simulates that internal security audit, evaluating existing security controls, identifying risks and compliance gaps, and proposing recommendations based on the NIST Cybersecurity Framework (CSF). It demonstrates practical skills in risk analysis, security control evaluation, documentation, and compliance review.

## Objective
To evaluate existing IT controls, identify gaps and vulnerabilities, and provide actionable recommendations to improve Botium Toys' security posture while supporting compliance with NIST CSF and relevant regulations.

## Scope
The audit scope includes the entire security program at Botium Toys, covering IT assets (employee devices, office equipment), internal networks, and critical systems. All assets and existing controls will be reviewed for compliance and effectiveness.

### Goals
- Assess and classify existing IT assets based on their criticality.
- Complete the security controls and compliance checklist.
- Identify gaps in security controls and compliance.
- Provide actionable recommendations to improve overall security posture.

## Methodology

The assessment followed a structured five-step methodology based on the NIST Cybersecurity Framework (CSF):

1. **Review of IT Assets** – Inventory of all IT assets including devices, software, network, and physical assets.
2. **Risk Assessment** – Analyze gaps, identify vulnerabilities, assign risk scores.
3. **Control Evaluation** – Evaluate existing technical and administrative controls.
4. **Compliance Review** – Compare practices against NIST CSF and relevant regulations.
5. **Documentation** – Compile findings and recommendations.

## Risk Matrix

| Category                   | Finding                                                                                                                                                                   | Risk Level  |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| Asset Management            | Asset inventory is incomplete, and critical assets are not properly classified. All employees have access to sensitive information, including cardholder data and PII. | 🔴 High     |
| Data Protection              | Sensitive information is stored without encryption, and no Intrusion Detection System (IDS) is deployed to detect malicious activity.                                  | 🔴 High     |
| Access Control               | Least privilege and Separation of Duties (SoD) principles are not enforced. No Multi-Factor Authentication (MFA) is in place. Password management lacks centralized control. | 🔴 High     |
| Disaster Recovery            | No disaster recovery plan or backup strategy exists for critical business systems.                                                                                     | 🔴 High     |
| Compliance                   | Partial alignment with GDPR requirements. Several security controls do not meet recommended best practices.                                                            | 🟠 Medium   |
| Legacy Systems               | Legacy systems are monitored manually without documented procedures or maintenance schedules.                                                                          | 🟠 Medium   |
| Physical Security            | Physical controls including CCTV, door locks, and fire prevention systems are properly implemented.                                                                    | 🟢 Low      |
| Existing Security Controls   | Firewalls and antivirus solutions are deployed and monitored, contributing to system availability and integrity.                                                       | 🟢 Strength |

## Documentation

- 📄 [Scope, Goals & Risk Assessment Report](./Scope-goals-risk-assessment-report.pdf)
- 📋 [Controls and Compliance Checklist](./Controls-and-compliance-checklist.pdf)

## Recommendations and Expected Benefits

Based on the audit findings, the following recommendations are proposed to improve Botium Toys' security posture and compliance:

| Category                       | Recommendation                                                                                                                                                                                    | Expected Benefit                                                                                            |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Asset Management**           | Create and maintain a centralized inventory of all physical and digital assets. Classify assets based on their business value and criticality.                                                   | Improves asset visibility, supports risk management, and helps prioritize security efforts.                  |
| **Access Control**              | Implement the Principle of Least Privilege (PoLP), enforce role-based access control (RBAC), and apply Separation of Duties (SoD) for sensitive business processes.                              | Reduces the risk of unauthorized access, insider threats, and privilege abuse.                                |
| **Data Protection**             | Encrypt sensitive data at rest and in transit, implement Multi-Factor Authentication (MFA) for critical accounts, and deploy an Intrusion Detection System (IDS) to monitor malicious activity.  | Protects confidential information, strengthens authentication, and improves threat detection capabilities.   |
| **Disaster Recovery**          | Develop a formal Disaster Recovery Plan (DRP) and implement regular backups for critical systems. Test recovery procedures periodically.                                                         | Minimizes downtime and ensures business continuity following security incidents or system failures.          |
| **User & Password Management** | Establish strong password policies aligned with NIST recommendations, centralize identity management, and regularly review user permissions.                                                    | Improves authentication security and simplifies account management and auditing.                             |
| **Legacy Systems**              | Continuously monitor unsupported legacy systems and develop a phased migration plan to modern or cloud-based platforms.                                                                          | Reduces security risks associated with outdated technology and improves long-term maintainability.           |

## Lessons Learned

This project reinforced the importance of conducting structured risk assessments before implementing security controls.

It also demonstrated how frameworks such as the NIST CSF provide a practical approach to identifying risks, prioritizing remediation efforts, and improving an organization's overall security posture.

## Future Improvements

Future improvements could include:

- Mapping controls to MITRE ATT&CK
- Developing a complete Incident Response Plan
- Creating a Business Continuity Plan

## Skills Demonstrated

- **Risk Assessment & Analysis**: Conducted a detailed risk assessment of IT assets, identifying vulnerabilities, potential threats, and gaps in controls.
- **Security Control Evaluation**: Evaluated technical, administrative, and physical security controls, including firewalls, antivirus, access controls, and legacy system management.
- **Regulatory Compliance Awareness**: Assessed compliance with NIST CSF and relevant U.S. and E.U. regulations, including GDPR and data privacy requirements.
- **Access Management & Least Privilege**: Applied principles of least privilege, proper user access controls, and centralized account/password management policies.
- **Data Protection & Encryption**: Evaluated encryption needs and data protection mechanisms to safeguard sensitive information.
- **Disaster Recovery & Business Continuity Planning**: Designed recommendations for backup strategies and disaster recovery plans to maintain operational continuity.
- **Legacy System Management**: Assessed risks associated with legacy systems and proposed upgrades/migration strategies for cloud-based environments.
- **Documentation & Reporting**: Produced professional audit documentation, summarizing methodology, findings, and actionable recommendations.
- **Analytical & Problem-Solving Skills**: Applied structured thinking to identify risks, prioritize remediation, and propose practical solutions.

## Tools & Frameworks

- NIST Cybersecurity Framework (CSF)
- Risk Assessment Methodology
- Security Controls Assessment
- Compliance Review
- Markdown Documentation
- Git & GitHub
