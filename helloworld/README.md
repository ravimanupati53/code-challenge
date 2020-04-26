# <!--0_toc.adoc-->

<!-- toc -->

- [Openshift Walk-In Session](#OpenShift-Walk-In-Session)

    + [Introduction to Openshift Container Platform](#Introduction-to-Openshift-Container-Platform)
    + [Setup OpenShift CLI Tools](#Setup-OpenShift-CLI-Tools)
    + [Creating an Appliation Using Web Console](#Creating-an-Application-Using-Web-Console)
    + [Creating an Application Using Command line](#Creating-an-Application-Using-Command-line)
    + [Scale Up and Scale Down the Application Instances](#Scale-Up-Scale-Down-the-Application-Instances)
    + [Rollback Applications](#Rollback-Applications)

<!-- tocstop -->
## INTRODUCTION TO OPENSHIFT CONTAINER PLATFORM: 
-------

   **Openshift Container Platform** is a Platform as a Service (PaaS) that brings Docker and Kubernetes together in providing the 
   API to manage the services and allows creating and managing the containers. Containers are standalone processes that run within their
   own environment which is independent of any operating system helps to develop, deploy, and manage container-based applications. 
   OCP provides self-service platform which is used to create, modify and deploy applications to enable the faster development 
   in business organizations.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/process.png)


**Source-to-Image (S2I)** is a framework that makes it easy to write images that take application source code as an input and produce a new image that runs the assembled application as output. S2I is a toolkit and workflow for building reproducible Docker images from source code. S2I produces ready-to-run images by injecting source code into a Docker container and letting the container prepare that source code for execution. **Source-To-Image (S2I)** is a standalone tool which is very useful when creating builder images. It also happens that S2I is the major strategy used for building applications in OpenShift runtime environments. 

#### This Document walks you through Platform to experience the environment in creating an application from command line and from web console.

# **PREREQUISITES: Setup OpenShift CLI Tools**

***OpenShift Origin*** is a distribution of [Kubernetes](https://kubernetes.io) optimized for continuous application development and multi-tenant deployment.  OpenShift adds developer and operations-centric tools on top of Kubernetes to enable rapid application development, easy deployment and scaling, and long-term lifecycle maintenance for small and large teams. The OCP CLI exposes commands for managing applications, as well as lower-level tools to interact with each component of a system.

**Prerequisites**

* GIT for Windows. 
   
* OpenShift client Tools for Windows. 

***Instructions to Setup OpenShift Client Tools in local machine***

* Please follow the link to setup OpenShift Client Tools in local machine

https://thebank.info53.com/teams/ITInfra/CldEng/Hybrid%20Cloud%20Program/Lists/AWS%20Innovation%20Lab%20Faqs/DispForm.aspx?ID=60&Source=https%3A%2F%2Fthebank%2Einfo53%2Ecom%2Fteams%2FITInfra%2FCldEng%2FHybrid%2520Cloud%2520Program%2FLists%2FAWS%2520Innovation%2520Lab%2520Faqs%2FAllItems%2Easpx&ContentTypeId=0x01008C63473FCC54684596E2159F7ACE346C

* Login to the remote server by using the following command `oc login <host server>`.

 **You can Find the login command from webconsole and click on `Copy Login Command`**
 
 ![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Login%20command.PNG)

 **Paste the Login Command in the command line.**
 
 `oc login https://master.ocpsandbox.info53.com:8443 --token= {{ "Copied from Web Console" }}`
 
--------

****Git Repository Hosting****

To create a new application you need to have your source code hosted in the Git Repository and have it accessible. 

-------
## **LAB 1:Creating New Application using Web Console**

Walk Through Openshift Container Platform

**STEP 1:** Login to OpenShift Environment via Web Console:

   **Open Web Browser and type URL: https://master.ocpsandbox.info53.com:8443**
   
You will find the Request for Approval(Identity provider) page opened, click on `Allow`

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Ping%20Identity.PNG)

**STEP 2:** To Deploy an application in OpenShift, Create a project and click on `Browse Catalog`

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Project.PNG)

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Image%20Deployment.PNG)

**STEP 3:** Find `JBoss Web Server 3.1 Apache Tomcat 8 (no https)` image template in the catalog under `Middleware ---> RunTime & Frameworks Section1`

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/JBoss%20Tomcat%20Web%20Server.PNG)

**STEP 4:** Modify the Configuration section by specifying the Source code GIT repository, Branch and Directory name.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/image%20configuration%20-%20Copy.PNG)

**STEP 5:** You can select to bind the secret to the build or you can add it later 

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Secret%20Binding.PNG)

**STEP 6:** Service is Provisioned, click on `Continue to the Project Overview`

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Project%20creation.PNG)

