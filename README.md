Discard Old Build plugin
===========================

Pantheon's fork of a Jenkins plugin to discard old builds with detailed configuration.

We have added the option to discard all successful builds, beyond a certain number of kept builds. The existing plugin did not support this functionality out of the box.

Typically we would want to configure our frequently-run jobs using this plugin option set to some numerical limit, e.g. 1000. The most recent 1000 builds will be kept, and then all successful builds beyond 1000 will be deleted. This will leave only the failed, aborted, etc. builds in the range of 1000+. Using it with Jenkin's default option `Discard Old Builds` with a higher limit, say 4000, and the net affect will be that we have unsuccessful builds saved for far longer.


Developing
----------

Clone the repo, then build the plugin, which will run the tests:

    mvn install

Copy the .hpi plugin file to the Jenkins home, "pin" it, and then restart Tomcat to make it available in the Jenkins interface:

    touch /opt/jenkins/plugins/discard-old-build.hpi.pinned
    sudo cp discard-old-build-plugin/target/*.hpi /opt/jenkins/plugins/
    sudo systemctl restart tomcat


What's this?
-------------

Discard Old Build is a [Jenkins](http://jenkins-ci.org/) plugin.
This plugin provides a post-build step where you can discard old build results.

* You can configures in more detail than the default 'Discard Old Build' function.
* Other than # of builds and days, you can specify build status to discard.
* For older builds, you can configure interval to keep builds (once in a month, once in ten builds...).
* You can also delete builds which has logfile size smaller or larger than specified bytes
* Or use Regular expression to parse log file for builds to discard
*
* Notes:
* Multi discard conditions can be selected and right now they are executed in order showing in UI
* Builds in Last are always kept


TODO
----
* Add help files
* Dynamic add discard condition in UI which decides the discard priority


