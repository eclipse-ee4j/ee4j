# Eclipse Enterprise for Java (EE4J)

Eclipse Enterprise for Java (EE4J) is an open source initiative to create standard APIs, implementations of those APIs, and technology compatibility kits for Java runtimes that enable development, deployment, and management of server-side and cloud-native applications.  EE4J is based on the Java™ Platform, Enterprise Edition (Java EE) standards, and uses Java EE 8 as the baseline for creating new standards.

This organization provides a home for Git repositories that implement the various APIs, TCKs, and RIs for the related specifications.

Please see the [Eclipse EE4J Project](https://projects.eclipse.org/projects/ee4j).

[EE4J/Jakarta EE Wiki](https://wiki.eclipse.org/Category:Jakarta_EE)

## Release process for EE4J projects

The following sequence diagram illustrates the release process that is supported by this project and how the various profiles are intended to be used.

```mermaid
    sequenceDiagram
        actor Committer
        participant Project
        participant Staging@{ "type" : "database" }
        participant MavenCentral@{ "type" : "database" }
        actor Consumer
        loop development
            note left of Committer: v: X.Y.Z-SNAPSHOT
            Committer->>Project: merge pull request
            Project->>MavenCentral: mvn -Poss-release clean deploy 
            Consumer->>MavenCentral: mvn -Psnapshots ...
            Committer->>Committer: open new pull request
        end
        loop stage
            note left of Committer: v: X.Y.Z
            Committer->>Project: merge pull request
            Project->>Staging: mvn -Pstage-release clean deploy
            Consumer->>Staging: mvn -Pstaged ...
            Consumer->>Committer: request change
            Committer->>Committer: open new pull request
        end
        alt isStaged
            note left of Committer: v: X.Y.Z
            Committer->>Project: staged release verified
            Staging->>MavenCentral: mvn -Ppromote-stage clean deploy
            Consumer->>MavenCentral: mvn ... (generally available)
        else isNotStaged
            note left of Committer: v: X.Y.Z
            Committer->>Project: request release without staging
            Project->>MavenCentral: mvn -Poss-release clean deploy
            Consumer->>MavenCentral: mvn ... (generally available)
        end
        Committer->>Committer: update version
```