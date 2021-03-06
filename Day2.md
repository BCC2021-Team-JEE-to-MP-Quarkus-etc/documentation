# Implement quick-start with wildfly 25

After intensive readings to the [Wildfly-Docs](https://docs.wildfly.org/bootablejar/#wildfly_jar_examples_download),
we understood the concept specifying the requirements that make up the wildfly-server used in the bootable jar.

There are Feature-Specs containing Galleon Layers. One can define own Feature-Specs that can be
included in the spec how the server should be built.

The cool part is the declarative way adding "layers" in the maven pom [wildfly-jar-maven-plugin](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/wf-starter/blob/main/pom.xml).
In the dev-watch mode, changes to the layer-specs automatically rebuilds the app.

The roundtrip time in dev-watch mode, providing updates to the current running server, feels a bit lazy compared
to the quarkus quick-start example.

## Build Dockerfile, integrate in GitHub Build-Pipeline

The [ci-build.yml](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/wf-starter/blob/main/.github/workflows/ci-build.yml) provides a similar ci-workflow that builds up 
a docker-image provided via 
[GitHub Container Registry](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/wf-starter/pkgs/container/wf-starter)

## Add Database-Connectivity

The already defined postgresql-datasource was failing to be connected during server-start. This step provides a locally
provided PostgreSQL instance startet with [Docker Compose](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/wf-starter/blob/main/docker-compose.yaml)
This uses the [Dockerfile](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/wf-starter/blob/main/src/main/docker/Dockerfile) (no `docker build` required in advance).

## Publish to Openshift

Provide new PostgreSQL instance using simple 
[deployment, service, pvc and init-config yamls](https://github.com/baloise-incubator/code-camp-apps/tree/master/mp-wf-quarkus/templates)

Add wf-starter app to [Chart.yaml](https://github.com/baloise-incubator/code-camp-apps/blob/master/mp-wf-quarkus/Chart.yaml)
and [values.yaml](https://github.com/baloise-incubator/code-camp-apps/blob/master/mp-wf-quarkus/values.yaml) in our
[OKD4 Deployment Repo](https://github.com/baloise-incubator/code-camp-apps/tree/master/mp-wf-quarkus)

### Test deployed application

[wf-quickstart homepage](https://wf-starter.apps.okd.baloise.dev/)
[wf-quickstart hello path](https://wf-starter.apps.okd.baloise.dev/api/hello)

# Persistence PoC with quarkus
The code can be found in the quarkus-starter project on branch _persistence_
[quarkust-starter_persistence](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/tree/persistence)

Detailed Information can be found here: [README_persistence.md](https://github.com/BCC2021-Team-JEE-to-MP-Quarkus-etc/quarkus-starter/blob/persistence/README_persistence.md)

# Questions / Conclusions

## Quarkus persistence entity-key mapped to null

### Issue
With PanacheEntity, we had an issue with the id-column and autogenerated key. In the postgreSQL schema, we defined
```sql
id serial primary key
```
### Solution
The mapping in the `Book` class wasn't able to map because we didn't define `@GeneratedValue(strategy = GenerationType.IDENTITY)`
After the change the extension from `PanacheEntity` to `PanacheEntityBase`, we could annotate the id-field as expected.