**STEP 7:** If the build fails with the `source code repository exists error`, 

    Cloning ".git@sogramihqbhub99.53:ravi-manupati/Traning/git" ...
    error: ssh: Could not resolve hostname sogramihqbhub99.53: Name or service not known
    fatal: Could not read from remote repository.

    Please make sure you have the correct access rights
    and the repository exists.
    
Please make sure you added `public key(ssh-keygen-->.ssh/id_rsa.pub)` in your git repo `click on settings` `select SSH and GPG keys` `Add SSH key`.
If you dont have a public key generated, Please execute this command `ssh-keygen` and `cat .ssh/id_rsa.pub` copy the encrypted key and paste the key in Git Repo.

you need to create a new secret by adding the private key("Execute this command `cat .ssh/id_rsa` and copy the encrypted key") to the build config file. To add a new secret follow the steps mentioned below.

- Go to `Builds`
- Click on `Actions`
- Click on `Edit`
- Go to `Advanced Options` under `Source Configuration` Section 
- Click on `Create New Secret`
- Click on `Create`
- CLick on `Save` 

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Priviate%20Key.PNG)

**STEP 8:** Click on `Start Build` to start the New Build.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/start%20build.PNG)

**STEP 9:** You can find the build was success and the image is pushed to internal docker registry.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/build%20success.PNG)

**STEP 10:** You can see the pod is up and running successfully.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/pod%20creation.PNG)

**STEP 11:** Click on `Route` you can see the output on the web browser.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/output.PNG)

-------
-------

## **LAB 2: Create an Application using Command line**

**STEP 1:**Login to OpenShift Environment via Command line:

       
**STEP 2:** Upon the project creation, Openshift will automatically switch to the newly created project/namespace. If you wish to view the list of projects, run the following command:


    $ oc get projects


If you have more than one project, you can switch to a different one by issuing `oc project <project name>`. Although you don’t want to do it now.

**STEP 3:** To run the build successfully we need the secret created prior that can be used in future step. To create the secret execute the following command

    oc create secret generic <Secret Name> --from-file=ssh-privatekey=.ssh/id_rsa --type=kubernetes.io/ssh-auth
    oc create secret generic training --from-file=ssh-privatekey=.ssh/id_rsa --type=kubernetes.io/ssh-auth

**STEP 4:** Create a new-app by issuing the following command `oc new-app` along with the image template available in the catalog and repository URL.

    oc new-app --template=<Template name> -p APPLICATION_NAME=<unique application name> -p SOURCE_REPOSITORY_URL=<Git repo URL> -p SOURCE_REPOSITORY_REF=<branch name> -p CONTEXT_DIR=<directory-name or '' default> --source-secret=<Secret-name> -n <project-name>

    oc new-app --template=jws31-tomcat8-basic-s2i -p APPLICATION_NAME=jbosstomcat -p SOURCE_REPOSITORY_URL=git@sogramihqghub99.53.com:ravi-manupati/Training.git -p SOURCE_REPOSITORY_REF=master -p CONTEXT_DIR='' --source-secret=training -n training


