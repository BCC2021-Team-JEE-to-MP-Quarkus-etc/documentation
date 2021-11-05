# WildFly 25 Assessment

## Developer experience

* Heavy configuration-effort compared to Quarkus or Spring
* Improved Dev-Experience (dev-mode) compared to classic JBoss standalone remote-debug. Short roundtrip (code, save, compile, redeploy, test) runs implicit after 
  change of source-files.
* No Server-Restarts needed during code-changes.

## Migration path for JEE-Apps
* All JEE-Specs (jakartaee) are available (like jpa, hibernate, cdi, jax-rs) and therefore WildFly is
  a valuable migration-path-candidate for legacy jee-apps.
* Manually implemented features like health-checks, open-api, oidc, http-client, configuration 
  can be replaced by Microprofile features.

## Workload effects

* Optimized packaging leads to reduced footprint, but still starting from 200Mi+
* Supports layered image-creation

## WildFly Ecosystem

* Small community, a few Core-Committer. 
* Well curated documentation.
* WildFly seems to be very early adopter of MicroProfile Implementations 
