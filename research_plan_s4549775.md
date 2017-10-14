---
title: Research Plan
author: Hendrik Werner s4549775
date: \today
bibliography: references.bib
fontsize: 12pt
geometry: margin=5em
header-includes:
	- \usepackage{pgfgantt}
---

Author=Hendrik Werner

Topic=IPv10

Academic year::2017-18

---

# Topic

I want to investigate whether the proposed IPv10 standard solves the communication and transition problems between IPv4 and IPv6, that it claims to solve.

Should the IPv10 draft be accepted and implemented as a solution to the current communication and transition problems between IPv4 and IPv6?

# Problem

IPv4 does not have sufficient address space to accommodate the number of Internet connected devices in use today [@rfc1550]. Therefore a new standard was published, called IPv6. Along with a much bigger address space, IPv6 simplifies the protocol, and corrects several design flaws in the original IPv4 specification, like the header checksums. [@rfc2460]

IPv10 was recently proposed to ease IPv4 and IPv4 coexistence and transition. It claims to be superior to existing solutions. [@ipv10draft]

Does IPv10 meet its declared goals?

* Is the proposed solution more efficient than currently used ones?
* Does it allow for communication between all types of hosts?
	* IPv4 / IPv4
	* IPv4 / IPv6
	* IPv6 / IPv4
	* IPv6 / IPv6
* Does it increase flexibility when using DNS?
* Does it solve the transition problem?
* Is it easy to deploy to all Internet connected hosts?

# Relevance

IPv4 is indisputably insufficient for the current Internet landscape. This problem was recognized a long time ago and a new standard was invented called IPv6.

There is the problem of transitioning from one protocol to the other though. Despite ongoing efforts the adoption of IPv6 is not nearly as universal as many had hoped. Currently there are several workarounds in use for reconciling the communication between hosts using different protocols, and to ease the transition.

The Internet is far too complex, big, and diverse to allow for a "switch day" as proposed before. The workarounds are mostly ad hoc, or complex, and don't solve many of the problems. The number of IPv6 hosts is still increasing only very slowly.

The IPv10 proposal claims to solve the communication and transition problems, while being easy to deploy, efficient, and flexible. It is important to test these claims in order to decide whether to officially adopt the standard, and to ultimately finally solve the problems with IPv4 that were identified decades ago. [@ipv10draft]

# Theoretical Background

Both IPv4 [@rfc791] and IPv6 [@rfc2460] were introduced through RFCs (request for comment), which are the usual publication medium for standards by the IETF (Internet engineering task force). The RFCs were proposed and went through several rounds of comments, and changes, until they got accepted and published in their final form.

We want to subject the IPv10 proposal to the same scrutiny, in order to decide whether to adopt it as the new standard Internet protocol. There are several established methods to deal with coexistence, as well as transition of IPv4 and IPv6 hosts. Therefore we not only want to test whether the claims made in the proposal hold up, but also how the new protocol compares to existing solutions, currently deployed.

IPv4 and IPv6 use different, incompatible header formats, which is the reason for all the communication and transition problems [@rfc6219]. The main reason for this incompatibility is the different address space. IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses [@rfc791; @rfc2460; @rfc6219].

It became apparent very quickly that a "switch day" was unrealistic, because of the diversity, number of hosts, and complexity of the Internet. Even before specifying IPv6, the IETF published an RFC dealing with the addressing architecture that was going to be used in IPv6. It contains two forms of transitional IPv6 addresses, termed "IPv4-compatible IPv6 addresses", and "IPv4-mapped IPv6 addresses". These contain 32-bit IPv4 addresses embedded in the 128-bit IPv6 addresses. [@rfc1884]

Embedding IPv4 addresses, like every fixed translation scheme, leads to the same problem Dual Stack also has [@tsuchiya2000], namely no increase in the usable address space, as every IPv6 address using this mechanism, must have a corresponding IPv4 address. [@rfc1884]

From the beginning it was clear that these measures were not really satisfactory, and only transitional. The main factor that required the specification of a new Internet Protocol was the limited address space of IPv4 [@raicu2003]. IPv4 offers only $2^{32} = 4294967296 \approx 4.3bn$ addresses [@rfc791]. This seemed like a lot back when it was specified, but turned out not to be sufficient with the prevalence of the Internet and Internet connected devices.

There are several currently available transition mechanisms, like IPv4/IPv6 Dual Stack, NAT, \dots. Most of these mechanisms have major drawbacks however, regarding complexity, scaling, authentication, \dots. [@raicu2003; @rfc6052]

