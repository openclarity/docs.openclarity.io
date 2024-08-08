---
title: APIClarity
weight: 2000
github_project_repo: "https://github.com/openclarity/apiclarity/"
cascade:
  github_project_repo: "https://github.com/openclarity/apiclarity/"
---

APIClarity, an open source cloud native visibility tool for APIs, uses a Service Mesh framework to capture and analyze API traffic, and identify potential risks.

Use APIClarity to compare your OpenAPI specification to its state at runtime. For apps that don’t have an OpenAPI specification, APIClarity can reconstruct a specification in a live environment.

Cloud native applications use and expose APIs, which have been the source of many highly publicized cyber-attacks and breaches. APIClarity improves your API visibility and your applications security posture.

APIClarity is the tool responsible for API Security in the [OpenClarity platform](https://openclarity.io).

## Why APIClarity?

- **Quick and Easy API Visibility and Analysis**: Reduce API security risk without code instrumentation or workload modification.
- **Comprehensive Dashboard to Monitor APIs**: Evaluate OpenAPI specifications for security issues and best practices. Where there is no spec, automatically generate one.
- **Designed for Developers, Loved by Security**: Detect Zombie and Shadow APIs, alert users on risks, identify changes between approved OpenAPI specs and APIs at runtime.

### Challenges for API microservices

Microservice applications interact via API’s with many other applications. To minimize risk, it is valuable to have visibility to the OpenAPI specifications and to understand any potential changes to that specification throughout the application lifecycle. However, obtaining OpenAPI specs can be challenging, particularly for external or legacy applications.

Proper OpenAPI specifications can be further complicated by microservices that use deprecated APIs (a.k.a. Zombie APIs)​ or microservices that use undocumented APIs (a.k.a. Shadow APIs).

Finally, it’s important to be able to obtain Open API specifications without code instrumentation or modifying existing workloads.

- Not all applications have their Open API specification available.​
- How can we get this for our legacy or external applications?​​
- Ability to detect that microservices still use deprecated APIs (a.k.a. Zombie APIs)​​
- Ability to detect that microservices use undocumented APIs (a.k.a. Shadow APIs)​
- Ability to get Open API specifications without code instrumentation or modifying existing workloads (seamless documentation)

### How does APIClarity overcome these challenges?

- Capture all API traffic in an existing environment using a service-mesh framework​​
- Construct the Open API specification by observing the API traffic​​​
- Allow the User to upload Open API spec, review, modify and approve generated Open API specs​
- Alert the user on any difference between the approved API specification and the one that is observed in runtime, detects shadow & zombie APIs​
- UI dashboard to audit and monitor the API findings​

## Overview

<video src="/videos/apiclarity.mp4" style="width: 100%; height: 100%;" preload="auto" controls=""></video>

## High-level architecture

![APIClarity architecture](/img/carousel/APIsec.png)
