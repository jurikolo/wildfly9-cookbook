# wildfly9-domain-example
This is example of how to setup Wildfly 9 domain with 2 slaves as described in
book "Wildfly Cookbook", pages 83-93

HOW TO
------
1. Copy directories master, slave-1 and slave-2 to the Wildfly9 directory
2. Run domain controller: ./bin/domain.sh -Djboss.domain.base.dir=master
3. Run slave-1:
./bin/domain.sh -Djboss.domain.base.dir=slave-1 -Djboss.domain.master.address=127.0.0.1
4. Run slave-2:
./bin/domain.sh -Djboss.domain.base.dir=slave-2 -Djboss.domain.master.address=127.0.0.1
