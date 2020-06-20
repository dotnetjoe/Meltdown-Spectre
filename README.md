# Meltdown & Spectre

[![LICENSE](https://img.shields.io/github/license/adamalston/Meltdown-Spectre?color=black)](LICENSE)

## Meltdown

The Meltdown attack exploits critical vulnerabilities existing in many modern processors, including those from Intel and ARM. These vulnerabilities allow a user-level program to read data stored inside the kernel memory. The vulnerabilities were discovered in 2017 and publicly disclosed in January 2018.

Such access is not allowed by the hardware protection mechanism implemented in most CPUs, but a vulnerability exists in the design of these CPUs that makes it possible to defeat the hardware protection.

Because the flaw exists in the hardware, the fundamental safeguard is to replace the CPU. However, that is an insurmountable task to accomplished given the tens of millions of CPUs that would need to be replaced.

The Meltdown vulnerability represents a special genre of vulnerabilities in the design of CPUs.

## Spectre

The Spectre attack exploits critical vulnerabilities existing in many modern processors, including those from Intel, AMD, and ARM. Much like Meltdown, this attacks was discovered in 2017 and publicly disclosed in January 2018. 

The vulnerabilities allow a program to break inter-process and intra-process isolation, so a malicious program can read the data from an process that is not accessible to it. This level of access is not allowed by the hardware protection mechanism (for inter-process isolation) or software protection mechanism (for intra-prcess isolation), but a vulnerability exists in the design of CPUs that makes it possible to defeat these protections.

As with Meltdown - because the flaw exists in the hardware, the fundamental safeguard is to replace the CPU. However, that is an insurmountable task to accomplished given the tens of millions of CPUs that would need to be replaced.

The Spectre vulnerability represents a special genre of vulnerabilities in the design of CPUs.

---

> Given that this attack was conducted inside of a VM running Linux, even if the OS of the host machine is patched, the attack will still work.