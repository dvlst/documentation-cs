# CVSS 3.1 Base Score Metrics
![[Pasted image 20220910141055.png]]
*All base metrics are required to generate a base score.

**URL**: [NVD - CVSS v3 Calculator (nist.gov)](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)

## Exploitability Metrics
### Attack Vector (AV) Values
This metric reflects the context by which vulnerability exploitation is possible. This metric value (and consequently the Base score) will be larger the more remote (logically, and physically) an attacker can be in order to exploit the vulnerable component.

#### Network (AV:N)
A vulnerability exploitable with Network access means the vulnerable component is bound to the network stack and the attacker's path is through OSI layer 3 (the network layer). Such a vulnerability is often termed ‘remotely exploitable’ and can be thought of as an attack being exploitable one or more network hops away (e.g. across layer 3 boundaries from routers).

#### Adjacent Network (AV:A)
A vulnerability exploitable with Adjacent Network access means the vulnerable component is bound to the network stack, however the attack is limited to the same shared physical (e.g. Bluetooth, IEEE 802.11), or logical (e.g. local IP subnet) network, and cannot be performed across an OSI layer 3 boundary (e.g. a router).

#### Local (AV:L)
A vulnerability exploitable with Local access ‘means that the vulnerable component is not bound to the network stack, and the attacker's, path is via read/write/execute capabilities. In some cases, the attacker may be logged in locally in order to exploit the vulnerability, o ‘may rely on User Interaction to execute a malicious file.

#### Physical (AV:P)
A vulnerability exploitable with Physical access requires the attacker to physically touch or manipulate the vulnerable component, such as attaching an peripheral device to a system.

### Attack Complexity (AC) Values
The Attack Complexity metric describes the conditions beyond the attacker's control that must exist in order to exploit the vulnerability. As described below, such conditions may require the collection of more information about the target, the presence of certain system configuration settings, or computational, exceptions.

#### Low (AC:L)
Specialized access conditions or extenuating circumstances do not exist. An attacker can expect repeatable success against the vulnerable component.

#### High (AC:H)
A successful attack depends on conditions beyond the attacker's control. That is, a successful attack cannot be accomplished at will, but requires the attacker to invest in some ‘measurable amount of effort in preparation or execution against the vulnerable component before a successful attack can be expected.

### Privileges Required (PR) Values
This metric describes the level of privileges an attacker must possess before successfully exploiting the vulnerability.

#### None (PR:N)
The attacker is unauthorized prior to attack, and therefore does not require any access to settings or files to carry out an attack.

#### Low (PR:L)
The attacker is authorized with (i.e. requires) privileges that provide basic user capabilities that could normally affect only settings and files owned by a user. Alternatively, an attacker with Low privileges may have the ability to cause an impact only to non-sensitive resources.

#### High (PR:N)
The attacker is authorized with (i.e. requires) privileges that provide significant (e.g administrative) control over the vulnerable component that could affect component-wide settings and files.

### User Interaction (UI) Values
This metric captures the requirement for a user, other than the attacker, to participate in the successful compromise of the vulnerable component. This metric determines whether the vulnerability can be exploited solely at the will ofthe attacker, or whether a separate user (or user-initiated process) must participate in some manner.

#### None (UI:N)
The vulnerable system can be exploited without interaction from any user.

#### Required (UI:R)
Successful exploitation of this vulnerability requires a user to take some action before the vulnerability can be exploited, such as convincing a user to click a link in an email.

