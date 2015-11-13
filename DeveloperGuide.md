﻿PuMuKIT-2 Developer & Architecture Guide
========================================

*This page is updated to the 2.1.0*

Architecture
============

Technologies
------------

PuMuKIT-2 has been built using the below technologies. It is recommended to read the documentation of each technology in order to extend PuMuKIT-2 or create new features.

* Symfony 2.6: [web](http://symfony.com) | [doc](http://symfony.com/doc/2.6/index.html)
* PHP5: [web](http://php.net/) | [doc](http://php.net/manual/en/)
* MongoDB 3.0: [web](https://www.mongodb.org/) | [doc](https://docs.mongodb.org/v3.0/)
* Doctrine MongoDB ODM 1.0: [web](http://www.doctrine-project.org/projects/mongodb-odm.html) | [doc](http://doctrine-mongodb-odm.readthedocs.org/en/latest/)
* Bootstrap: [web](http://getbootstrap.com/) | [CSS doc](http://getbootstrap.com/css/) | [Components doc](http://getbootstrap.com/components/) | [JavaScript doc](http://getbootstrap.com/javascript/)
* Material Design [web](http://www.google.com/design/spec/material-design/introduction.html) | [doc](https://fezvrasta.github.io/bootstrap-material-design/)
* FFmpeg: [web](https://www.ffmpeg.org/) | [doc](https://www.ffmpeg.org/documentation.html)
* libav: [web](https://libav.org/) | [doc](https://libav.org/documentation/)


List of Bundles
---------------

PuMuKIT-2 has been developed with the Symfony framework. Symfony 2.x is based on bundles, and so, PuMuKIT-2 is structured in bundles. There is a list of bundles that come activated by default with the project, these are mandatory for the code to work. There is also a list of optional bundles that come deactivated. In order to install/activate them, follow the instructions in the guide of each bundle.

Activated by default:
* EncoderBundle: provides a service to encode audio/video tracks.
* ExampleDataBundle: provides a command to add example data on a new installation on the instance.
* InspectionBundle: provides a service to inspect multimedia tracks.
* InstallBundleBundle: provides a command to install new bundles into the PuMuKIT-2 project.
* LiveBundle: provides a service to show live stream events.
* NewAdminBundle: provides the back-office admin UI.
* [OpencastBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/OpencastBundle/Resources/doc/ConfigurationGuide.md): provides a service to import multimedia content of an Opencast Server.
* SchemaBundle: defines the schema of classes and services.
* StatsBundle: provides a service to log the statistics.
* [WebTVBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/WebTVBundle/Resources/doc/OverrideGuide.md): defines the portal web.
* WizardBundle: provides a service to guide the user on uploading multimedia content.
* [WorkflowBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/WorkflowBundle/Resources/doc/ConfigurationGuide.md): provides a service to automatically extract a picture from a video that just has been transcoded if the MultimediaObject does not have any picture yet.


Not activated by default:
* [ArcaBundle](https://github.com/campusdomar/PuMuKIT2/blob/2.1.x/src/Pumukit/ArcaBundle/Resources/doc/InstallationGuide.md): provides a service to add RSS for the Academic Community.
* [LDAPBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/LDAPBundle/Resources/doc/AdminGuide.md): provides a service to connect to a LDAP Server and to retrieve data from the server.
* [NotificationBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/NotificationBundle/Resources/doc/AdminGuide.md): sends emails when a job finished, whether it failed or succeed
* [PodcastBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/PodcastBundle/Resources/doc/InstallationGuide.md): provides a service to add PuMuKIT videos into Podcast channel.

Third party bundles:
* [List of third party bundles](ThirdPartyBundlesGuide.md)


List of Events
--------------

Custom events added to PuMuKIT-2:
* *multimediaobject.update*: thrown each time a multimedia object is updated.
* *multimediaobject.view*: thrown each time a multimedia object is played in the webtv portal.
* *job.success*: thrown each time a job is finished successfully in the system.
* *job.error*: thrown each time a job fails in the system.

To add more events, read the Symfony documentation about creating [custom events](http://symfony.com/doc/current/components/event_dispatcher/introduction.html#creating-and-dispatching-an-event) and [listeners](http://symfony.com/doc/current/cookbook/event_dispatcher/event_listener.html).


How to extend Pumukit
=====================

Best practices:
* Do not modify PuMuKIT-2 Bundles, extend them following the Symfony documentation about [overriding Bundles](http://symfony.com/doc/current/cookbook/bundles/inheritance.html).
* Create your own Bundles and add them to the PuMuKIT-2 project.
* All the bundles created or overridden should be inside an organization directory:

```
src/Pumukit/ExampleOrg/Feature1Bundle
src/Pumukit/ExampleOrg/Feature2Bundle
src/Pumukit/ExampleOrg/Feature3Bundle
...
```


Override a Bundle
-----------------

See an example in [WebTVBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/WebTVBundle/Resources/doc/OverrideGuide.md).


Create a new Bundle
----------------------

#### 1.1 Generate the bundle.

`
$ php app/console  generate:bundle --namespace=Pumukit/ExampleOrg/FeatureBundle --dir=src --no-interaction
`

#### 1.2 Install the new bundle (if necessary).
`
$ php app/console  pumukit:install:bundle Pumukit/ExampleOrg/FeatureBundle/PumukitExampleOrgFeatureBundle
`

#### 1.3 Develop the bundle

Create all Documents, [Services](http://symfony.com/doc/current/book/service_container.html), Events, Event Listeners, [Controllers](http://symfony.com/doc/current/book/controller.html), [Commands](http://symfony.com/doc/current/bundles/SensioGeneratorBundle/commands/generate_command.html) and HTML Twig templates as needed, following the bundles structured defined by Symfony.

Examples
--------

* [Cmar/LiveBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/Cmar/LiveBundle/Resources/doc/AdminGuide.md) overrides LiveBundle.
* Cmar/SonarBundle is a new Bundle for Cmar organization.
* [Cmar/WebTVBundle](https://github.com/campusdomar/PuMuKIT2/blob/master/src/Pumukit/Cmar/WebTVBundle/Resources/doc/AdminGuide.md) overrides WebTVBundle



Main URLs of a PuMuKIT deployment
---------------------------------
* Web Portal: `http://{MyPuMuKIT_IP}/`
* Back-office (admin interface): `http://{MyPuMuKIT_IP}/admin`