and the output something looks like:

        $ oc new-app --template=jws31-tomcat8-basic-s2i -p APPLICATION_NAME=jbosstomcat -p SOURCE_REPOSITORY_URL=git@sogramihqghub99.53.com:ravi-manupati/Training.git -p SOURCE_REPOSITORY_REF=master -p CONTEXT_DIR='' --source-secret=training -n training
    --> Deploying template "openshift/jws31-tomcat8-basic-s2i" to project training

         JBoss Web Server 3.1 Apache Tomcat 8 (no https)
         ---------
         An example JBoss Web Server application. For more information about using this template, see https://github.com/jboss-openshift/application-templates.

         A new JWS application for Apache Tomcat 8 has been created in your project. The username/password for administering your JWS is mFAP5j1b/Gr3gyaCv.

         * With parameters:
            * Application Name=jbosstomcat
            * Custom http Route Hostname=
            * Git Repository URL=git@github.info53.com:Fifth-Third/cloud-openshift-tomcat-hello-world.git
            * Git Reference=master
            * Context Directory=
            * JWS Admin Username=mFAP5j1b # generated
            * JWS Admin Password=Gr3gyaCv # generated
            * Github Webhook Secret=NHxs0URL # generated
            * Generic Webhook Secret=71R6ya4j # generated
            * ImageStream Namespace=openshift
            * Maven mirror URL=
            * ARTIFACT_DIR=

    --> Creating resources ...
        service "jbosstomcat" created
        route "jbosstomcat" created
        imagestream "jbosstomcat" created
        buildconfig "jbosstomcat" created
        deploymentconfig "jbosstomcat" created
    --> Success
        Access your application via route 'jbosstomcat-training.apps.ocpsandbox.info53.com'
        Build scheduled, use 'oc logs -f bc/jbosstomcat' to track its progress.
        Run 'oc status' to view your app.

**STEP 5:** The Build is scheduled and to track the build process run this command `oc logs -f bc/jbosstomcat`

    $ oc logs -f bc/jbosstomcat
        Cloning "git@sogramihqghub99.53.com:ravi-manupati/Training.git" ...
        Commit:	2d9071d63c5400b598c474a389163096f536b452 (Update index.jsp)
        Author:	Manupati, Ravi <Ravi.Manupati@53.com>
        Date:	Thu Aug 23 05:32:50 2018 -0400
    Using HTTP proxy http://redacted@216.131.54.74:8080  and HTTPS proxy http://redacted@216.131.54.74:8080  for script download
    Pulling image "registry.access.redhat.com/jboss-webserver-3/webserver31-tomcat8-openshift@sha256:5315886dd2e5185307d71f3a9d62227f593e4403e621fc8ccfa4b0bf02d1db22" ...
    Found pom.xml... attempting to build with 'mvn -e -Popenshift -DskipTests -Dcom.redhat.xpaas.repo.redhatga package --batch-mode -Djava.net.preferIPv4Stack=true '
    Using MAVEN_OPTS '-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+UseParallelOldGC -XX:MinHeapFreeRatio=10 -XX:MaxHeapFreeRatio=20 -XX:GCTimeRatio=4 -XX:AdaptiveSizePolicyWeight=90 -XX:MaxMetaspaceSize=100m -XX:+ExitOnOutOfMemoryError'
    Using Apache Maven 3.5.0 (Red Hat 3.5.0-4.3)
    Maven home: /opt/rh/rh-maven35/root/usr/share/maven
    Java version: 1.8.0_181, vendor: Oracle Corporation
    Java home: /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.181-3.b13.el7_5.x86_64/jre
    Default locale: en_US, platform encoding: ANSI_X3.4-1968
    OS name: "linux", version: "3.10.0-862.9.1.el7.x86_64", arch: "amd64", family: "unix"
    [INFO] Error stacktraces are turned on.
    [INFO] Scanning for projects...
    [INFO]
    [INFO] ------------------------------------------------------------------------
    [INFO] Building getting-started-tomcat Maven Webapp 1.0-SNAPSHOT
    [INFO] ------------------------------------------------------------------------
    [INFO] Downloading: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.pom
    [INFO] Downloaded: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-resources-plugin/2.6/maven-resources-plugin-2.6.pom (8.1 kB at 11 kB/s)
    [INFO] Downloading: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-plugins/23/maven-plugins-23.pom
    [INFO] Downloaded: https://repo1.maven.org/maven2/org/apache/maven/plugins/maven-plugins/23/maven-plugins-23.pom (9.2 kB at 103 kB/s)
    [INFO] Downloading: https://repo1.maven.org/maven2/org/apache/maven/maven-parent/22/maven-parent-22.pom
    [INFO] Downloaded: https://repo1.maven.org/maven2/org/apache/maven/maven-parent/22/maven-parent-22.pom (30 kB at 234 kB/s)
    [INFO] Downloading: https://repo1.maven.org/maven2/org/apache/apache/11/apache-11.pom
    [INFO] Packaging webapp
    [INFO] Assembling webapp [getting-started-tomcat] in [/tmp/src/target/getting-started-tomcat]
    [INFO] Processing war project
    [INFO] Copying webapp resources [/tmp/src/src/main/webapp]
    [INFO] Webapp assembled in [29 msecs]
    [INFO] Building war: /tmp/src/target/ROOT.war
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 24.219 s
    [INFO] Finished at: 2018-08-21T15:09:02Z
    [INFO] Final Memory: 12M/56M
    [INFO] ------------------------------------------------------------------------
    [WARNING] The requested profile "openshift" could not be activated because it does not exist.
    Copying all war artifacts from /tmp/src/target directory into /opt/webserver/webapps for later deployment...
    '/tmp/src/target/ROOT.war' -> '/opt/webserver/webapps/ROOT.war'
    Copying all war artifacts from /tmp/src/deployments directory into /opt/webserver/webapps for later deployment...

    Pushing image docker-registry.default.svc:5000/training/jbosstomcat:latest ...
    Pushed 6/7 layers, 89% complete
    Pushed 7/7 layers, 100% complete
    Push successful

