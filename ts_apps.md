---

copyright:

  years: 2015, 2018

lastupdated: "2018-07-05"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Troubleshooting for managing apps
{: #managingapps}

General problems with managing apps might include apps that can't be updated, or double-byte characters that aren't displayed. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## You have unsaved changes
{: #ts_unsaved_changes}

When you click items on the app details page, you might be unable to take any actions and might be prompted to save changes before you can proceed.

When you try to check your app or services on the app details page, you keep getting the following error message:
{: tsSymptoms}

`You have unsaved changes in page app_name. Save or cancel the changes.`

When you scroll your mouse over the **INSTANCES** or **MEMORY QUOTA** field on the runtime pane, the values change. This behavior is by design; however, the error message prompts you to save the memory or instance settings before you go to another page.
{: tsCauses}

Close the message window, and then click **RESET** in your runtime pane.
{: tsResolve}

## Automatic failover between {{site.data.keyword.Bluemix_notm}} regions isn't available
{: #ts_failover}

You can't use automatic failover between {{site.data.keyword.Bluemix_notm}} regions. However, you can use a DNS provider that supports failover among many IP addresses as a workaround.

When an {{site.data.keyword.Bluemix_notm}} region becomes unavailable, the apps that are running in that region are also unavailable, even if the same apps are running in another {{site.data.keyword.Bluemix_notm}} region.
{: tsSymptoms}

{{site.data.keyword.Bluemix_notm}} doesn't yet provide automatic failover from one region to another.
{: tsCauses}

You can use a DNS provider that supports intelligent failover among many ID addresses, and manually configure your DNS settings to enable the automatic failover between {{site.data.keyword.Bluemix_notm}} regions. DNS providers with this feature include NSONE, Akamai, Dyn.
{: tsResolve}

When you configure your DNS settings, you must specify the public IP addresses of the {{site.data.keyword.Bluemix_notm}} regions that your apps are running in. To get the public IP address of an {{site.data.keyword.Bluemix_notm}} region, use the `nslookup` command. For example, you can type the following command in a command line window.

```
nslookup stage1.mybluemix.net
```

## Can't switch apps into debug mode
{: #ts_debug}

You can't enable the debug mode if the Java virtual machine (JVM) version is 8 or earlier.

After you select **Enable application debug**, the tools try to switch the app into the debug mode. Then, the Eclipse workbench begins a debug session. When the tools successfully enable debug mode, the web application status displays `Updating mode`, `Developing`, and `Debugging`.
{: tsSymptoms}

However, when the tools fail to enable the debug mode, the web application status displays `Updating mode` and `Developing` only, and doesn't display `Debugging`. The tools might also display the following error message in the Console view:

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```

The following Java virtual machine (JVM) versions can't establish a debug session: IBM JVM 7, IBM JVM 8, and previous versions of Oracle JVM 8.
{: tsCauses}

If your workbench JVM is one of these versions, you might have issues when you create a debug session. Your workbench JVM version is typically the system JVM of your local computer. Your system JVM isn't the same as the JVM of your running {{site.data.keyword.Bluemix_notm}} Java&trade; application. The {{site.data.keyword.Bluemix_notm}} Java application almost always runs on IBM JVM, and sometimes runs on OpenJDK JVM.

To check the version of Java that {{site.data.keyword.eclipsetoolsfull}} runs, complete the following steps:
{: tsResolve}

  1. In IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, select **Help** > **About Eclipse** > **Installation Details** > **Configuration**.
  2. Find the `eclipse.vm` property from the list. The following line is an example of an `eclipse.vm` property:

	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. At the command line, enter `java -version` from the `bin` directory of your Java installation. Your IBM JVM version information is displayed.

If your workbench JVM is IBM JVM 7 or 8, or a previous version of Oracle JVM 8, complete the following steps to switch to Oracle JVM 8:

  1. Download and then install Oracle JVM 8, see [Java SE Downloads ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} for details.
  2. Restart Eclipse.
  3. Check whether the `eclipse.vm` property points to your new installation of Oracle JVM 8.


## Can't reuse names of deleted apps
{: #ts_reuse_appname}

After you delete an app, you can reuse the app name only after you delete the app route.

When you try to reuse the app name, you receive the following message:
{: tsSymptoms}

`The name is already used by another app.`

When an app is deleted, its route, which is the URL for the app, isn't automatically deleted and it's not available for reuse. You must go to the space where the app was created to delete the route so that it can be reused.
{: tsCauses}

Complete the following steps to delete the unused route:
{: tsResolve}

  1. Check whether the route belongs to the current space by entering the following command:

    ```
    cf routes
    ```

  2. If the route doesn't belong to the current space, switch to the space or org that it belongs to by entering the following command:

    ```
    cf target -o org_name -s space_name
    ```

  3. Delete the app route by entering the following command:

    ```
    cf delete-route domain_name -n host_name
    ```

  For example:

  ```
  cf delete-route mybluemix.net -n app001
  ```

## Can't retrieve spaces in the org
{: #ts_retrieve_space}

You can't create an app or a service if your current organization doesn't have a space that is associated with it.

When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms}

`BXNUI0515E: The spaces in the org weren't retrieved. Either a network connection problem occurred, or your current organization does not have a space associated with it.`

This error often occurs the first time that you try to create an app or a service from the catalog when a space isn't created yet.
{: tsCauses}

Ensure that you created a space in your current organization. To create a space, use one of the following methods:
{: tsResolve}

* From the menu bar, click **Manage > Account > Organizations**. Select the organization that you want to create the space in, and click **Create a Space**.
* In the `cf` command line interface, type `cf create-space <space_name> -o <organization_name>`.

Try again. If this message occurs again, go to the [{{site.data.keyword.Bluemix_notm}} status ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window} page to check whether a service or component has an issue.

## Can't perform requested actions
{: #ts_authority}

You can't complete actions without appropriate access authority.

When you try to perform actions for a service instance or an app instance, you can't complete the requested actions and see one of the following error messages:
{: tsSymptoms}

`BXNUI0514E: You are not a developer for any of the spaces in the <orgName> organization.`

`Server error, status code: 403, error code: 10003, message: You are not authorized to perform the requested action.`

You don't have the appropriate level of authority to perform the actions.
{: tsCauses}

To get the appropriate authority level, use one of the following methods.
{: tsResolve}

* Select another organization and space for which you have the developer role.
* Ask the org manager to change your role to developer or to create a space and then assign you a developer role. See [Managing organizations and spaces](/docs/admin/orgs_spaces.html) for details.

## Can't access {{site.data.keyword.Bluemix_notm}} services because of authorization errors
{: #ts_vcap}

Authorization errors might occur when your app accesses an {{site.data.keyword.Bluemix_notm}} service, if the service credentials are hardcoded in your app.

After you configure your app to communicate with an {{site.data.keyword.Bluemix_notm}} service, you deploy the app to {{site.data.keyword.Bluemix_notm}}. However, you can't use the app to access the {{site.data.keyword.Bluemix_notm}} service and receive an authorization error.
{: tsSymptoms}

The hardcoded credentials in the app might not be correct. Every time that the service is re-created, the credentials to access it change.
{: tsCauses}

Instead of hardcoding the credentials in your app, use connection parameters from the VCAP_SERVICES environment variable. The methods to use connection parameters from the VCAP_SERVICES environment variable vary depending on program languages. For example, for Node.js apps, you can use the following command:
{: tsResolve}

```
process.env.VCAP_SERVICES
```
For more information about the commands that you can use in other program languages, see [Java ![External link icon](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} and [Ruby ![External link icon](../icons/launch-glyph.svg "External link icon")](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}.


## Can't deploy apps by using IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

When an unsupported facet is applied to your Eclipse project, you might not be able to deploy your apps to {{site.data.keyword.Bluemix_notm}} by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.

You can successfully deploy your app to {{site.data.keyword.Bluemix_notm}} by using the Cloud Foundry CLI. However, you can't deploy the app to {{site.data.keyword.Bluemix_notm}} by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, and you see the error message: `Project facet <facet_name> is not supported.` For example:
{: tsSymptoms}
`Project facet Cloud Foundry Standalone Application version 1.0 is not supported.`

The IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} map projects to {{site.data.keyword.Bluemix_notm}} runtimes by project facets. Facets define the requirements for Java EE projects in Eclipse, and are used as part of the runtime configuration so that different runtimes are associated with different projects. If the facet that is applied to the project isn't supported by the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, you can't deploy your app by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

You must remove the facet from the Eclipse project so that you can deploy your app by using the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve}

To remove the facet, in the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, click **Project > Properties > Project Facets** for the project. Then, clear the check box for the unsupported facet.

## 502 Bad Gateway errors are received
{: #ts_502_error}

If you receive 502 Bad Gateway errors when you interact with apps on {{site.data.keyword.Bluemix_notm}}, check the {{site.data.keyword.Bluemix_notm}} status page, and then take appropriate actions.

You receive error messages that start with 502 Bad Gateway. For example, you might see `502 Bad Gateway: Registered endpoint failed to handle the request.`
{: tsSymptoms}

A Bad Gateway error usually happens when you go to a website that uses a proxy server to store and relay the data from the main server that hosts the site. The main server and the proxy server might not connect properly. Then, you see the HTTP status code 502 in your browser window. This status code indicates that the site's main server didn't receive the HTTP implementation that it expected from the proxy server.
{: tsCauses}

Other less common causes of a Bad Gateway error are internet service provider (ISP) dropouts, bad firewall configurations, and browser cache errors.

If you suspect that an {{site.data.keyword.Bluemix_notm}} service is down, first check the [{{site.data.keyword.Bluemix_notm}} status ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixstatus){: new_window} page. A workaround might be to use the service in another {{site.data.keyword.Bluemix_notm}} region. Detailed information is available in [Using services in another region ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/reqnsi.html#cross_region_service){: new_window}. If the service status is normal, try the following steps to solve the problem:
{: tsResolve}

  * Retry the action:
    * Reload the page by pressing F5 on your keyboard, or by clicking **Refresh**. If this step doesn't work, clear your browser's cache and cookies, and then reload again.
    * Use a different browser.
    * Restart your router, your modem, and your computer. Rebooting these devices can clear up various errors that lead to the error 502.
  * Wait and try again later. Temporary problems might occur with your internet service provider or the {{site.data.keyword.Bluemix_notm}} services. You can wait until the temporary problems are solved.
  * If the problem still exists, contact {{site.data.keyword.Bluemix_notm}} support. See [Contacting {{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/support/index.html#contacting-bluemix-support){: new_window} for more information.

## Disk quota is exceeded
{: #ts_disk_quota}

If you run out of disk space, you can manually modify the disk quota to get more disk space.

When you run out of disk space, you might see a message that states that the disk quota is exceeded. To resolve the problem, you might have tried scaling up your app instance to get more disk space. For example, you might scale from 256 MB to 1256 MB by changing the memory quota on the app details page. However, because the disk quota remained the same, you did not get more disk space.
{: tsSymptoms}

The default disk quota that is allocated for an app is 1 GB. If you need more disk space, you must manually specify the disk quota.
{: tsCauses}

Use one of the following methods to specify your disk quota. The maximum disk quota that you can specify is 2 GB. If 2 GB is still not enough, try an external service such as [Object Store](/docs/services/ObjectStorage/index.html).
{: tsResolve}

  * In the manifest.yml file, add the following item:
    ```
	disk_quota: <disk_quota>
	```
  * Use the **-k** option with the `cf push` command when you push your app to {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push appname -p app_path -k <disk_quota>
	```

## Android apps can't receive {{site.data.keyword.mobilepushshort}}
{: #ts_push}

Android apps in certain regions where Google isn't accessible can't receive notifications that you send out through the IBM {{site.data.keyword.mobilepushshort}} service. In this case, a workaround is to use third-party services.

You bind a {{site.data.keyword.mobilepushshort}} service for your {{site.data.keyword.Bluemix_notm}} app and send a message to the registered devices. However, apps that are developed on Android can't receive your notifications in certain regions.
{: tsSymptoms}

IBM {{site.data.keyword.mobilepushshort}} service uses the Google Cloud Messaging (GCM) service to dispatch notifications to mobile apps that are developed on Android. To enable the Android apps to receive notifications, Google Cloud Messaging (GCM) service must be accessible by the mobile apps. In regions where the Android apps can't reach the GCM service, the Android apps can't receive {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

As a workaround, use third-party services that don't rely on the GCM service, for example, [Pushy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://pushy.me){: new_window}, [getui ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.getui.com/){: new_window}, and [jpush ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.jpush.cn/){: new_window}.
{: tsResolve}

## Org's services limit is exceeded
{: #ts_servicelimit}

If you are a trial account user, you might be unable to create an app in {{site.data.keyword.Bluemix_notm}} if you exceeded your organization's services limit.

When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms}

`BXNUI2032E: The <service_instances> resource wasn't created. While Cloud Foundry was being contacted to create the resource, an error occurred. Cloud Foundry message: "You have exceeded your organization's services limit."`

This error occurs when you exceed the limit on the number of service instances that you can have for your account. The maximum number of services instances for a trial account is 10.
{: tsCauses}

Delete any services instances that aren't needed, or remove the limit on the number of service instances that you can have.
{: tsResolve}

  * To delete a services instance, you can use the {{site.data.keyword.Bluemix_notm}} console or the command line interface.

    To use the {{site.data.keyword.Bluemix_notm}} console to delete a service instance, complete the following steps:
	  1. In the Services dashboard, click the **Actions** menu for the service that you want to delete.
	  2. Click **Delete Service**. You are prompted to restage the app that the service instance was bound to.

    To use the command line interface to delete a service instance, complete the following steps:
	  3. Unbind the service instance from an app by typing `cf unbind-service <appname> <service_instance_name>`.
	  4. Delete the service instance by typing `cf delete-service <service_instance_name>`.
	  5. After you delete the service instance, you might want to restage your app that the service instance was bound to by typing `cf restage <appname>`.

  * To remove the limit on the number of service instances that you can have, convert your trial account to a pay account. For more information, see [How to change your plan](/docs/pricing/index.html#changing).

## Executable files can't be run on {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

You might be unable to run executables on {{site.data.keyword.Bluemix_notm}} when those executables were developed and built in a different environment.

You can't run executables on {{site.data.keyword.Bluemix_notm}} when those executables were developed and built in a different environment.
{: tsSymptoms}

If the content that you want to push to {{site.data.keyword.Bluemix_notm}} is already an executable, the content was previously built and doesn't need to be built on {{site.data.keyword.Bluemix_notm}}. In this case, no buildpack is required for the executable to be run on {{site.data.keyword.Bluemix_notm}}. You must explicitly indicate to {{site.data.keyword.Bluemix_notm}} that no buildpack is required.
{: tsCauses}

When you push the executable to {{site.data.keyword.Bluemix_notm}}, you must specify a `null-buildpack`, which indicates that no buildpack is required. Specify a `null-buildpack` by using the **-b** option with the `cf push` command:
{: tsResolve}

```
cf push appname -p app_path -c <start_command> -b <null-buildpack>
```
For example:
```
cf push appname -p app_path -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```

## Org's memory limit is exceeded
{: #ts_outofmemory}

If you are a trial account user, you might be unable to deploy an app to {{site.data.keyword.Bluemix_notm}} if you have exceeded the memory limit of your organization. You can either reduce the memory that your apps use or increase the memory quota of your account. The maximum memory quota for a trial account is 2 GB and can be increased only by moving to a paid account.

When you deploy an app to {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms}

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

This error occurs when the amount of memory that is remaining for your organization is less than the amount of memory that is required by the app that you want to deploy. The maximum memory quota for a trial account is 2 GB.
{: tsCauses}

You can either increase the memory quota of your account, or reduce the memory that your apps use.
{: tsResolve}

  * To increase the memory quota of your account, convert your trial account to a pay account. For information about how to convert your trial account to a pay account, see [Pay accounts](/docs/pricing/index.html#pay-accounts).
  * To reduce the memory that your apps use, use either the {{site.data.keyword.Bluemix_notm}} console or the `cf` command line interface.

    If you use the {{site.data.keyword.Bluemix_notm}} console, complete the following steps:

    1. In the Apps Dashboard, select your app. The app details page opens.
    2. In the runtime pane, you can reduce the maximum memory limit or the numbers of app instances, or both, for your app.

    If you use the `cf` command line interface, complete the following steps:

    1. Check how much memory is being used for your apps:

	  ```
	  cf apps
	  ```

	  The `cf apps` command lists all the apps that you deployed in your current space. The status of each app is also displayed.

    2. To reduce the amount of memory that is used by your app, reduce the number of app instances or the maximum memory limit, or both:

	  ```
	  cf push appname -p app_path -i instance_number -m memory_limit
      ```

    3. Restart your app for the changes to take effect.

## Apps aren't automatically restarted
{: #ts_apps_not_auto_restarted}

An app isn't automatically restarted when a service that you bind to the app stops working.

When a service that you bind to an app crashes, problems such as outages, exceptions, and connection failures might occur on the app. {{site.data.keyword.Bluemix_notm}} doesn't automatically restart the app to recover from these problems.
{: tsSymptoms}

This behavior is by design of Cloud Foundry.
{: tsCauses}

You can manually restart the app by typing the following command in the command line interface:
{: tsResolve}

```
cf push appname -p app_path
```

In addition, you can code the app to identify and recover from problems such as outages, exceptions, and connection failures.

## User-defined variables are lost when an app is pushed
{: #ts_varsnotretained}

When you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, the variables that you specified are reset unless you save the variables to the manifest file.

The variables that you specified are lost after you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

The variables that you specified are saved only if you save them to the manifest file.
{: tsCauses}

When you push an app to {{site.data.keyword.Bluemix_notm}} from IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, select the **Save to the manifest file** check box in the Application details page of the Application wizard. Then, the variables that you specified in the wizard are saved to the manifest file for your application. The next time that you open the wizard, the variables are displayed automatically.
{: tsResolve}


## Orgs can't be found on {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

You might not be able to locate your organization on {{site.data.keyword.Bluemix_notm}} when working on a {{site.data.keyword.Bluemix_notm}} region.

You can log in to the {{site.data.keyword.Bluemix_notm}} console successfully, but you can't push apps by using the `cf` command line interface or the Eclipse plug-in.
{: tsSymptoms}

When you try to push an application to {{site.data.keyword.Bluemix_notm}} by using the `cf` command line interface, you see one of the following error messages with the organization name that is specified in the message:

`Error finding org`

`Organization not found`

When you try to push an application to {{site.data.keyword.Bluemix_notm}} by using the Cloud Foundry Eclipse plug-in, you see the following error message:

`cloudspace not found.`

This problem occurs because the API endpoint of the region that you want to work with isn't specified, and the organization you're looking for might be in a different region.
{: tsCauses}

If you are pushing your application to {{site.data.keyword.Bluemix_notm}} by using the `cf` command line interface, enter the `cf api` command and specify the API endpoint of the region. For example, enter the following command to connect to the {{site.data.keyword.Bluemix_notm}} Europe United Kingdom region:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```

If you're pushing your application to {{site.data.keyword.Bluemix_notm}} by using the Eclipse tools, you must first create an {{site.data.keyword.Bluemix_notm}} server and specify the API endpoint of the {{site.data.keyword.Bluemix_notm}} region that your organization was created in. For more information about using the Eclipse tools, see [Deploying apps with IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html).

## App routes can't be created
{: #ts_hostistaken}

When you deploy an app to {{site.data.keyword.Bluemix_notm}}, the route of the app can't be created if the host name that you specified is already being used.

When you deploy an app to {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms}

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`

This problem occurs if the host name that you specified is already being used.
{: tsCauses}

The host name that you specify must be unique within the domain that you are using. To specify a different host name, use one of the following methods:
{: tsResolve}

  * If you deploy your application by using the `manifest.yml` file, specify the host name in the host option.
    ```
    host: host_name
	```
  * If you deploy your application from the command prompt, use the `cf push` command with the **-n** option.
    ```
    cf push appname -p app_path -n host_name
    ```

## WAR apps can't be pushed by using the cf push command
{: #ts_cf_war}

You might not be able to use the `cf push` command to deploy an archived web app to {{site.data.keyword.Bluemix_notm}} if the app location isn't specified correctly.

When you upload a WAR app to {{site.data.keyword.Bluemix_notm}} by using the `cf push` command, you see the following error message:
{: tsSymptoms}
`Staging error: cannot get instances since staging failed.`

This problem might happen if the WAR file isn't specified, or if the path to the WAR file isn't specified.
{: tsCauses}

Use the **-p** option to specify a WAR file or add the path to the WAR file. For example:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
For more information about the `cf push` command, enter `cf push -h`.

## Double-byte characters aren't displayed properly when apps are pushed to {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

Double-byte characters might not be displayed properly if Unicode support isn't configured properly for the servlet or JSP files.

When an application is pushed to the {{site.data.keyword.Bluemix_notm}}, the double-byte characters that are specified within the app aren't displayed properly.
{: tsSymptoms}

The problem might occur if Unicode support isn't configured properly for the servlet or JSP files.
{: tsCauses}

You can use the following code in your servlet or JSP file:
{: tsResolve}

  * In the servlet source file
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * In the JSP
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```

## Node.js apps can't be deployed
{: #ts_nodejs_deploy}

You might experience problems when you update a Node.js app or deploy a Node.js app to {{site.data.keyword.Bluemix_notm}}.

When you update a Node.js app or deploy your Node.js app to {{site.data.keyword.Bluemix_notm}}, you might see one of the following error messages:
{: tsSymptoms}

`An app was not successfully detected by any available buildpack.`

`Instance (index 0) failed to start accepting connections.`

`Cannot get instances since staging failed.`

Possible causes are as follows:
{: tsCauses}

  * The start command isn't specified.
  * Files that are required to deploy a Node.js app are either missing from the app or in a folder other than the root directory.

Use one of the following methods, depending on the cause of the problem:
{: tsResolve}

  * Specify the start command by one of the following methods:
     * Use the `cf` command line interface. For example:
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
    * Use the [package.json ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/jsonfile){: new_window} file. For example:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
    * Use the `manifest.yml` file. For example:
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Ensure that a `package.json` file exists in your Node.js app so that the Node.js buildpack can recognize the app. Ensure that this file is in the root directory of your app.
    The following example shows a simple `package.json` file:
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```

For more tips about Node.js apps, see [Tips for Node.js Applications ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.

## Configuration errors appear in the `server.xml` file after you import an {{site.data.keyword.Bluemix_notm}} Liberty app into Eclipse
{: #ts_eclipse}

If you see configuration errors in the `server.xml` file after you import an {{site.data.keyword.Bluemix_notm}} Liberty app into Eclipse, you might need to remove the `server.xml` file from the project.

After you import an {{site.data.keyword.Bluemix_notm}} Liberty app into Eclipse, you see configuration errors within the `server.xml` file from Eclipse Problems view.
{: tsSymptoms}

Liberty buildpack uses the `server.xml` file to configure the app and generates a `runtime-vars.xml` file when the Liberty app is pushed to {{site.data.keyword.Bluemix_notm}}. When you import the app to Eclipse, the `runtime-vars.xml` file doesn't exist in your local environment.
{: tsCauses}

You can resolve this problem by removing the server.xml file from the project. The buildpack creates the `server.xml` file dynamically when you push the app as a WAR app. For more information, see [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}

## Apps can't be staged by using custom buildpacks
{: #ts_bp_compilation}

You might not be able to deploy an app to {{site.data.keyword.Bluemix_notm}} with a custom buildpack if the scripts in the buildpack aren't executable files.

When you deploy an app to {{site.data.keyword.Bluemix_notm}} with a custom buildpack, you see the error message, `The application failed to stage, so there are no instances to display.`
{: tsSymptoms}

This problem might happen if scripts, such as the detect script, the compile script, and the release script, aren't executable.
{: tsCauses}

You can use the [Git update ![External link icon](../icons/launch-glyph.svg "External link icon")](http://git-scm.com/docs/git-update-index){: new_window} command to change the permission of each script to executable. For example, you can type `git update --chmod=+x script.sh`.
{: tsResolve}

## Can't deploy an app from the Delivery Pipeline in {{site.data.keyword.Bluemix_notm}} Continuous Delivery
 {: #ts_devops_to_bm}

 You might not be able to deploy your app with the {{site.data.keyword.deliverypipeline}} in {{site.data.keyword.contdelivery_short}} if the `manifest.yml` file isn't present in your app.

 When you deploy an app with the {{site.data.keyword.deliverypipeline}} in {{site.data.keyword.contdelivery_short}}, an error message `Unable to detect a supported application type` might display.
 {: tsSymptoms}

 This problem might happen because the pipeline requires a `manifest.yml` file to deploy an app to {{site.data.keyword.Bluemix_notm}}.
 {: tsCauses}

 To resolve this problem, you must create a `manifest.yml` file. For more information about how to create a `manifest.yml` file, see [Application manifest](/docs/manageapps/depapps.html#appmanifest).
 {: tsResolve}

## Meteor apps can't be pushed
{: #ts_meteor}

You might not be able to push a Meteor application to {{site.data.keyword.Bluemix_notm}} if the buildpack isn't specified correctly.

When you deploy a Meteor app to {{site.data.keyword.Bluemix_notm}}, you might see the error message, `The application failed to stage, so there are no instances to display.`
{: tsSymptoms}

This problem occurs because no built-in buildpack is provided for Meteor apps. You must use a custom buildpack.
{: tsCauses}

To use a custom buildpack for Meteor apps, use one of the following methods:
{: tsResolve}

  * If you deploy your app by using the `manifest.yml` file, specify the URL or the name of your custom buildpack by using the buildpack option. For example:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor
  ```
  * If you deploy your application from the command prompt, use the `cf push` command and specify your custom buildpack by using the **-b** option. For example:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
