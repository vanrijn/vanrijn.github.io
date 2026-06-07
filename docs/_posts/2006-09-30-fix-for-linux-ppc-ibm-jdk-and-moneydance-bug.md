---
layout: post
title: Fix for Linux PPC, IBM JDK, and Moneydance Bug
date: 2006-09-30 16:24:58.000000000 -07:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/09/30/fix-for-linux-ppc-ibm-jdk-and-moneydance-bug/"
---

Wow. You know... I've worked around this annoyance for FAR too long... I'd [blogged previously](http://movingparts.net/2006/04/16/after-all-that-back-to-os-x/) (5 months + ago???) about a [bug that affects Moneydance](http://trac.moneydance.com/trac/ticket/569) with IBM's JRE/JDK (you know... the ONLY one that you can find for Linux PowerPC!!) with online transaction downloading. So I decided to poke at it a bit again today and what do you know? I found a solution! As it turns out, to solve the moneydance problem with SSLContext and IBM's JRE, change $JAVA_HOME/jre/lib/security/java.security like this:

> # diff -pruN java.security.original java.security --- java.security.original 2006-09-30 16:09:38.000000000 -0400 +++ java.security 2006-09-30 16:11:48.000000000 -0400 @@ -48,11 +48,11 @@ # # List of providers and their preference orders (see above): # -security.provider.1=com.ibm.jsse2.IBMJSSEProvider2 -security.provider.2=com.ibm.crypto.provider.IBMJCE -security.provider.3=com.ibm.security.jgss.IBMJGSSProvider -security.provider.4=com.ibm.security.cert.IBMCertPath -security.provider.5=com.ibm.security.sasl.IBMSASL +#security.provider.1=com.ibm.jsse2.IBMJSSEProvider2 +security.provider.1=com.ibm.crypto.provider.IBMJCE +security.provider.2=com.ibm.security.jgss.IBMJGSSProvider +security.provider.3=com.ibm.security.cert.IBMCertPath +security.provider.4=com.ibm.security.sasl.IBMSASL
>
>
> # # The entropy gathering device is described as a URL and can

Woohoo!! Mark that up to yet something else I should have figured out 5 months ago.... =:(
