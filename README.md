# Wildfly 9 domain mode no cluster
This example configures Wildfly 9 domain with 2 slaves as described in a
book "Wildfly Cookbook", pages 83-93

HOW TO
------
```bash
1. Copy directories master, slave-1 and slave-2 to the Wildfly9 directory
2. Run domain controller: ./bin/domain.sh -Djboss.domain.base.dir=master
3. Run slave-1:
./bin/domain.sh -Djboss.domain.base.dir=slave-1 \
  -Djboss.domain.master.address=127.0.0.1
4. Run slave-2:
./bin/domain.sh -Djboss.domain.base.dir=slave-2 \
  -Djboss.domain.master.address=127.0.0.1
```

# Wildfly 9 standalone mode clustered
This example configures 2 standalone Wildfly 9 instances in a cluster as
described in a book "Wildfly Cookbook", pages 176-185
HOW TO
------
```bash
1. Copy directories cl-std-node-1 and cl-std-node-2 to the Wildfly9 directory
2. Run node-1:
./bin/standalone.sh -Djboss.server.base.dir=cl-std-node-1 \
  --server-config=standalone-ha.xml \
  -Djboss.socket.binding.port-offset=100 \
  -Djboss.node.name=node-1
3. Run node-2:
./bin/standalone.sh -Djboss.server.base.dir=cl-std-node-2 \
  --server-config=standalone-ha.xml \
  -Djboss.socket.binding.port-offset=200 \
  -Djboss.node.name=node-2
```
Visit http://localhost:8180/cluster-test/ and
http://localhost:8280/cluster-test/ for results

# Wildfly 9 domain mode clustered
This examples configures Wildfly 9 domain with no management console available
(due to no server configured) and 1 slave with 2 servers as described in a book
"Wildfly Cookbook", pages 193-203
HOW TO
------
```bash
1. Copy directories cl-dmn-master and cl-dmn-host-1 to the Wildfly9 directory
2. Run domain controller: ./bin/domain.sh -Djboss.domain.base.dir=cl-dmn-master
3. Run host-1:
./bin/domain.sh -Djboss.domain.base.dir=cl-dmn-host-1 \
-Djboss.domain.master.address=127.0.0.1
```
NOTE 1: you might have problems connecting slave to master due to both machenes
are on localhost. As a workaround I added 2 domain controllers to slave
host.xml so it searches for a DC longer
NOTE 2: to deploy a package I run following command from a shell:
```bash
./jboss-cli.sh --connect --command="deploy --force \
/home/jurikolo/wf_cookbook/wildfly902/cluster-test.war"
```

