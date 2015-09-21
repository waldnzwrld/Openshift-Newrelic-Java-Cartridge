OpenShift New Relic Java Agent cartridge
===================================

An embedded cartridge to enable New Relic Monitoring for Java applications deployed on OpenShift JBoss cartridges.

The cartridge installs the latest release of the New Relic for Java agent, property of New Relic. https://docs.newrelic.com/docs/release-notes/agent-release-notes/java-release-notes
To see detailed information about usage conditions see https://docs.newrelic.com/docs/licenses/licenses

Requirements
------------

- A [New Relic](http://www.newrelic.com/) account.
- OpenShift JBoss AS/EAP/EWS as primary cartridge.


Install
-------

- Install the cartridge from GitHub.

```
  rhc cartridge-add -a <your_app_name> \
    -e OPENSHIFT_NEWRELIC_LICENSE_KEY=<your_new_relic_key> \
    -c https://raw.githubusercontent.com/waldnzwrld/Openshift-Newrelic-Java-Cartridge/master/metadata/manifest.yml
```

- Restart your application.

```
  rhc app restart <your_app_name>
```

Remove
------

```
  rhc cartridge-remove newrelic -a <your_app_name>
```

Known Issues
------------

* A **JAVA\_OPTS\_EXT** user defined environment variable will override the one defined by the cartridge, so you could inadvertently disable the agent. Since the New Relic for Java agent requires a JVM flag to be written to your JAVA\_OPTS\_EXT a backup of this file is written to your newrelic directory and then moved into place again on teardown. To add extra JVM arguments to your startup, you should echo them into the file  echo "my:jvm-argument" >> ${OPENSHIFT\_HOMEDIR}.env/user_vars/JAVA\_OPTS\_EXT" Any arguments which were added after this cartridge is installed, will need to be added again if the cartridge is removed. 