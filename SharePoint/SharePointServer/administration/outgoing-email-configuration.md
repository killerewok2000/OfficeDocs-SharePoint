---
title: "Configure outgoing email for a SharePoint Server farm"
ms.author: stevhord
author: bentoncity
manager: pamgreen
ms.date: 3/12/2018
ms.audience: ITPro
ms.topic: article
ms.prod: sharepoint-server-itpro
localization_priority: Normal
ms.collection: IT_Sharepoint_Server_Top
ms.assetid: f3ccc8bd-922e-49f6-9929-b5b8a6982d76
description: "Summary: Learn how to install and configure the SMTP service and configure outgoing email for a SharePoint Server 2016 and SharePoint 2013 farm."
---

# Configure outgoing email for a SharePoint Server farm

 **Summary:** Learn how to install and configure the SMTP service and configure outgoing email for a SharePoint Server 2016 and SharePoint 2013 farm. 
  
This article describes how to configure outgoing email for a farm or for a specific web application for SharePoint Server. This article also describes how to install and configure the SMTP service that you must use to enable outgoing email.
  
After you have installed SharePoint Server and completed the initial configuration of your server farm, you can configure outgoing email. Doing so enables users to create alerts to track such site items as lists, libraries, and documents. In addition, site administrators can receive administrative messages about site administrator issues, such as the information that site owners have exceeded their specified storage space. For more information, see [Plan outgoing email for a SharePoint Server farm](outgoing-email-planning.md).
  
To configure outgoing email for a specific web application, first configure the default outgoing email for all web applications in the farm. If you configure the outgoing email for a specific web application, that configuration will override the default configuration for all web applications in the farm.
  
