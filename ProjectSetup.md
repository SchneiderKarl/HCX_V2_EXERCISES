# Project Setup (Mandatory)

## Table of contents 

- [Project Setup (Mandatory)](#project-setup-mandatory)
  - [Table of contents](#table-of-contents)
  - [Access SAP Business Application Studio](#access-sap-business-application-studio)
  - [Create Development Space in BAS](#create-development-space-in-bas)
  - [Customize the default BAS layout](#customize-the-default-bas-layout)
  - [Set Cloud Foundry Endpoint](#set-cloud-foundry-endpoint)
  - [Clone the preconfigured project](#clone-the-preconfigured-project)
  - [Open the project](#open-the-project)
  - [SAP HANA PROJECTS tab](#sap-hana-projects-tab)
  - [Bind SAP HDI Container](#bind-sap-hdi-container)
  - [Bind existing User-Provided Service instance](#bind-existing-user-provided-service-instance)
  - [Deploy the project to HANA Cloud](#deploy-the-project-to-hana-cloud)
  - [Open the SAP HANA Database Explorer](#open-the-sap-hana-database-explorer)

## Access SAP Business Application Studio

> To realize database projects we mainly use the SAP Businness Application Studio (BAS for short).
> It is recommended to use the incognito tab of one of the following three browsers with the latest version. <!-- https://help.sap.com/docs/SAP%20Business%20Application%20Studio/9d1db9835307451daa8c930fbd9ab264/8f46c6e6f86641cc900871c903761fd4.html#availability -->
> - Mozilla Firefox
> - Google Chrome
> - Microsoft Edge

Click [here](https://sharedservices.eu10cf.applicationstudio.cloud.sap/index.html) to open the SAP Business Application Studio.

## Create Development Space in BAS

> Before you can start your project you must first create a Development Space within BAS. 
> > A dev space is a development environment with the tools, capabilities, and resources needed for developing your application.
> > A dev space provides tailored tools and pre-installed runtimes for your business scenario. This simplifies and saves time in setting up your development environment and allows you to efficiently develop, test, build, and run your solution locally or in the cloud.

1) Click on **Create Dev Space** to create a new development environment for your project.

![img](Images/Image_ProjectSetup_Create-Development-Space-in-BAS_01.png)

2) Provide the following inputs to the wizard:
   1) Give your Development Space the Name `HCX`.
   2) Select **SAP HANA Native Application** as application kind. You do not need to add any Additional SAP Extension. 
   3) Click on **Create Dev Space**

![img](Images/Image_ProjectSetup_Create-Development-Space-in-BAS_02.png)

3) Your HCX Dev Space is being created right now.

![img](Images/Image_ProjectSetup_Create-Development-Space-in-BAS_03.png)

4) It takes roughly 1-2 minutes to switch from **STARTING** to **RUNNING**. Now that your space is running click on the Name **HCX** to open it. Your BAS Development Editor opens, in which you create your projects.

![img](Images/Image_ProjectSetup_Create-Development-Space-in-BAS_04.png)

## Customize the default BAS layout

> For a better orientation in SAP BAS we adapt the default layout to our needs.
> <!-- (If possible set default editors for hdi artifacts)-->

1) Click on the **Customize Layout...** Icon on the top right corner. 

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_01.png)

2)  1) Change the **Visibility** of the **Menu Bar** to true by clicking on it. 
    2) Then Close the Customize Layout wizard by clicking the X.

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_02.png)

3) Click on the icon to open the **Explorer**.

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_03.png)

4) Right-click on the **Outline** tab

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_04.png)

5) Deselect the **Outline**

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_05.png)

6) Repeat the process and deselect the **Timeline**

![img](Images/Image_ProjectSetup_Customize-the-default-BAS-layout_06.png)

## Set Cloud Foundry Endpoint

> You will connect your development space in SAP BAS to Cloud Foundry, so we can later deploy the project to the SAP HANA Cloud running on the Cloud Foundry environment.

<!--
### Option A)
1)  1) Click on **View** in the Menu Bar
    2) Then click on **Command Palette...**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_01.png)

2) Type in `cf login` and select the given option.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_02.png)

3) Provide the following inputs to the Cloud Foundry Sign In wizard:
   1) **Cloud Foundry Endpoint**: `https://api.cf.eu10.hana.ondemand.com`
   2) **Username**: `YOUR_EMAIL_ADDRESS`
   3) **Password**: `YOUR_DOMAIN_PASSWORD`
   4) Then click on **Sign in**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_03.png)

4) Select the following options in the Cloud Foundry Target wizard:
   1) **Cloud Foundry Organization**: `SharedServices`
   2) **Cloud Foundry Space**: `HANA Cloud Experience V2`
   3) Then click on **Apply**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_04.png)

5) You set your Cloud Foundry target successfully.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_05.png)


### Option B)
-->
1) Click on the **Cloud Foundry** Icon on the Activity Bar on the left side.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_01.png)

