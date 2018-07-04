# Releasing

## Requirements

* read [Deploying to OSSRH with Apache Maven](https://central.sonatype.org/pages/apache-maven.html)
* read [Maven: Guide to uploading artifacts to the Central Repository](https://maven.apache.org/repository/guide-central-repository-upload.html)
* GPG
    * install GPG
    * [generate key](https://help.github.com/articles/generating-a-new-gpg-key/)
    * setup Git so all your commits are auto-signed with GPG
* Create [JIRA account here](https://issues.sonatype.org/projects/MVNCENTRAL/summary)
    * Someone that already has access has to request that access to the maven repository is given to you

## Configuration

* get `ossrh` credentials are username and password for your [JIRA account](https://issues.sonatype.org/projects/MVNCENTRAL/summary)
* get the `gpg.keyname` from `gpg --list-secret-keys --keyid-format LONG`, see [Github help](https://help.github.com/articles/generating-a-new-gpg-key/)
* create `~/.m2/settings.xml` with at the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <servers>
    <server>
      <id>ossrh</id>
      <username>my-jira-username</username>
      <password>my-jira-password</password>
    </server>
  </servers>

  <profiles>
    <profile>
      <id>ossrh</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <gpg.keyname>my-key</gpg.keyname>
        <gpg.passphrase>secret</gpg.passphrase>
      </properties>
    </profile>
  </profiles>

</settings>
```

## Execution

1. Builds the artifacts, modifies `pom.xml` and pushes new tag to Github - warning, this creates commits!

```bash
mvn release:clean release:prepare
```

2. Release to maven repository

```bash
mvn release:perform
```

3. profit


## Notes

* maven repository setup [OSSRH-33874](https://issues.sonatype.org/browse/OSSRH-33874)
