# Meltdown & Spectre

[![LICENSE](https://img.shields.io/github/license/adamalston/Meltdown-Spectre?color=black)](LICENSE)

Meltdown and Spectre are the names given to different variants of the same fundamental underlying vulnerability that affects nearly every computer chip manufactured in the last two decades<sup id="r1">[[1]](#1)</sup>. If exploited, these vulnerabilities allow attackers to get access to data previously considered completely protected. Security researchers discovered the flaws late in 2017 and publicized them in early 2018. Technically speaking, there are three variations of the vulnerability, each given its own CVE number; two of these variants are grouped together as Spectre and the third is dubbed Meltdown.

Common Vulnerability and Exposure<sup id="r2">[[2]](#2)</sup> (CVE):
- Bounds Check Bypass: `CVE-2017-5753` (Spectre Variant 1)
- Branch Target Injection: `CVE-2017-5715` (Spectre Variant 2)
- Rogue Data Cache Load: `CVE-2017-5754` (Meltdown Variant 3)

All of the variants of this underlying vulnerability involve a malicious program gaining access to data that it shouldn't have the right to see, and do so by exploiting two important techniques used to speed up computer chips, called speculative execution and caching. 

In practice, Meltdown and Spectre are side-channel attacks on vulnerable CPU hardware implementations.  

## Meltdown

Meltdown is a bug that "melts" the security boundaries normally enforced by the hardware.

By exploiting Meltdown, an attacker can use a program running on a machine to gain access to data from all over that machine that the program shouldn't normally be able to see, including data belonging to other programs and data that only administrators should have access to. Meltdown doesn't require too much knowledge of how the program the attacker hijacks works, but it only works with specific kinds of Intel chips.

Caching is a technique used to speed up memory access. It takes a relatively long time for the CPU to fetch data from RAM, which lives on a separate chip, so there's a special small amount of memory storage called CPU cache on that lives on the CPU chip itself and that can be accessed very quickly. This memory gets filled with data that the chip will need soon, or often. What's relevant for this demonstration is that data that's output by speculative execution is often stored in cache, which is part of what makes speculative execution a speed booster.

The problem arises when caching and speculative execution start grappling with protected memory.

## Spectre

Spectre is a flaw an attacker can exploit to force a program to reveal its data. The name derives from "speculative execution" — an optimization method a computer system performs to check whether it will work to prevent a delay when actually executed.

Speculative execution involves a chip attempting to predict the future in order to work faster. If the chip knows that a program involves multiple logical branches, it will start working out the math for all of those branches before the program even has to decide between them. For instance, if the program says, "If A is true, compute function X; if A is false, compute function Y", the chip can start computing both functions X and Y in parallel, before it even knows whether A is true or false. Once it knows whether A is true or false, it already has a head start on what comes after, which speeds up processing overall. Or, in another variation, if a chip learns that a program makes use of the same function frequently, it might use idle time to compute that function even when it hasn't been asked to, just so it has what it thinks the answer will be on hand.

Spectre requires more intimate knowledge of the victim program's inner workings, and doesn't allow access to other programs' data. However, it will also work on just about any computer chip out there.

## Patches

Patches for Meltdown and Spectre generally mitigate the vulnerabilities by altering or disabling how software code makes use of the speculative execution and caching features built into the underlying hardware. The downside of this is that these features were designed to improve system performance, and so working around them can slow your systems down.

Apple<sup id="r3">[[3]](#3)</sup> did not go into detail about their specific mitigations, but did say that there was no measurable reduction in performance in iOS or macOS. They also released full mitigation<sup id="r4">[[4]](#4)</sup> which is the ability to enable an additional CPU instruction and disable hyper-threading processing technology. Full mitigation further prevents unauthorized applications from exploiting Meltdown and Spectre among other things.

Microsoft<sup id="r5">[[5]](#5)</sup> applied the following mitigations to Windows:

| Vulnerability | CVE | Public vulnerability name | Windows changes |
|:-|:-|:-|:-|
| Spectre Variant 1 | `CVE-2017-5753` | Bounds Check Bypass (BCB) | Recompiling with a new compiler<br>Hardened Browser to prevent exploit from JavaScript |
| Spectre Variant 2 | `CVE-2017-5715` | Branch Target Injection (BTI) | New CPU instructions eliminating branch speculation |
| Meltdown Variant 3 | `CVE-2017-5754` | Rogue Data Cache Load (RDCL) | Isolate kernel and user mode page tables |

Microsoft's patch for Spectre Variant 2 also included a firmware change. They have stated that users with older hardware (pre 2016) may experience decreases in system performance. Most users with Windows 10 on newer hardware would experience a negligible performance impact.

> **Note:** The attacks in this repository were carried out inside of a VM running an unpatched version of Linux. Of importance here is that even if the OS of the host machine is patched, the attack will work so long as the VM does not contain the patch.

---

### References

1. [^](#r1) <a href="https://www.csoonline.com/article/3247868/spectre-and-meltdown-explained-what-they-are-how-they-work-whats-at-risk.html" id="1">"Spectre and Meltdown explained: What they are, how they work, what's at risk"</a> <i>CSO</i>

2. [^](#r2) <a href="https://www.us-cert.gov/ncas/alerts/TA18-004A" id="2">"Meltdown and Spectre Side-Channel Vulnerability Guidance"</a> <i>Cybersecurity & Infrastructure Security Agency</i>

3. [^](#r3) <a href="https://support.apple.com/en-us/HT208394" id="3">"About speculative execution vulnerabilities in ARM-based and Intel CPUs"</a> <i>Apple</i>

3. [^](#r4) <a href="https://support.apple.com/en-us/HT210107" id="4">"Additional mitigations for speculative execution vulnerabilities in Intel CPUs"</a> <i>Apple</i>

5. [^](#r5) <a href="https://www.microsoft.com/security/blog/2018/01/09/understanding-the-performance-impact-of-spectre-and-meltdown-mitigations-on-windows-systems/" id="5">"Understanding the performance impact of Spectre and Meltdown mitigations on Windows Systems"</a> <i>Microsoft</i>

---

Thank you for your interest, this project was fun and insightful!