### you can keep track of build configuration Json file by the following command

        $ oc get bc/jbosstomcat -o json
        {
            "apiVersion": "build.openshift.io/v1",
            "kind": "BuildConfig",
            "metadata": {
                "annotations": {
                    "openshift.io/generated-by": "OpenShiftNewApp"
                },
                "creationTimestamp": "2018-08-21T15:08:25Z",
                "labels": {
                    "app": "jws31-tomcat8-basic-s2i",
                    "application": "jbosstomcat",
                    "template": "jws31-tomcat8-basic-s2i",
                    "xpaas": "1.4.14"
                },
                "name": "jbosstomcat",
                "namespace": "training",
                "resourceVersion": "4002925",
                "selfLink": "/apis/build.openshift.io/v1/namespaces/training/buildconfigs/jbosstomcat",
                "uid": "0d3dcb01-a554-11e8-b118-005056b2c717"
            },
            "spec": {
                "failedBuildsHistoryLimit": 5,
                "nodeSelector": null,
                "output": {
                    "to": {
                        "kind": "ImageStreamTag",
                        "name": "jbosstomcat:latest"
                    }
                },
                "postCommit": {},
                "resources": {},
                "runPolicy": "Serial",
                "source": {
                    "git": {
                        "ref": "master",
                        "uri": "git@github.info53.com:Fifth-Third/cloud-openshift-tomcat-hello-world.git"
                    },
                    "sourceSecret": {
                        "name": "training"
                    },
                    "type": "Git"
                },
                "strategy": {
                    "sourceStrategy": {
                        "env": [
                            {
                                "name": "MAVEN_MIRROR_URL"
                            },
                            {
                                "name": "ARTIFACT_DIR"
                            }
                        ],
                        "forcePull": true,
                        "from": {
                            "kind": "ImageStreamTag",
                            "name": "jboss-webserver31-tomcat8-openshift:1.2",
                            "namespace": "openshift"
                        }
                    },
                    "type": "Source"
                },
                "successfulBuildsHistoryLimit": 5,
                "triggers": [
                    {
                        "github": {
                            "secret": "NHxs0URL"
                        },
                        "type": "GitHub"
                    },
                    {
                        "generic": {
                            "secret": "71R6ya4j"
                        },
                        "type": "Generic"
                    },
                    {
                        "imageChange": {
                            "lastTriggeredImageID": "registry.access.redhat.com/jboss-webserver-3/webserver31-tomcat8-openshift@sha256:5315886dd2e5185307d71f3a9d62227f593e4403e621fc8ccfa4b0bf02d1db22"
                        },
                        "type": "ImageChange"
                    },
                    {
                        "type": "ConfigChange"
                    }
                ]
            },
            "status": {
                "lastVersion": 1
            }
        }


**STEP 6:** You can check the status of the application

    $ oc status
    In project Training (training) on server https://master.ocpsandbox.info53.com:8443

    http://jbosstomcat-training.apps.ocpsandbox.info53.com (svc/jbosstomcat)
      dc/jbosstomcat deploys istag/jbosstomcat:latest <-
        bc/jbosstomcat source builds git@github.info53.com:Fifth-Third/cloud-openshift-tomcat-hello-world.git#master on openshift/jboss-webserver31-tomcat8-openshift:1.2
        deployment #1 deployed 4 minutes ago - 1 pod

