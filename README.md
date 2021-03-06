# IBM Application Security on Cloud Bamboo Plug-in

Easily integrate security scanning with the [IBM Application Security on Cloud](https://appscan.ibmcloud.com) service into your builds running on Atlassian Bamboo.

# Prerequisites

- An account on the [IBM Application Security on Cloud](https://appscan.ibmcloud.com) service. You'll also need to [create an application](http://www.ibm.com/support/knowledgecenter/SSYJJF_1.0.0/ApplicationSecurityonCloud/ent_create_application.html) on the service and copy down its numeric ID in the browser URL. This ID will be required later on when configuring the SAST scan task.
- The plug-in has been tested to run on Bamboo server version 5.13.2 or later.
- To build the plug-in, you will need to install the [Atlassian plug-in SDK](https://developer.atlassian.com/docs/getting-started).
- You will need to setup the Static Analyzer Client Utility on your Bamboo server (to initiate scans on local agents), or on remote agent machines. For more information on obtaining the client utility, see the docs [here](http://www.ibm.com/support/knowledgecenter/SSYJJF_1.0.0/ApplicationSecurityonCloud/src_scanning.html).

# Building the Plug-in

- Navigate to the plug-in's root folder and issue the `atlas-package` command. The built plug-in JAR will be in the target folder.

# Installation and Configuration

1. Install the plug-in via the Bamboo's administration dashboard. After installing the plug-in, it will appear in the list of user installed add-ons.

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/install1.png)

2. Via Bamboo's administration dashboard, add the SA Client capability to your server (for local agents), or to your remote agents. Specify the path to the Static Analyzer Client Utility.

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/install2.png)

3. Enter your IBM Application Security on Cloud account username and password in Bamboo's shared credentials page.

# Adding the SAST Scan Task to your Build Plan

1. Add the SAST scan task to your build plan after your artifacts have been built. The SAST scan task will generate an intermediate representation of your artifacts and submit it to the cloud service for scanning.

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/task1.png)

2. Enter information for the SAST scan task:

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/task2.png)

   - Select the client utility to use from the dropdown
   
   - Select the credentials to use to login to the cloud service
   
   - Enter the ID of the application to associate your scan with
   
   - Optionally, specify the criteria for whether or not to fail the build when security findings are found

# Scan Results after a Build

1. The SAST scan task publishes two artifacts:

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/result1.png)

   - IRX - this is the intermediate representation of your artifacts that is uploaded to the cloud service for scanning.
   
   - Scan Results - HTML report of the security findings that are found.

2. Messages about the outcome of the scan will also be emitted to the build log:

   ![](https://github.com/AppSecDev/asoc-bamboo-plugin/blob/master/images/result2.png)

# License

All files found in this project are licensed under the [Apache License 2.0](LICENSE).