The two most promising transition mechanisms are *host-to-host encapsulation* (6-over-4) and *router-to-router encapsulation* (IPv6 in IPv4 tunneling).

> In the host-to-host encapsulation method, the encapsulation is done at the source host and the decapsulation is done at the destination host. The encapsulated datagrams are sent through a native IPv4 network that has no knowledge of the IPv6 network protocol.
[@raicu2003]

> In router-to-router tunneling mechanism, encapsulation is done at the edge router of the originating host and decapsulation is done at the edge router of the destination host.
[@raicu2003]

Host-to-host encapsulation performs better with regards to latency, throughput, and connection time, but leads to large increases in the CPU utilization of the hosts [@raicu2003]. This is based on a benchmark done on Windows 2000 though, so it may be outdated.

As far back as 2000, only two years after the specification of IPv6 was complete [@rfc2460], patents have been granted for an "IPv4-IPv6 converting apparatus" that works around some of the issues with conventional transitional measures. It is relatively complicated, and requires a dedicated converter sitting between the IPv4 and IPv6 hosts. [@tsuchiya2000] Another big drawback is that the technology is patented.

There are a lot of legacy devices in use that do not support IPv6, and probably never will. We cannot wait for all legacy devices to be replaced before moving on from IPv4. Every solution requiring both hosts to be aware is therefore inherently flawed. A satisfactory solution must work transparently for IPv4 hosts.

IPv10 promises a superior solution to any of the previously named, in multiple aspects [@ipv10draft]. There is not much empirical evidence for these claims at the moment, as IPv10 is a very recent proposal. We want to change that with our research.

# Method

The research method we want to use is a case study, in which we transition (some part of) the university network from dual stack to IPv10. We will evaluate the difficulties we encounter on the way, as well as performance improvements in the categories of flexibility, efficiency, as well as ease of deployment.

Currently there is no implementation of IPv10 available, so we will have to employ the "design and creation" strategy to produce an artifact, which will be an IPv10 based network layer implementation.

We will also do a survey of members of the C&CZ, to gather additional data about problems occurring after deployment, and in the maintenance phase.

# Planning

We plan on conducting our research over the course of 12 weeks.

To deploy an IPv10 solution we first need to create an implementation of the spec, as there is currently none available. To this end we first design a system that fulfills the requirements of the IPv10 specification draft. Then we begin implementing that design, while continually testing that no regressions occur, and we adhere to the spec.

When we have a working artifact, shortly before the implementation phase is finished, we can commence with the deployment stage. First we need to deliberate with the C&CZ about which part of the network to deploy IPv10 to. Ideally it should be a nonessential, but frequently used area, so that we can gather sufficient information without interrupting academic work, in case something goes wrong. Then we deploy the IPv10 implementation to this part of the network, and finally we test the subnetwork.

During the whole 12 weeks, we will be writing our article. In the Gantt chart this is indicated as "general" article writing. We split this up into a few subtasks, to specifically focus on certain parts of the article. For example, in week 1 and 2 we want to focus on the Introduction, Abstract, etc. We will be working on, and refining the whole article continuously, however.

\begin{center}
\begin{ganttchart}[
	vgrid,
	x unit = 2em,
]{1}{12}
	\gantttitlelist{1, ..., 12}{1}\\
	\ganttgroup{IPv10 Implementation}{1}{6}\\
	\ganttbar[name=imp_design]{System Design}{1}{2}\\
	\ganttbar[name=imp_testing]{Testing}{3}{6}\\
	\ganttbar[name=imp_implementation]{Implementation}{3}{6}\\
	\ganttlink[link type=f-s]{imp_design}{imp_testing}
	\ganttlink[link type=f-s]{imp_design}{imp_implementation}
	\ganttlink[link type=f-f]{imp_testing}{imp_implementation}
	\ganttgroup{Deployment}{6}{9}\\
	\ganttbar[name=dep_deliberation]{Deliberation}{6}{6}\\
	\ganttbar[name=dep_deployment]{Deployment}{7}{8}\\
	\ganttbar[name=dep_testing]{Testing}{8}{9}\\
	\ganttgroup{Survey}{9}{11}\\
	\ganttbar[name=sur_sending]{Sending out Survey}{9}{9}\\
	\ganttbar[name=sur_answering]{Answering}{9}{10}\\
	\ganttbar[name=sur_evaluation]{Evaluation}{9}{11}\\
	\ganttlink[link type=s-s]{sur_sending}{sur_answering}
	\ganttlink[link type=s-s]{sur_answering}{sur_evaluation}
\end{ganttchart}
\end{center}

# Literature