**STEP 7:** To return a list of objects for the specified object type 

**get**

Return a list of objects for the specified object type. If the optional <object_name> is included in the request, then the list of results is filtered by that value.

    $ oc get <object_type> [<object_name>]
    
    $ oc get all

***$oc get bc***-- Contains a description on how to build a source code and a base image into a new image – the primary changes for delivering changes to your application.

    $ oc get bc
    NAME          TYPE      FROM         LATEST
    jbosstomcat   Source    Git@master   1

***$oc get build***-- Builds create a new image from source code, other images, Docker files, or binary input.

    $ oc get build
    NAME            TYPE      FROM          STATUS     STARTED          DURATION
    jbosstomcat-1   Source    Git@5cd81a4   Complete   11 minutes ago   44s
    
***$ oc get is***-- An image stream groups sets of related images under tags – analogous to a branch in a source code repository.

    $ oc get is
    NAME          DOCKER REPO                                             TAGS      UPDATED
    jbosstomcat   docker-registry.default.svc:5000/training/jbosstomcat   latest    10 minutes ago
    
***$ oc get dc***-- Defines the template for a pod and manages deploying new images or configuration changes whenever those change.

    $ oc get dc
    NAME          REVISION   DESIRED   CURRENT   TRIGGERED BY
    jbosstomcat   1          1         1         config,image(jbosstomcat:latest)

***$ oc get route***-- A route is an external DNS entry that is created to a point of a service so that can be accessed outside the cluster.

    $ oc get route
    NAME          HOST/PORT                                         PATH      SERVICES      PORT      TERMINATION   WILDCARD
    jbosstomcat   jbosstomcat-training.apps.ocpsandbox.info53.com             jbosstomcat   <all>     edge          None

***$oc get pod***-- A set of one or more components that are deployed onto a node together and share a unique IP and volumes (persistent storage). Pods also define the security and runtime policy for each container.

    $ oc get pods
    NAME                  READY     STATUS      RESTARTS   AGE
    jbosstomcat-1-build   0/1       Completed   0          11m
    jbosstomcat-1-kn7ss   1/1       Running     0          10m
 
***$ oc get rc***-- A replication controller maintains a specific number of pods based on a template that match a set of labels.

    $ oc get rc
    NAME            DESIRED   CURRENT   READY     AGE
    jbosstomcat-1   1         1         1         10m

***$ oc get svc***-- A name representing a set of pods (or external servers) that are accessed by other pods.

    $ oc get svc
    NAME          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
    jbosstomcat   ClusterIP   172.22.80.242   <none>        8080/TCP   12m


-------
-------

## **LAB 3: Scale Up and Scale Down the Application Instances**

In this exercise we will learn how to scale our application. OpenShift has the capability to scale your application and make sure that many instances are always running. 

**STEP 1:** Switch to the existing Project

    oc project <projectname>
    
    oc project training
    
**STEP 2:** View the deployment config

    $ oc get dc
    NAME      REVISION   DESIRED   CURRENT   TRIGGERED BY
    jws-app   1          1         1         config,image(jws-app:latest)

    
