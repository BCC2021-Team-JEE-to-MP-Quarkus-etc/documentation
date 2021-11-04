# Persistence PoC with wildfly

Struggling to integrate `@Transaction` -Annotation. Solution was found by navigating to the `parent-parent-pom` to find out
which dependency is needed:
```pom
  <groupId>org.wildfly.bom</groupId>
  <artifactId>wildfly-jakartaee8</artifactId>
```

## Debugging:

Activated debug-agent works.  BUT: If the dev-watch mode is used, every code-change leads to a lost debug-connection. This is annoying.

## Persistence with standard JPA entities:

Implemented standard-jpa to serve book-list.

# Persistence PoC with quarkus

## Debugging:
- start quarkus as usual: `mvn quarkus:dev`
- In IntelliJ Menubar select: `Run/Attach to Process...` and choose the quarkus process from the list of the dialog
- Set breakpoints in the code and invoke a REST endpoint in the browser
- IntelliJ should stop at the breakpoint

## Persistence with standard JPA entities:

In addition to the PanacheEntity approach
we created a standard JPA entity JpaBook 


https://quarkus-starter.apps.okd.baloise.dev/
https://argocd.baloise.dev/applications/mp-wf-quarkus?resource=&view=network
https://console.baloise.dev/