You can also configure outgoing email for a specific web application by using Microsoft PowerShell. For more information, see the "Configure the settings for a specific web application" section in [SharePoint Server 2016 outgoing email configuration settings](https://social.technet.microsoft.com/wiki/contents/articles/34167.sharepoint-2016-outgoing-email-configuration-settings.aspx#Configure_using_the_PowerShell).
  
    
## Before you begin
<a name="begin"> </a>

Before you begin this operation, review the following information about prerequisites:
  
- Your computer is running SharePoint Server 2016, SharePoint Server 2013, or SharePoint Foundation 2013.
    
- One or more servers in the server farm are running the Simple Mail Transfer Protocol (SMTP) service and have a valid SMTP server address. Alternatively, you must know the name of a server outside the farm that is running the SMTP service.
    
## Install and configure the SMTP service
<a name="begin"> </a>

Before you can enable outgoing email, you must determine which SMTP server to use. This SMTP server must be configured to allow anonymous SMTP email submissions. The SMTP server can be a server in the farm or outside the farm.
  
> [!NOTE]
> If your organization does not allow anonymous SMTP email messages to be sent by using Exchange Server, you can use a local SMTP server in the SharePoint farm that accepts anonymous email messages. The local SMTP server automatically authenticates the messages and then forwards them to the computer that's running Exchange Server. 
  
### Install the SMTP service

To install the SMTP service, use the Add Features Wizard in Server Manager. The wizard creates a default SMTP configuration. You can customize this default SMTP configuration to meet the requirements of your organization.
  
If you've already installed the SMTP service on a server, skip to [Configure the SMTP service](outgoing-email-configuration.md#ConfigureSMTPservice).
  
 **To install the SMTP service**
  
1. Verify that the user account that is performing this procedure is a member of the Administrators group on the application server.
    
2. Open **Server Manager**, click **Manage**, and select **Add Roles and Features**.
    
3. Click **Next** until the Select features page appears, select **SMTP Server**, click **Add Features**, and then click **Next**..
    
4. On the Confirm Installation Selections page, click **Install**.
    
5. On the Installation Results page, check that the installation finished successfully, and then click **Close**.
    
### Configure the SMTP service
<a name="ConfigureSMTPservice"> </a>

After you install the SMTP service, you configure it to send email messages from servers in the farm.
  
You can decide to send relayed email messages to all servers except those that you specifically exclude. Alternatively, you can block messages to all servers except those that you specifically include. You can include servers individually or in groups by subnet or domain.
  
If you enable anonymous access and relayed email messages, you increase the possibility that the SMTP server will be used to relay unsolicited commercial email messages (spam). It is important to limit this possibility by carefully configuring mail servers to help protect against spam. One way that you can do this is by limiting relayed email messages to a list of specific servers or to a domain, and by preventing relayed email messages from all other servers.
  
> [!NOTE]
> To manage the SMTP service on Windows Server 2008, Windows Server 2012 R2 and Windows Server 2016, you must use Internet Information Services (IIS) 6.0 Manager. Ensure that you install IIS 6.0 Management tools in Server Manager. 
  
### To install IIS 6.0 Management tools
<a name="ConfigureSMTPservice"> </a>

1. Verify that you have the following administrative credentials:
    
  - You must be a member of the Administrators group on the front-end web server.
    
2. Open **Server Manager**, click **Manage**, and select **Add Roles and Features**.
    
3. Click **Next** until the Select server roles page appears, select **Management Tools** and **IIS 6 Management compatibility**, and then click **Install**.
    
4. In **Application Server** section, click **Add Role Services**.
    
5. On the Select Role Services page, select **Management Tools** and **IIS 6 Management compatibility**, and then click **Install**.
    
### To configure the SMTP service
<a name="ConfigureSMTPservice"> </a>

1. Verify that the user account that is performing this procedure is a member of the Administrators group on the application server. 
    
2. Open Server Manager, click **Tools**, and select click **Internet Information Services (IIS) 6.0 Manager**.
    
3. In IIS Manager, expand the server name that contains the SMTP server that you want to configure. 
    
4. Right-click the SMTP virtual server that you want to configure, and then click **Start**, and then right-click the server again and click **Properties**.
    
5. On the **Access** tab, in the **Access control** area, click **Authentication**.
    
6. In the **Authentication** dialog box, verify that **Anonymous access** is selected, and click **OK**.
    
7. On the **Access** tab, in the **Relay restrictions** area, click **Relay**.
    
8. To enable relayed email messages to any server, click **All except the list below**.
    
9. To accept relayed email messages from one or more specific servers, follow these steps:
    
  - Click **Only the list below**.
    
  - Click **Add**, and then add servers one at a time by IP address, or in groups by using a subnet or domain.
    
  - Click **OK** three times to close the **Computer**, **Relay Restrictions**, and **Properties** dialog boxes. 
    
Ensure that the SMTP service is running and set to start automatically. To do this, use the following procedure.
  
### To set the SMTP service to start automatically
<a name="ConfigureSMTPservice"> </a>

1. Open Server Manager, click **Tools**, and then click **Services**.
    
2. In **Services**, right-click **Simple Mail Transfer Protocol (SMTP)**, and then select **Properties**.
    
3. In the **Simple Mail Transfer Protocol (SMTP) Properties** dialog box, on the **General** tab, in the **Startup type** list, select **Automatic**, and then click **OK**.
    
## Configure outgoing email for a farm
<a name="begin"> </a>

You can configure outgoing email for a farm by using the SharePoint Central Administration website. Use the following procedures to configure outgoing email. After you complete the procedures, users can track changes and updates to individual site collections. In addition, site administrators can, for example, receive notices when users request access to a site.
  
 **To configure outgoing email for a farm by using Central Administration**
  
1. Verify that the user account that is performing this procedure is a member of the Farm Administrators group on the server that is running Central Administration.
    
2. In Central Administration, click **System Settings**.
    
3. On the System Settings page, in the **E-Mail and Text Messages (SMS)** section, click **Configure outgoing e-mail settings**.
    
4. On the Outgoing E-Mail Settings page, in the **Mail Settings** section, type the SMTP server name for outgoing email (for example, mail.example.com) in the **Outbound SMTP server** box. 
    
5. In the **From address** box, type the email address as you want it to be displayed to email recipients. 
    
6. In the ** Reply-to address ** box, type the email address to which you want email recipients to reply. 
    
7. In the **Use TLS connection encryption** box, select **Yes** or **No** in the drop-down box. 
    
8. In the **SMTP server port** box, type the port number for your SMTP. By default, SMTP is configured on port 25. 
    
9. In the **Character set** list, select the character set that is appropriate for your language. 
    
10. Click **OK**.
    
## Configure outgoing email for a specific web application
<a name="begin"> </a>

You can configure outgoing email for a specific web application by using the Central Administration website. Use the following procedures to configure outgoing email. 
  
> [!NOTE]
> To configure outgoing email for a specific web application, first configure the default outgoing email for all web applications in the farm. If you configure the outgoing email for a specific web application, that configuration will override the default configuration for all web applications in the farm. 
  
 **To configure outgoing email for a specific web application by using Central Administration**
  
1. Verify that the user account that is performing this procedure is a member of the Farm Administrators group on the server that is running the SharePoint Central Administration website.
    
2. In Central Administration, in the **Application Management** section, click **Manage web applications**.
    
3. On the Web Applications Management page, select a web application, and then in the **General Settings** group on the ribbon, click **Outgoing E-mail**.
    
4. On the Web Application Outgoing E-Mail Settings page, in the **Mail Settings** section, type the name of the SMTP server for outgoing email (for example, mail.fabrikam.com) in the **Outbound SMTP server** box. 
    
5. In the **From address** box, type the email address (for example, the site administrator alias) as you want it to be displayed to email recipients. 
    
6. In the **Reply-to address** box, type the email address (for example, a help desk alias) to which you want email recipients to reply. 
    
7. In the **Use TLS connection encryption** box, select **Yes** or **No** in the drop-down box. 
    
8. In the **SMTP server port** box, type the port number for your SMTP. By default, SMTP is configured on port 25. 
    
9. In the **Character set** list, click the character set that is appropriate for your language. 
    
10. Click **OK**.
    
## See also
<a name="begin"> </a>

#### Concepts

[Plan outgoing email for a SharePoint Server farm](outgoing-email-planning.md)