You can find deployment config json file of the appliaton bu using `oc get dc/<dcname> -o json` command and the output looks similar

    $ oc get dc/jws-app -o json
    {
        "apiVersion": "v1",
        "kind": "DeploymentConfig",
        "metadata": {
            "creationTimestamp": "2018-08-21T12:13:50Z",
            "generation": 2,
            "labels": {
                "application": "jws-app",
                "template": "jws31-tomcat8-basic-s2i",
                "xpaas": "1.4.14"
            },
            "name": "jws-app",
            "namespace": "training",
            "ownerReferences": [
                {
                    "apiVersion": "template.openshift.io/v1",
                    "blockOwnerDeletion": true,
                    "kind": "TemplateInstance",
                    "name": "194dbfda-c9c5-4228-b5d5-afcf786e2e98",
                    "uid": "a9c351d8-a53b-11e8-889a-005056b2d886"
                }
            ],
            "resourceVersion": "3963775",
            "selfLink": "/oapi/v1/namespaces/training/deploymentconfigs/jws-app",
            "uid": "a9cb39a5-a53b-11e8-8e37-005056b24b6b"
        },
        "spec": {
            "replicas": 1,
            "selector": {
                "deploymentConfig": "jws-app"
            },
            "strategy": {
                "activeDeadlineSeconds": 21600,
                "recreateParams": {
                    "timeoutSeconds": 600
                },
                "resources": {},
                "type": "Recreate"
            },
            "template": {
                "metadata": {
                    "creationTimestamp": null,
                    "labels": {
                        "application": "jws-app",
                        "deploymentConfig": "jws-app"
                    },
                    "name": "jws-app"
                },
                "spec": {
                    "containers": [
                        {
                            "env": [
                                {
                                    "name": "JWS_ADMIN_USERNAME",
                                    "value": "3MxxKcvN"
                                },
                                {
                                    "name": "JWS_ADMIN_PASSWORD",
                                    "value": "eHINL3Nj"
                                }
                            ],
                            "image": "docker-registry.default.svc:5000/training/jws-app@sha256:61a4d4cff46269f27de371b7bce8fd5aa920bf3432967df18766e8c65a683d24",
                            "imagePullPolicy": "Always",
                            "name": "jws-app",
                            "ports": [
                                {
                                    "containerPort": 8778,
                                    "name": "jolokia",
                                    "protocol": "TCP"
                                },
                                {
                                    "containerPort": 8080,
                                    "name": "http",
                                    "protocol": "TCP"
                                }
                            ],
                            "readinessProbe": {
                                "exec": {
                                    "command": [
                                        "/bin/bash",
                                        "-c",
                                        "curl --noproxy '*' -s -u 3MxxKcvN:eHINL3Nj 'http://localhost:8080/manager/jmxproxy/?get=Catalina%3Atype%3DServer\u0026att=stateName' |grep -iq 'stateName *= *STARTED'"
                                    ]
                                },
                                "failureThreshold": 3,
                                "periodSeconds": 10,
                                "successThreshold": 1,
                                "timeoutSeconds": 1
                            },
                            "resources": {},
                            "terminationMessagePath": "/dev/termination-log",
                            "terminationMessagePolicy": "File"
                        }
                    ],
                    "dnsPolicy": "ClusterFirst",
                    "restartPolicy": "Always",
                    "schedulerName": "default-scheduler",
                    "securityContext": {},
                    "terminationGracePeriodSeconds": 60
                }
            },
            "test": false,
            "triggers": [
                {
                    "imageChangeParams": {
                        "automatic": true,
                        "containerNames": [
                            "jws-app"
                        ],
                        "from": {
                            "kind": "ImageStreamTag",
                            "name": "jws-app:latest",
                            "namespace": "training"
                        },
                        "lastTriggeredImage": "docker-registry.default.svc:5000/training/jws-app@sha256:61a4d4cff46269f27de371b7bce8fd5aa920bf3432967df18766e8c65a683d24"
                    },
                    "type": "ImageChange"
                },
                {
                    "type": "ConfigChange"
                }
            ]
        },
        "status": {
            "availableReplicas": 1,
            "conditions": [
                {
                    "lastTransitionTime": "2018-08-21T12:14:58Z",
                    "lastUpdateTime": "2018-08-21T12:14:58Z",
                    "message": "Deployment config has minimum availability.",
                    "status": "True",
                    "type": "Available"
                },
                {
                    "lastTransitionTime": "2018-08-21T12:14:51Z",
                    "lastUpdateTime": "2018-08-21T12:14:58Z",
                    "message": "replication controller \"jws-app-1\" successfully rolled out",
                    "reason": "NewReplicationControllerAvailable",
                    "status": "True",
                    "type": "Progressing"
                }
            ],
            "details": {
                "causes": [
                    {
                        "type": "ConfigChange"
                    }
                ],
                "message": "config change"
            },
            "latestVersion": 1,
            "observedGeneration": 2,
            "readyReplicas": 1,
            "replicas": 1,
            "unavailableReplicas": 0,
            "updatedReplicas": 1
        }
    }


**Note** that the replicas: is set to 1. This tells OpenShift that when this application deploys, make sure that there is 1 instance.

The replicationController mirrors this configuration initially; the replicationController (or rc) will ensure that there is always the set number of instances always running.

To view the rc for your application first get the current pod running.

    $ oc get pods
    NAME              READY     STATUS       RESTARTS   AGE
    jws-app-1-build   0/1       Init:Error   0          5m
    jws-app-1-mnt8f   1/1       Running      0          4m
    jws-app-2-build   0/1       Completed    0          5m

   
