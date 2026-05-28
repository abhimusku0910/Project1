# Risk Assessment and Security Controls

## Risk Assessment

[View risk assessment spreadsheet](./risk-assessment.xlsx)

The risk assessment was carried out using the TVAMatrix template on the Brisbane accounting services network. It included the OpenWRT router/firewall, the staff workstations running Windows, hosted website, SSH management access and firewall rules as well as captured network traffic. Data, hardware, software, network, people and process assets were all assessed. The data assets comprised of customer contact information, staff credentials, website content, router configurations, and network traffic records. Vulnerabilities analyzed covered at least eight categories of information security threats, such as unauthorised access, weak authentication, insecure transmission, service exposure, malware, misconfiguration, data loss and insider misuse.

![Risk assessment screenshot 1](./images/risk-assessment-1.png)
*Figure 34: Main Risk Assessment*

![Risk assessment screenshot 2](./images/risk-assessment-2.png)
*Figure 35: TVAMatrix*

## Security Controls

Customer contact information was found to be the most vulnerable data asset, as it may be exposed via poor access controls, unsecured traffic, or a poorly configured management service.

| Control                                   | Implementation                                                                                                 | Benefit                                                                      | Disadvantage                                                           |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Access control and SSH key authentication | Use SSH key-based login for OpenWRT administration and restrict management access to authorised IT users only. | Reduces the risk of unauthorised administrator access and password guessing. | Requires secure private-key storage and user training.                 |
| Firewall restrictions                     | Allow only required services, such as the business website on port 80, and restrict management port 81.        | Reduces attack surface by limiting access to sensitive router services.      | Incorrect rules may block legitimate users or require troubleshooting. |
| Secure transmission and monitoring        | Replace HTTP with HTTPS in production and review packet captures/logs for suspicious traffic.                  | Protects customer and business data from being read in transit.              | Requires certificate management and additional configuration effort.   |

These controls are a direct extension of the hardening, firewall testing and traffic analysis that was done in the OpenWRT lab.
