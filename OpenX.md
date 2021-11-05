# JEE to MP to Quarkus

## Motivation

* Current trend: Traditional App-Servers move to finer grained Services, JEE becomes `lightweight` with MicroProfile.
* Clumsy dev-experience with classic JEE Apps.
* Heard from cool things like Quarkus or WildFly 25 with bootable-jar and MicroProfile Support.
* Explore Quarkus and WildFly MicroProfile and find out, whether these runtimes could be next candidates in our stack. 

## Concerns

* Need to adapt all Java-Files.
* Need for proprietary Product-specific features like Annotations, Package-Imports.
* What happens when this cool hyped technology disappears in a few years?
* Are these technologies working with Baloise-specific Setups?

## Overview

| Technologie    | Proof of Concept Description |
| -------------- | -----------------------------|
| Quarkus        | Quarkus-starter with rest-endpoint and database-access |
| Quarkus Native | Quarkus-starter with rest-endpoint and database-access, native compiled |
| WildFly 25 MP  | WildFly 25 MP with rest-endpoint and database-access, Bootable-jar |
| WildFly 25 MP Native  | not available out of the box, could be achieved by huge manual effort |

## Assessment Criteria

- Developer experience
- Migration path for JEE-Apps
- Workload effects
- Oekosystem, Community, Perspectives
- Support Subscription

## Demo

- Quarkus dev-mode, some minor code-tweaks
- GitActions Workflow, Build-Steps, Container-Registry
- Demo-App served from OpenShift
- OpenShift Console App-Insights (Memory etc.)

## Comparison

tbd see [WildFlyAssessment.md](WildFlyAssessment.md) and [QuarkusAssessment](QuarkusAssessment.md)

## Conclusion

* Excited about quarkus.
* Try to port some non-critical Baloise Apps to Quarkus, collect more experiences.