This shows that the build jws-app-1 is running in pod mnt8f. Let us view the rc on this build.

    $ oc get rc/jws-app-1
    NAME        DESIRED   CURRENT   READY     AGE
    jws-app-1   1         1         1         5m

    
Note: You can change the number of replicas in DeploymentConfig or the ReplicationController.

However note that if you change the deploymentConfig it applies to your application. This means, even if you delete the current replication controller, the new one that gets created will be assigned the REPLICAS value based on what is set for DC. If you change it on the Replication Controller, the application will scale up. But if you happen to delete the current replication controller for some reason, you will loose that setting.

**STEP 3:** Scale Application

To scale your application we will edit the deploymentConfig to 3.

Open your browser to the Overview page and note you only have one instance running.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/pod%20creation.PNG)
    
Now scale your application using the oc scale command (remembering to specify the dc)

    $ oc scale --replicas=3 dc/jws-app
    deploymentconfig "jws-app" scaled

If you look at the web console and you will see that there are 3 instances running now 
![alt text](https://sogramihqghub99.53.com/ravi-manupati/Training/blob/master/images/Pod%20Scale%20to%203.PNG)

**Note:** You can also scale up and down from the web console by going to the project overview page and clicking twice on image ![alt text](https://sogramihqghub99.53.com/ravi-manupati/Training/blob/master/images/scaleup.PNG) right next to the pod count circle to add 2 more pods.

On the command line, see how many pods you are running now:

    $ oc get pods
    NAME              READY     STATUS       RESTARTS   AGE
    jws-app-1-4w8zc   0/1       Running      0          7s
    jws-app-1-build   0/1       Init:Error   0          6m
    jws-app-1-mnt8f   1/1       Running      0          5m
    jws-app-1-sf2kv   0/1       Running      0          7s
    jws-app-2-build   0/1       Completed    0          6m

You now have 3 instances of jws-app-1 running (each with a different pod-id). If you check the rc of the jws-app-1 build you will see that it has been updated by the dc.

    $ oc get rc/jws-app-1
    NAME        DESIRED   CURRENT   READY     AGE
    jws-app-1   3         3         3         6m


**STEP 4:** Idling the application

Run the following command to find the available endpoints

    $ oc get endpoints
    NAME      ENDPOINTS                                                AGE
    jws-app   172.31.12.69:8080,172.31.14.138:8080,172.31.17.31:8080   7m

Note that the name of the endpoints is jws-app and there are many ips addresses for the three pods.

Run the `oc idle endpoints/jws-app` command to idle the application  

    $ oc idle endpoints/jws-app
    The service "training/jws-app" has been marked as idled
    The service will unidle DeploymentConfig "training/jws-app" to 3 replicas once it receives traffic
    DeploymentConfig "training/jws-app" has been idled

Go back to the webconsole. You will notice that the pods show up as idled.  

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/pod%20idle.PNG)

At this point the application is idled, the pods are not running and no resources are being used by the application. This doesn’t mean that the application is deleted. The current state is just saved.. that’s all.

**STEP 6:** Reactivate your application Now click on the application route URL or access the application via curl.

Note that it takes a little while for the application to respond. This is because pods are spinning up again. You can notice that in the web console.

In a little while the output comes up and your application would be up with 3 pods.

So, as soon as the user accesses the application, it comes up!!!

**STEP 7:** Scaling Down

Scaling down is the same procedure as scaling up. Use the `oc scale` command on the time application dc setting.

    $ oc scale --replicas=1 dc/jws-app
    deploymentconfig "jws-app" scaled

    
![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/pod%20creation.PNG)

Alternately, you can go to project overview page and click on image twice ![alt text](https://sogramihqghub99.53.com/ravi-manupati/Training/blob/master/images/scaledown.PNG) to remove 2 running pods.

---------
---------

## **Lab 4: Rollback Applications**

In this lab we will see how we can rollback an application in OpenShift quickly without switching to an older version of the source code in SCM.

**Rollback Appliction defines Revert an application back to a previous deployment**

**STEP 1:** Create an application

        $ oc new-app --template=jws31-tomcat8-basic-s2i -p APPLICATION_NAME=jbosstomcat -p SOURCE_REPOSITORY_URL=git@sogramihqghub99.53.com:ravi-manupati/Training.git -p SOURCE_REPOSITORY_REF=master -p CONTEXT_DIR='' --source-secret=training -n training
    --> Deploying template "openshift/jws31-tomcat8-basic-s2i" to project training

         JBoss Web Server 3.1 Apache Tomcat 8 (no https)
         ---------
         An example JBoss Web Server application. For more information about using this template, see https://github.com/jboss-openshift/application-templates.

         A new JWS application for Apache Tomcat 8 has been created in your project. The username/password for administering your JWS is skapDcsB/B7gc8QNp.

         * With parameters:
            * Application Name=jbosstomcat
            * Custom http Route Hostname=
            * Git Repository URL=git@sogramihqghub99.53.com:ravi-manupati/Training.git
            * Git Reference=master
            * Context Directory=
            * JWS Admin Username=skapDcsB # generated
            * JWS Admin Password=B7gc8QNp # generated
            * Github Webhook Secret=cu0e7Ker # generated
            * Generic Webhook Secret=naqtLsak # generated
            * ImageStream Namespace=openshift
            * Maven mirror URL=
            * ARTIFACT_DIR=

    --> Creating resources ...
        service "jbosstomcat" created
        route "jbosstomcat" created
        imagestream "jbosstomcat" created
        buildconfig "jbosstomcat" created
        deploymentconfig "jbosstomcat" created
    --> Success
        Access your application via route 'jbosstomcat-training.apps.ocpsandbox.info53.com'
        Build scheduled, use 'oc logs -f bc/jbosstomcat' to track its progress.
        Run 'oc status' to view your app.


**STEP 2:** Check Application Health Status
   
    $ oc get pods
    NAME                  READY     STATUS      RESTARTS   AGE
    jbosstomcat-1-build   0/1       Completed   0          14m
    jbosstomcat-1-sl8bs   1/1       Running     0          13m

    $ oc get dc
    NAME          REVISION   DESIRED   CURRENT   TRIGGERED BY
    jbosstomcat   1          1         1         config,image(jbosstomcat:latest)

**STEP 3:** Run the Application using web browser and the output looks similar 

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/output.PNG)


**STEP 4:** Edit the `index.jsp` file which is located at " https://sogramihqghub99.53.com/ravi-manupati/Training/blob/master/src/main/webapp/index.jsp", commit changes and `start build` 

You can start the new build under `build section` click on latest build app name and select `Start Build`.

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Build%20process.PNG)

