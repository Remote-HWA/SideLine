# SideLine 

To meet the ever-growing need for performance in silicon devices, SoC providers have been increasingly relying on software-hardware cooperation. By controlling hardware resources such as power or clock management from the software, developers earn the possibility to build more flexible and power efficient applications. Despite the benefits, these hardware components are now exposed to software code and can potentially be misused as open-doors to jeopardize trusted environments, perform privilege escalation or steal cryptographic secrets. In this work, we introduce SideLine, a novel side-channel vector based on delay-line components widely implemented in high-end SoCs. After providing a detailed method on how to access and convert delay-line data into power consumption information, we demonstrate that these entities can be used to perform remote power side-channel attacks. We report experiments carried out on two SoCs from distinct vendors and we recount several core-vs-core attack scenarios in which an adversary process located in one processor core aims at eavesdropping the activity of a victim process located in another core. For each scenario, we demonstrate the adversary ability to fully recover the secret key of an OpenSSL AES running in the victim core. Even more detrimental, we show that these attacks are still practicable if the victim or the attacker program runs over an operating system.

## Victim Project
![VICTIM_PROGRAM_CREATION](https://user-images.githubusercontent.com/67143135/85423468-04885280-b577-11ea-8fbd-bd365845c6ec.png)

## Attack Project
![ATTACK_PROGRAM_CREATION](https://user-images.githubusercontent.com/67143135/85423382-ec183800-b576-11ea-891c-488eb2b538dd.PNG)