### Scope (S) Values
An important property captured by CVSS v3.0 is the ability for a vulnerability in one software component to impact resources beyond its, ‘means, or privileges. This consequence is represented by the metric Authorization Scope, or simply Scope. For more information see the Cvssv3 Specification  (http://www.first.org/cvss/specification-document#2.2).

#### Unchanged (S:U)
An exploited vulnerability can only affect, resources managed by the same authority. In this case the vulnerable component and the impacted component are the same.

#### Changed (S:C)
An exploited vulnerability can affect resources beyond the authorization privileges intended by the vulnerable component. In this case the vulnerable component and the impacted component are different.

## Impact Metrics
### Confidentiality Impact (C) Values
This metric measures the impact to the confidentiality of the information resources managed by a software component due to a successfully exploited vulnerability. Confidentiality refers to limiting information access and disclosure to only authorized users, as well as preventing access by, or disclosure to, unauthorized ones.

#### None (C:N)
There is no loss of confidentiality within the impacted component.

#### Low (C:L)
There is some loss of confidentiality. Access to some restricted information is obtained, but the attacker does not have control over what information is obtained, or the amount or kind of loss is constrained. The information disclosure does not cause a direct, serious loss to the impacted component.

#### High (C:H)
There is total loss of confidentiality, resulting in ll resources within the impacted component being divulged to the attacker. Alternatively, access to only some restricted information is obtained, but the disclosed information presents a direct, serious impact.

### Integrity Impact (I) Values
This metric measures the impact to integrity of a successfully exploited vulnerability. Integrity refers to the trustworthiness and veracity of information.

#### None (I:N)
There is no loss of integrity within the impacted component.

#### Low (I:L)
Modification of data is possible, but the attacker does not have control over the consequence of a modification, or the amount of modification is constrained. The data ‘modification does not have a direct, serious impact on the impacted component.

#### High (I:H)
There is a total loss of integrity, or a complete loss of protection. For example, the attacker is able to modify any/all files protected by the impacted component. Alternatively, only some files can be modified, but malicious ‘modification would present a direct, serious consequence to the impacted component.

### Availability Impact (A) Values
This metric measures the impact to the availability of the impacted component resulting from a successfully exploited vulnerability. While the Confidentiality and Integrity impact metrics apply to the loss of confidentiality or integrity of data (e.g. information, files) used by the impacted component, this metric refers to the loss of availability of the impacted component itself, such as a networked service (e.g., web, database, email). Since availability refers to the accessibility of information resources, attacks that consume network bandwidth, processor cycles, or disk space all impact the availability of an impacted component.

#### None (A:N)
There is no impact to availability within the impacted component.

#### Low (A:L)
There is reduced performance or interruptions in resource availability. Even ifrepeated exploitation of the vulnerability is possible,  the attacker does not have the ability to completely deny service to legitimate users. The resources in the impacted component are either partially available all ofthe time, or fully available only some of the time, but overall there isno direct, serious consequence to the impacted component.

#### High (A:H)
There is total loss of availability, resulting in the attacker being able to fully deny access to resources in the impacted component; this loss is either sustained (while the attacker continues to deliver the attack) or persistent (the condition persists even after the attack has completed). Alternatively, the attacker has the ability to deny some availability, but the loss of availability presents a direct, serious consequence to the impacted component (eg. the attacker cannot disrupt existing connections, but can prevent new connections; the attacker can repeatedly exploit a vulnerability that, in each instance of a successful attack, leaks a only small amount of memory, but after repeated exploitation causes a service to become completely unavailable).


# CVSS 3.1 Temporal Score Metrics
![[Pasted image 20220910144634.png]]

### Exploit Code Maturity (E)
#### Not Defined (E:X)
Assigning this value to the metric will not influence the score. it is a signal to a scoring equation to skip this metric.

#### Unproven that exploit exists (E:U)
No exploit code is available, or an exploit is entirely theoretical.

#### Proof of concept code (E:P)
Proof-of-concept exploit code is available, or an attack demonstration is not practical for most systems. The code or technique is not functional in all situations and may require substantial modification by a skilled attacker.

#### Functional exploit exists (E:F)
Functional exploit code is available. The code ‘works in most situations where the vulnerability exists.

#### High (E:H)
Functional autonomous code exists, or no. exploits required (manual trigger) and details are widely available. Exploit code works in every situation, or is actively being delivered via an autonomous agent (such as a worm or virus). Network-connected systems are likely to encounter scanning or exploitation attempts. Exploit development has reached the level of reliable, widely-available, easy-to- use automated tools.

### Remediation Level (RL)
#### Not Defined (RL:X)
Assigning this value to the metric will not influence the score. it is a signal to a scoring equation to skip this metric.

#### Official fix (RL:O)
Acomplete vendor solution is available. Either the vendor has issued an official patch, or an upgrade is available.

#### Temporary fix (RL:T)
There is an official but temporary fix available. This includes instances where the vendor issues a temporary hotfix, tool, or workaround.

#### Workaround (RL:W)
There is an unofficial, non-vendor solution available. In some cases, users of the affected technology will create a patch of their own or provide steps to work around or otherwise mitigate the vulnerability.

#### Unavailable (RL:U)
There is either no solution available or itis impossible to apply.

### Report Confidence (RC)
#### Not Defined (RC:X)
Assigning this value to the metric will not influence the score. it is a signal to a scoring equation to skip this metric.

#### Unknown (RC:U)
There are reports of impacts that indicate a vulnerability is present. The reports indicate that the cause of the vulnerability is unknown, or reports may differ on the cause orimpacts, of the vulnerability. Reporters are uncertain of the true nature of the vulnerability, and there islittle confidence in the validity of the reports or whether a static Base score can be applied given the differences described

#### Reasonable (RC:R)
Significant details are published, but researchers either do not have full confidence in the root cause, or do not have access to source code to fully confirm all of the interactions that may lead to the result. Reasonable confidence exists, however, that the bugis reproducible and at least one impactis able to be verified (proof-of- concept exploits may provide this).

#### Confirmed (RC:C)
Detailed reports exist, or functional reproduction is possible (functional exploits may provide this). Source code is available to independently verify the assertions of the research, or the author or vendor of the affected code has confirmed the presence of the vulnerability.


# CVSS 3.1 Environmental Score Metrics
![[Pasted image 20220910144105.png]]

## Exploitability Metrics
### Attack Vector (MAV)
Used to modify the base attack vector settings.

#### Network (MAV:N)
Modified: A vulnerability exploitable with Network access means the vulnerable component is bound to the network stack and the attacker's path is through OSI layer 3 (the network layer). Such a vulnerability is often termed 'remotely exploitable’ and can be thought of as an attack being exploitable one or more network hops away (e.g. across layer 3 boundaries from routers).

#### Adjacent Network (MAV:A)
Modified: A vulnerability exploitable with Adjacent Network access means the vulnerable component is bound to the network stack, however the attack is limited to the same shared physical (e.g. Bluetooth, IEEE 802.11), or logical (e.g. local P subnet) network, and cannot be performed across an SI layer 3 boundary (e.g. a router).

#### Local (MAV)
Modified: A vulnerability exploitable with Local access means that the vulnerable component is not bound to the network stack, and the attacker's path is via read/write/execute capabilities. In some cases, the attacker may be logged in locally in order to exploit the vulnerability, or may rely on User Interaction to execute a malicious file.

#### Physical (MAV:P)
Modified: A vulnerability exploitable with Physical access requires the attacker to physically touch or manipulate the vulnerable component, such as attaching an peripheral device to a system.

### Attack Complexity (MAC)
Used to modify the base access complexity settings.

#### Low (MAC:L)
Modified: Specialized access conditions or extenuating circumstances do not exist. An attacker can expect repeatable success against, the vulnerable component.

#### High (MAC:H)
Modified: A successful attack depends on conditions beyond the attacker's control. That is, a successful attack cannot be accomplished at will, but requires the attacker to invest in some measurable amount of effort in preparation or execution against the vulnerable component before a successful attack can be expected.

### Privileges Required (MPR)
Used to modify the base privileges required settings.

#### None (MPR:N)
Modified: The attacker is unauthorized prior to attack, and therefore does not require any access to settings or files to carry out an attack.

#### Low (MPR:L)
Modified: The attacker is authorized with (i.e. requires) privileges that provide basic user capabilities that could normally affect only settings and files owned by a user. Alternatively, an attacker with Low privileges ‘may have the ability to cause an impact only to non-sensitive resources.

#### High (MPR:H)
Modified: The attacker is authorized with (i.e. requires) privileges that provide significant (e.g. administrative) control over the vulnerable component that could affect component-wide settings and files.

### User Interaction (MUI)
Used to modify the base user interaction settings.

#### None (MUI:N)
Modified: The vulnerable system can be exploited without interaction from any user.

#### Required (MUI:R)
Modified: Successful exploitation of this vulnerability requires a user to take some action before the vulnerability can be exploited, such as convincing a user to click a link in an email.

### Scope (MS)
Used to modify the base scope settings.

#### Unchanged (MS:U)
Modified: An exploited vulnerability can only affect resources managed by the same authority. In this case the vulnerable component and the impacted component are the same.

#### Changed (MS:C)
Modified: An exploited vulnerability can affect resources beyond the authorization privileges intended by the vulnerable component. In this case the vulnerable component and the impacted component are different.

## Impact Metrics
### Confidentiality Impact (MC)
Used to modify the base confidentiality requirement settings.

#### None (MC:N)
Modified: There is no loss of confidentiality within the impacted component.

#### Low (MC:L)
Modified: There is some loss of confidentiality. Access to some restricted information is, obtained, but the attacker does not have control over what information is obtained, or the amount or kind of loss is constrained. The information disclosure does not cause a direct, serious loss to the impacted component.

#### High (MC:H)
Modified: There is total loss of confidentiality, resulting in all resources within the impacted  component being divulged to the attacker. Alternatively, access to only some restricted information is obtained, but the disclosed information presents a direct, serious impact.

### Integrity Impact (MI)
Used to modify the base integrity impact settings.

#### None (MI:N)
Modified: There is no loss of integrity within the impacted component.

#### Low (MI:L)
Modified: Modification of data is possible, but the attacker does not have control over the consequence of a modification, or the amount of modification is constrained. The data modification does not have a direct, serious impact on the impacted component.

#### High (MI:H)
Modified: There is a total loss of integrity, or a complete loss of protection. For example, the attacker is able to modify any/all files protected by the impacted component. Alternatively, only some files can be modified, but malicious modification would present a direct, serious consequence to the impacted component.

### Availability Impact (MA)
Used to modify the base availability impact settings.

#### None (MA:N)
Modified: There is no impact to availability within the impacted component.

#### Low (MA:L)
Modified: There is reduced performance or interruptions in resource availability. Even if repeated exploitation of the vulnerability is possible, the attacker does not have the ability to completely deny service to legitimate users. The resources in the impacted component are either partially available all of the time, or fully available only some of the time, but overall there is no direct, serious consequence to the impacted component.

#### High (MA:H)
Modified: There is total loss of availability, resulting in the attacker being able to fully deny access to resources in the impacted component; this loss is either sustained (while the attacker continues to deliver the attack) or persistent (the condition persists even after the attack has completed). Alternatively, the attacker has the ability to deny some availability, but the loss of availability presents a direct, serious consequence to the impacted component (eg., the attacker cannot disrupt existing connections, but can prevent new connections; the attacker can repeatedly exploit a vulnerability that, in each instance of a successful attack, leaks a only small amount of memory, but after repeated exploitation causes a service to become completely unavailable).

## Impact Subscore Modifiers
### Confidentiality Requirement (CR)
#### Low (CR:L)
Loss of Confidentiality is likely to have only a limited adverse effect on the organization or individuals associated with the organization (e.g., employees, customers).

#### Medium (CR:M)
Loss of Confidentiality is likely to have a serious adverse effect on the organization or individuals associated with the organization (e.g., employees, customers).

#### High (CR:H)
Loss of Confidentiality is likely to have a catastrophic adverse effect on the organization or individuals associated with the organization (e.g., employees, customers).

### Integrity Requirement (IR)
#### Low (IR:L)
Loss of Integrity is likely to have only a limited adverse effect on the organization or individuals associated with the organization (eg. employees, customers).

#### Medium (IR:M)
Loss of Integrity is likely to have a serious adverse effect on the organization or individuals associated with the organization (e.g. employees, customers).

#### High (IR:H)
Loss of Integrity is likely to have a catastrophic adverse effect on the organization or individuals associated with the organization (eg. employees, customers).

### Availability Requirement (AR)
#### Low (AR:L)
Loss of availability is likely to have only a limited adverse effect on the organization or individuals associated with the organization (e.g., employees, customers).

#### Medium (AR:M)
Loss of availability is likely to have a serious adverse effect on the organization or individuals associated with the organization (e.g. employees, customers).

#### High (AR:H)
Loss of availability is likely to have a catastrophic adverse effect on the organization or individuals associated with the organization (e.g., employees, customers).