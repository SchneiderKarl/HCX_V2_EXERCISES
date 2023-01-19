# Project Setup (Mandatory)

## Table of contents 

- [Project Setup (Mandatory)](#project-setup-mandatory)
  - [Table of contents](#table-of-contents)
  - [Access SAP Business Application Studio](#access-sap-business-application-studio)
  - [Create Development Space in BAS](#create-development-space-in-bas)
  - [Customize the default BAS layout](#customize-the-default-bas-layout)
  - [Set Cloud Foundry Endpoint](#set-cloud-foundry-endpoint)
    - [Option A)](#option-a)
    - [Option B)](#option-b)
  - [Clone or import the preconfigured project](#clone-or-import-the-preconfigured-project)
  - [Open the project](#open-the-project)
  - [SAP HANA PROJECTS tab](#sap-hana-projects-tab)
  - [Bind SAP HDI Container](#bind-sap-hdi-container)
  - [Bind existing User-Provided Service instance](#bind-existing-user-provided-service-instance)
  - [Deploy the project to HANA Cloud](#deploy-the-project-to-hana-cloud)

## Access SAP Business Application Studio

>(recommend use an incognito tab in one of the following Browser and their latest browser version https://help.sap.com/docs/SAP%20Business%20Application%20Studio/9d1db9835307451daa8c930fbd9ab264/8f46c6e6f86641cc900871c903761fd4.html#availability)
>- Mozilla Firefox
>- Google Chrome
>- Microsoft Edge

Click [here](link|bas) to open the SAP Business Application Studio (BAS for short).

## Create Development Space in BAS

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

>(If possible set default editors for hdi artifacts)

## Set Cloud Foundry Endpoint

> To start developing, you need to tell BAS where you want to deploy your project.

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
   2) **Cloud Foundry Space**: `dev`
   3) Then click on **Apply**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_04.png)

5) You set your Cloud Foundry target successfully.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-A_05.png)

### Option B)
1) Click on the **Cloud Foundry** Icon on the Activity Bar on the left side.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_01.png)

2) Expand the **Services**

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
   2) **Cloud Foundry Space**: `dev`
   3) Then click on **Apply**

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_05.png)

6) You set your Cloud Foundry target successfully.

![img](Images/Image_ProjectSetup_Set-Cloud-Foundry-Endpoint-Option-B_06.png)

## Clone or import the preconfigured project

1) Click on Clone from Git or Import
2) Insert the following link in the text box at the top: ``xxx``
3) After you pressed enter, the cloning process starts.  When it is done you will receive a notification at the bottom right.

## Open the project

1) To open the cloned project, click on **Open**.
2) On the left, you should now see the imported project. In this area, you design your database objects. Click on the **arrow** next to the project name to expand the folder structure.
3) *Explain folder structure and files optional* - design time
4) optional Change mta project name by appending Username

## SAP HANA PROJECTS tab

1) *Explain structure and runtime optional*
2) To bind your project to an HDI Container, you will need to use the runtime area. Take the **SAP HANA Projects** tab, located at the bottom of your screen, **expand**, and **pull it up to the middle of the screen**. For a better overview, **expand the folders**. 

## Bind SAP HDI Container

1) SAP HDI stands for SAP HANA Deployment Infrastructure. *HDI under the Hood Video - SAP Academy*
2) Click on the plug symbol next to the **hdi_hcx-db** to create an HDI Container.
3) The command line at the top should pop up. Click on **+ Create a new service** **instance**.
4) Behind the given name add a **-YOURNAME** and hit enter.
5) Building your HDI container initially takes around one and a half minutes.

## Bind existing User-Provided Service instance

1) To access data that resides outside of the HDI Container and access remote sources that are already created, we will need to use a user-provided service. 
2) Click on the **Plug-Symbol** on the **cross-container-service-1** in the bottom part to bind this service (if you do not see the Plug-Symbol, hover over it).
3) Select the first binding option: **Bind to the 'HCX_SCHEMA_UPS' service**
4) If successful, you should see the following message:


(Idea: Bevor every Chapter short Info what is happening exactly)

## Deploy the project to HANA Cloud

Click on the rocket symbol to **deploy** the design-time objects to the SAP HANA Cloud runtime. The terminal opens and lets you know if the deployment was successful.