If you run the application after new build the ouput looks similar to this:

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Rollback%20output.PNG)

    $ oc get builds
    NAME            TYPE      FROM          STATUS     STARTED          DURATION
    jbosstomcat-1   Source    Git@bf58f6f   Complete   18 minutes ago   41s
    jbosstomcat-2   Source    Git@2d9071d   Complete   2 minutes ago    44s

 
After build you can observe the changes in `deployment config`

    $ oc get dc
    NAME          REVISION   DESIRED   CURRENT   TRIGGERED BY
    jbosstomcat   2          1         1         config,image(jbosstomcat:latest)

**STEP 5:** Rollback the Application

    $ oc rollback jbosstomcat --to-version=1
    #3 rolled back to jbosstomcat-1
    Warning: the following images triggers were disabled: jbosstomcat:latest
      You can re-enable them with: oc set triggers dc/jbosstomcat --auto

After Rollback the Application the changes can be seen in `deployment config` of the application

    $ oc get dc
    NAME          REVISION   DESIRED   CURRENT   TRIGGERED BY
    jbosstomcat   3          1         1         config


So OpenShift has rolled back the application to version 1 and created a new build configuration.

Reloading the application now displays:

It runs the new deployment after rollback the application.
![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/Rollback%20process.PNG)

The output looks similar like this 

![alt text](https://github.info53.com/Fifth-Third/cloud-openshift-training/blob/master/images/output.PNG)




## Note: For more information on OpenShift you can refer to FAQ document in the link mentioned below.

### You can find under Category: Platform as a Service(PaaS)

https://thebank.info53.com/teams/ITInfra/CldEng/Hybrid%20Cloud%20Program/_layouts/15/start.aspx#/Lists/AWS%20Innovation%20Lab%20Faqs/AllItems.aspx
