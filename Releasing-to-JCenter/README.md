# Releasing to JCenter and Maven

 - In order to publish jar and artifacts to JCenter we need to configure bintray
 - According to the droiddriver implementation, we have
   - separate jcenter.gradle with bintray configured
   - jcenter.gradle gets inputs from properties.gradle

bintray {
    publish = true
    configurations = ['archives']
    user = bintrayUser                       ---> properties.gradle
    key = bintrayKey                         ---> properties.gradle
    pkg {
        repo = 'maven'
        userOrg = 'appium'
        name = "${ddGroup}:${ddArtifactId}"  ---> properties.gradle
        websiteUrl = ddWebsite               ---> properties.gradle
        issueTrackerUrl = ddTracker          ---> properties.gradle
        vcsUrl = ddGit                       ---> properties.gradle
        desc = ddDescription                 ---> properties.gradle
        licenses = ['The Apache Software License, Version 2.0']
        publicDownloadNumbers = true
        version {
            name = ddVersion                 ---> properties.gradle
            desc = ddDescription             ---> properties.gradle
        }
    }
}

## properties.gradle

ext.ddArtifactId  = 'droiddriver'
ext.ddGroup       = 'io.appium'
ext.ddVersion     = '1.0.0-SNAPSHOT'
ext.ddWebsite     = 'https://github.com/appium/droiddriver'
ext.ddTracker     = 'https://github.com/appium/droiddriver/issues'
ext.ddGit         = 'https://github.com/appium/droiddriver.git'
ext.ddDescription = 'Android UI testing framewo


 - Creating a release on jcenter is done by
   - gradle -PbintrayUser=myusername -PbintrayKey=123 clean bintrayUpload
 - Artifacts uploaded in bintray can be synced with maven central using sync feature
   - Sync requires maven username to be entered in bintray profile.

