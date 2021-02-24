# Jenkins Build Information

## Jenkins URL
- https://ci.eclipse.org/ee4j/

## Jenkins Jobs
* [EE4J parent POM build and release](https://ci.eclipse.org/ee4j/job/ee4j-parent-master/)
  * This job is intended to support building and releasing to staging the [EE4J Parent POM](https://github.com/eclipse-ee4j/ee4j/blob/master/parent/pom.xml).  It's triggered manually.  This job is used when the parent POM needs be versioned in [Maven Central](https://search.maven.org/artifact/org.eclipse.ee4j/project).
  
* [nexus-staging](https://ci.eclipse.org/ee4j/job/nexus-staging/)
  * This job is *supposed* to help release the staged artifacts to Maven Central.  The only action that seems to work is "list", which does help with listing the staged repositories.  But, to do the actual release of the desired staging repository, go directly to [Nexus](https://jakarta.oss.sonatype.org/#welcome).  (You will need separate Nexus credentials.)  Or, you are welcome to debug this Jenkins job to allow for a more seamless release process.
  
### Other Jenkins Jobs

* [copy_promoted_jakartaee8_eftl_bundles](https://ci.eclipse.org/ee4j/job/copy_promoted_jakartaee8_eftl_bundles/)
  * Old job that was possibly used with Jakarta EE 8.  No longer used?
  
* [copy_staged_jakartaee9_jaxb_tck](https://ci.eclipse.org/ee4j/job/copy_staged_jakartaee9_jaxb_tck/)
  * This job still may be used by the JAXB project.