2) Expand **Services**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_02.png)

3) Click on the **Login to Cloud Foundry** Icon

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_03.png)

4) Provide the following inputs to the Cloud Foundry Sign In wizard:
   1) **Cloud Foundry Endpoint**: `https://api.cf.eu10.hana.ondemand.com`
   2) **Username**: `YOUR_EMAIL_ADDRESS`
   3) **Password**: `YOUR_DOMAIN_PASSWORD`
   4) Then click on **Sign in**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_04.png)

5) Select the following options in the Cloud Foundry Target wizard:
   1) **Cloud Foundry Organization**: `SharedServices`
   2) **Cloud Foundry Space**: `HANA Cloud Experience V2`
   3) Then click on **Apply**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_05.png)

6) You set your Cloud Foundry target successfully.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_06.png)

## Clone the preconfigured project

> You will import a HDI project prepared by us into BAS and open it up.

1) Click on **Clone from Git**

![img](Images/Image_ProjectSetup_Clone-the-preconfigured-project_01.png)

2) Insert the following link in the text box at the top: `https://github.com/SchneiderKarl/HCX_V2.git`
   
   After you pressed enter, the cloning process starts.

![img](Images/Image_ProjectSetup_Clone-the-preconfigured-project_02.png)

<!-- Screenshot mit OKay 

1) After you pressed enter, the cloning process starts.  When it is done you will receive a notification at the bottom right.

![img](Images/Image_ProjectSetup_Clone-the-preconfigured-project_03.png)
-->

> You will open the imported project to the workspace to start working on it.

3) To open the cloned project, click on **Open**.

![img](Images/Image_ProjectSetup_Clone-the-preconfigured-project_04.png)

## Open the project

<!-- optional Change mta project name by appending Username, *Explain folder structure and files optional* - design time -->

> 

1) On the left, you should now see the imported project. In this area, you design your database objects. Click on the **arrow** next to the project name **HCX_V2** to expand the folder structure. Expand also the folder **db** and after it the folder **src**. It should look like this in the end.

![img](Images/Image_ProjectSetup__01.png)


## SAP HANA PROJECTS tab

<!-- *Explain structure and runtime optional* -->

> The SAP HANA PROJECTS tab allows you to deploy the created design-time objects to the SAP HANA Cloud runtime. 

1) Take the SAP HANA Projects tab, located at the bottom of your screen, expand, and pull it up to the middle of the screen. For a better overview, expand the **HCX_V2/db**. It should look like this in the end.

![img](Images/Image_ProjectSetup__02.png)

## Bind SAP HDI Container

> <!--SAP HDI stands for SAP HANA Deployment Infrastructure. *HDI under the Hood Video - SAP Academy*-->

1) Click on the plug symbol next to the **hdi_db** to create an HDI Container.

![img](Images/Image_ProjectSetup__03.png)

2) The command line at the top should pop up. Click on **Bind to the default service instance**.

![img](Images/Image_ProjectSetup__04.png)

3) Building your HDI container initially takes around one and a half minutes.

![img](Images/Image_ProjectSetup__05.png)

4) After the process of creating and binding of the HDI container has ended a pop up ist opening. Click on **Enable & do not ask again**

![img](Images/Image_ProjectSetup__09.png)


## Bind existing User-Provided Service instance

> To access data that resides outside of the HDI Container and access remote sources that are already created, we will need to use a user-provided service. 

1) Click on the **Plug-Symbol** on the **cross-container-service-1** in the bottom part to bind this service (if you do not see the Plug-Symbol, hover over it).

![img](Images/Image_ProjectSetup__06.png)

2) Select the first binding option: **Bind to the 'REMOTE_SOURCE_GRANTOR_UPS' service**

![img](Images/Image_ProjectSetup__07.png)

3) If successful, you should see the following message:

![img](Images/Image_ProjectSetup__08.png)


## Deploy the project to HANA Cloud

> <!--Deploying...-->

1) Click on the rocket symbol to **deploy** the design-time objects to the SAP HANA Cloud runtime. 

![img](Images/Image_ProjectSetup__10.png)

2) The terminal opens and first of all some needed node modules will be installed. After this is done the deployment to HANA Cloud starts. After this has come to an end you see a massage if the deployment was successful.

![img](Images/Image_ProjectSetup__11.png)


## Open the SAP HANA Database Explorer

1) Click on **Open HDI container**

![img](Images/Image_ProjectSetup__12.png)

2) Click on **Open**

![img](Images/Image_ProjectSetup__13.png)

3) Select **Sign in with default identity provider**

![img](Images/Image_ProjectSetup__14.png)

4) You can see your HDI container in the SAP HANA Cloud runtime. The database objects are organized by their types in a catalog. Leave the Database Explorer tab open and return to BAS.

![img](Images/Image_ProjectSetup__15.png)

< [Back to Overview](README.md)