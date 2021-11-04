# Quarkus Hand-On with experts from Red Hat

_Developing with Quarkus: Supersonic Subatomic Java Hands-On Workshop_

**Torben Jäger**
Red Hat, Principal Specialist Solution Architect

## Bullet points

### Developer experience

* Minimal configuration-effort compared to JBoss/Wildfly (fully support for Config-Microprofile)
* Smooth Dev-Experience (dev-mode). Very short roundtrip (code, save, compile, redeploy, test) runs implicit after 
  change of source-files.
* No Server-Restarts needed during code-changes.

### Migration path for JEE-Apps
* Most important JEE-Specs (jakartaee) are available (like jpa, hibernate, cdi, jax-rs) and therefore quarkus is
  a valuable migration-path-candidate for legacy jee-apps.
* JEE-Features like @EJB, @Stateless etc, must be replaced by its corresponding implementations like cdi.
* Manually implemented features like health-checks, open-api, oidc, http-client, configuration 
  can be replaced by Microprofile features.

### Workload effects

* Provides both: `classic jvm` and `native binary` -mode
* Classic mode supports even dynamic code like reflection, class.forName etc.
* Native mode is limited. Quarkus-Extensions addresses this limitation. 
  Most used apis/libraries are available already and the number of extensions is growing fast.
* Optimized Java-Runtime for containerized usage (even in non-native mode)
* Ready to serve fast starting serverless-functions (knative etc.)
* Native-Mode designed for short living processes (minimal memory-footprint)
* Long-living processes in classic jvm-mode can outperform native-mode in terms of optimized memory-management.

### Beyond Quarkus

* Decoupled from Oracle GraalVM by integrating relevant features into OpenJDK.
* Growing ecosystem supported by curated documentation of how to implement Quarkus-Extensions. 
* Quarkus-Extensions for Spring Data and more is, or will be available.
* Keycloak will be ported to Quarkus-Native distribution.