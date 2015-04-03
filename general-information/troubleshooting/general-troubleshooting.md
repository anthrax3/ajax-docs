---
title: General Troubleshooting
page_title: General Troubleshooting | UI for ASP.NET AJAX Documentation
description: General Troubleshooting
slug: introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/general-troubleshooting
tags: general,troubleshooting
published: True
position: 1
---

# General Troubleshooting



## 

This article lists common problems and their solutions. You can go through the list below to see if your case is described there. You can also use the browser find command (Ctrl+F) to search for the error you get.

Here is a list with the main sections:

* [Error message "'Telerik' is undefined" when running a website on IIS 7+ Integrated mode](#error-message-"'telerik'-is-undefined"-when-running-a-website-on-iis-7+-integrated-mode)

* [ Error message, "The type 'System.Web.UI.IScriptControl' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.Extensions, Version=1.0.61025.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'" ](#error-message,-"the-type-'system.web.ui.iscriptcontrol'-is-defined-in-an-assembly-that-is-not-referenced.-you-must-add-a-reference-to-assembly-'system.web.extensions,-version=1.0.61025.0,-culture=neutral,-publickeytoken=31bf3856ad364e35'")

* [ Error message, "The control with ID '[ControlID]' requires a ScriptManager on the page. The ScriptManager must appear before any controls that need it." ](#error-message,-"the-control-with-id-'[controlid]'-requires-a-scriptmanager-on-the-page.-the-scriptmanager-must-appear-before-any-controls-that-need-it.")

* [Error message, "Microsoft JScript runtime error: 'Sys' is undefined"](#error-message,-"microsoft-jscript-runtime-error:-'sys'-is-undefined")

* [Error message, "The Controls collection cannot be modified because the control contains code blocks"](#error-message,-"the-controls-collection-cannot-be-modified-because-the-control-contains-code-blocks")

* [ Problem: Telerik control stylesheet is not registered after an AJAX request (inside MS UpdatePanel) when the control is not initially visible on the page ](#telerik-control-stylesheet-is-not-registered-after-an-ajax-request-(inside-ms-updatepanel)-when-the-control-is-not-initially-visible-on-the-page)

* [Problem: Using the Telerik controls with RadScriptManager on your login page throws an error](#using-the-telerik-controls-with-radscriptmanager-on-your-login-page-throws-an-error)

* [Problem: Design-Time error on a page using Telerik controls](#design-time-error-on-a-page-using-telerik-controls)

* [Problem: System.IO.FileLoadException: Could not load file or assembly 'Telerik.Web.UI, Version=xxxx.x.xxx.xx, Culture=neutral, PublicKeyToken=xxxxxxxxxxxxxxxx' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)](#system.io.fileloadexception:-could-not-load-file-or-assembly-'telerik.web.ui,-version=xxxx.x.xxx.xx,-culture=neutral,-publickeytoken=xxxxxxxxxxxxxxxx'-or-one-of-its-dependencies.-the-located-assembly's-manifest-definition-does-not-match-the-assembly-reference.-(exception-from-hresult:-0x80131040))

* [Problem: Telerik controls do not work if a Compression Module is used in the project/web site](#telerik-controls-do-not-work-if-a-compression-module-is-used-in-the-project/web-site)

* [Problem: Security Exception](#security-exception)

* [Problem: Setting ClientIDMode property to Static breaks the Telerik controls functionality](#setting-clientidmode-property-to-static-breaks-the-telerik-controls-functionality)

* [Problem: Telerik controls are incompatible with Ajax Control Toolkit](#telerik-controls-are-incompatible-with-ajax-control-toolkit)

* [Problem: Telerik controls integration with Kendo UI widgets](#telerik-controls-integration-with-kendo-ui-widgets)

## Error message "'Telerik' is undefined" when running a website on IIS 7+ Integrated mode

*Problem:*

__Error message "'Telerik' is undefined" when running a website on IIS 7+ Integrated mode.__

*Suggested Solution:*

When in integrated mode, IIS7 reads the application configuration from the __<system.webServer>__ section group in the application configuration file, but not the __<system.web>__ section group. Since Visual Studio 2005 does not provide "native" support for IIS7, the __RadScriptManager__ registration cannot be automatically added to the __system.webServer__.

To solve the problem you should manually add the __HttpHandler registration__ to the __system.webServer__ section group. There are two cases:

* Telerik.Web.UI.dll is in the __GAC__:

````XML
	<system.webServer>
	…
		<handlers>
		…
			<add name="Telerik.Web.UI.WebResource"  path="Telerik.Web.UI.WebResource.axd" verb="*" type="Telerik.Web.UI.WebResource, Telerik.Web.UI, Version=[ASSEMBLY_VERSION], Culture=neutral, PublicKeyToken=121fae78165ba3d4" />
		…
		</handlers>
	</system.webServer> 
````



>caution You need to replace [ __ASSEMBLY_VERSION__ ] with the exact version of your DLL.
>


* Telerik.Web.UI.dll is __not in the GAC__:

````XML
	<system.webServer>
	…
		<handlers>
		…
			<add name="Telerik.Web.UI.WebResource"  path="Telerik.Web.UI.WebResource.axd" verb="*" type="Telerik.Web.UI.WebResource, Telerik.Web.UI" />
		…
		</handlers>
	</system.webServer> 
````



Additional information is available in this blog post: [Web Resources demystified](http://blogs.telerik.com/aspnet-ajax/posts/08-07-18/web-resources-demystified-part-3-troubleshooting.aspx).

## Error message, "The type 'System.Web.UI.IScriptControl' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.Extensions, Version=1.0.61025.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'"

*Problem:*

__Error message, "The type 'System.Web.UI.IScriptControl' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.Extensions, Version=1.0.61025.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'"__

*Suggested Solution:*

This error occurs when you have added a control from Telerik UI for ASP.NET AJAX but your application is not configured to use ASP.NET AJAX. To fix it, you need to follow the steps described at [http://www.asp.net/ajax/documentation/live/ConfiguringASPNETAJAX.aspx](http://www.asp.net/ajax/documentation/live/ConfiguringASPNETAJAX.aspx) (read the topic called __Adding ASP.NET AJAX Configuration Elements to an Existing Web Site__).

## Error message, "The control with ID '[ControlID]' requires a ScriptManager on the page. The ScriptManager must appear before any controls that need it."

*Problem:*

__Error message, "The control with ID '[ControlID]' requires a ScriptManager on the page. The ScriptManager must appear before any controls that need it."__

*Suggested Solution:*

This error occurs when you have added a control from Telerik UI for ASP.NET AJAX to a page that does not contain a __ScriptManager__ control. To resolve this error, please add a __ScriptManager__ control to your page:

````ASPNET
	<asp:ScriptManager ID="ScriptManager1" runat="server" /> 
````



If you are using master pages, you can add the __ScriptManager__ control there. The __ScriptManager__ control must precede all controls from the Telerik UI for ASP.NET AJAX suite. For further details about the __ScriptManager__ control, you can read this article [http://msdn.microsoft.com/en-us/library/bb398863(v=vs.100).aspx](http://msdn.microsoft.com/en-us/library/bb398863(v=vs.100).aspx).

## Error message, "Microsoft JScript runtime error: 'Sys' is undefined"

*Problem:*

__Error message, "Microsoft JScript runtime error: 'Sys' is undefined"__

*Suggested Solution:*

This error occurs when you have added a control from Telerik UI for ASP.NET AJAX but your application is not configured to use ASP.NET AJAX. To fix it, you need to follow the steps described at [http://www.asp.net/ajax/documentation/live/ConfiguringASPNETAJAX.aspx](http://www.asp.net/ajax/documentation/live/ConfiguringASPNETAJAX.aspx) (read the topic called __Adding ASP.NET AJAX Configuration Elements to an Existing Web Site__).

## Error message, "The Controls collection cannot be modified because the control contains code blocks"

*Problem:*

__Error message, "The Controls collection cannot be modified because the control contains code blocks".__

*Suggested Solution:*

If you receive exceptions such as "System.Web.HttpException: The Controls collection cannot be modified because the control contains code blocks" you need to move the code block (i.e., <% ... %>) outside of the head tag:

Incorrect:

````ASPNET
	<head id="Head1" runat="server">
	  <script type="text/javascript">
	  var grid = $find('<%= RadGrid1.ClientID %>');
	  ...
	  </script>
	</head>
	<body>
	...
	</body> 
````



Correct:

````ASPNET
	<head id="Head2" runat="server">
	<telerik:RadCodeBlock id="RadCodeBlock1" runat="server">
	   <script type="text/javascript">
	       var grid = $find('<%= RadGrid1.ClientID %>');
	       ...
	   </script>
	</telerik:RadCodeBlock>
	</head>
	<body>
	...
	</body>
	or
	<head id="Head3" runat="server">
	</head>
	<body>
	   <telerik:RadCodeBlock id="RadCodeBlock1" runat="server">
	   <script type="text/javascript">
	       var grid = $find('<%= RadGrid1.ClientID %>');
	       ...
	   </script>
	   </telerik:RadCodeBlock>
	</body>   
````



## Telerik control stylesheet is not registered after an AJAX request (inside MS UpdatePanel) when the control is not initially visible on the page

*Problem:*

__Telerik control stylesheet is not registered after an AJAX request (inside MS UpdatePanel) when the control is not initially visible on the page__

*Suggested Solution:*

If the control is initially invisible and is shown after an ASP.NET AJAX update, you should manually register all the required CSS files in the head tag of your page. Otherwise, the control will not be displayed correctly. The easiest way to do this is through a LINK element:

	<link href="<my_path_to_stylesheet>" rel="stylesheet" runat="server" > 



Alternatively, replace the MS UpdatePanel with __RadAjaxPanel__ or ajaxify the control via __RadAjaxManager__. Thus the stylesheet should be applied properly after an AJAX request even if the __Telerik control__ is initially invisible.

## Using the Telerik controls with RadScriptManager on your login page throws an error

*Problem:*

__Using the Telerik controls with RadScriptManager on your login page throws one of the following errors:__

* __ASP.NET Ajax client-side framework failed to load__

* __'Sys' is undefined__

* __"Telerik.Web.UI" is undefined__

*Cause:*

As the website denies access to all pages to unauthorized users, access to the __Telerik.Web.UI.WebResource.axd__ handler is unauthorized. This causes the handler to serve the content of the login page instead of the combined scripts, hence the error.

*Suggested Solution:*

Add a __<location>__ section to the application configuration file to allow access to __Telerik.Web.UI.WebResource.axd__ to all users, like:

````XML
	<configuration>
	...
	<location path="Telerik.Web.UI.WebResource.axd">
	   <system.web>
	     <authorization>
	       <allow users="*"/>
	     </authorization>
	   </system.web>
	 </location>
	...
	</configuration> 
````



## Design-Time error on a page using Telerik controls

*Problem:*

__Design-Time error on a page using Telerik controls:__

__Error Creating Control -____'Property'__

*Cause:*

If the __Telerik.Web.UI.dll__ assembly is updated while a page using __Telerik controls__ is in Design-time, VisualStudio creates two different versions of the assembly; hence two different versions of the same __Telerik controls__ are available.

*Suggested Solution:*

Restart Visual Studio.



*Problem:*

When you drag a __Telerik control__ from the Toolbox to the design surface, you get this error message:

__Error creating control. Unable to cast object of type 'Telerik.Web.UI.Radxxx' to type 'Telerik.Web.UI.ControlItemContainer"__

*Suggested Solution:*

Please check the following links for different solution options: [link 1](http://www.telerik.com/community/forums/aspnet-ajax/menu/menu-problem-39-error-creating-control-39-at-design-time.aspx), [link 2](http://www.telerik.com/community/forums/aspnet-ajax/general-discussions/ajax-2009-q2-release-giving-me-gray-hair.aspx) and [link 3](http://blogs.microsoft.co.il/blogs/kolbis/archive/2008/06/29/unable-to-cast-object-from-type-x-to-type-x.aspx).

*Problem:*

__Design-time error on a page using Telerik controls after upgrading to Q1 2009__

__Error creating control -__

__Failed to create designer "Telerik.Web.UI.ControlName..."__

*Cause:*

Visual Studio 2008 has a problem with loading GAC-ed design-time assemblies of control libraries deployed in the Bin folder of a web site.

*Suggested Solutions (select one of these):*

1. Install SP1 of Visual Studio 2008.

1. Bin-deploy the design-time assembly

* Add a reference to Telerik.Web.Design.dll to your web site or application

* Remove Telerik.Web.Design.dll from the GAC

* Restart Visual Studio

1. GAC-deploy the control library assembly

* Add Telerik.Web.UI.dll in the GAC

* Remove Telerik.Web.UI.dll from your bin folder

* Restart Visual Studio

1. Copy __Telerik.Web.UI.dll__ to __C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PublicAssemblies__ and restart Visual Studio.



You can find more issues and solutions steps in the [Design-time Troubleshooting]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/design-time-troubleshooting%}) help article.

## System.IO.FileLoadException: Could not load file or assembly 'Telerik.Web.UI, Version=xxxx.x.xxx.xx, Culture=neutral, PublicKeyToken=xxxxxxxxxxxxxxxx' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)

*Problem:*

__System.IO.FileLoadException: Could not load file or assembly 'Telerik.Web.UI, Version=xxxx.x.xxx.xx, Culture=neutral, PublicKeyToken=xxxxxxxxxxxxxxxx' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)__

*Cause:*

There is a reference to a version of Telerik.Web.UI in the web.config that is different from the version of the deployed assembly.

*Suggested Solution:*

Update the reference in the web.config to match the version of the deployed assembly.

## Telerik controls do not work if a Compression Module is used in the project/web site

*Problem:*

__Telerik controls do not work if a Compression Module is used in the project/web site.__

*Cause:*

Double compression of web resources: Web resources requested by the __Telerik controls__ are compressed twice: once by the Script/RadScript/RadStyleSheet- Manager and once by the Compression Module.

*Suggested Solution:*

Skip compression for the requested resource in the Compression Module. If the __OutputCompression__ property of RadScriptManager/RadStyleSheetManager is set to __Disabled__, you can configure the Compression Module to compress __Telerik.Web.UI.WebResource.axd__.




>caption  

|  __Control__  |  __Requested Resources__  |
| ------ | ------ |
|ScriptManager|WebResource.axdScriptResource.axd|
|RadScriptManager|Telerik.Web.UI.WebResource.axd|
|RadStyleSheetManager|Telerik.Web.UI.WebResource.axd|

## Security Exception

*Problem:*

__Security Exception__

__Description:__The application attempted to perform an operation not allowed by the security policy. To grant this application the required permission, please contact your system administrator or change the application's trust level in the configuration file. __Exception Details:__System.Security.SecurityException:Request for the permission of type 'System.Web.AspNetHostingPermission,...

*Cause:*

Microsoft changed the default setting of the __Load User Profile__ setting of the application pools in Windows 7 and Windows 2008 (previously the setting was __True__, in IIS7.5 it is __False__).

*Suggested Solution:*

Open the __Advanced Settings__ of the Application Pool and set the __Load User Profile__ property to __True__.

## Setting ClientIDMode property to Static breaks the Telerik controls functionality

*Problem:*

__Setting ClientIDMode property to Static breaks the Telerik controls functionality__

*Suggested Solution:*

Please note that using __ClientIDMode=Static__ mode __for Telerik AJAX controls is not supported__. You should use __AutoID__ mode for the Telerik controls on the page especially when they are performing AJAX requests. Microsoft recommends using __ClientIDMode="Static"__ only for static controls. The Telerik controls, on the other hand, are controls with complex hierarchies of child controls and templates so setting their ClientID mode to static will break their functionality.

## Telerik controls are incompatible with Ajax Control Toolkit

The AJAX Toolkit Team announced that standard script manager can no longer be used with their controls:

*“- You must use the ToolkitScriptManager instead of the ScriptManager with the Ajax Control Toolkit.”*

[http://ajaxcontroltoolkit.codeplex.com/releases/view/112805](http://ajaxcontroltoolkit.codeplex.com/releases/view/112805)

Since the __RadScriptManager__ is based on the standard asp:ScriptManager, this change makes it not compatible, too. Therefore, to use both of the Telerik UI and AJAX Toolkit control bundles simultaneously within the same project, you have to use the __ToolkitScriptManager__.

Upon using the toolkit manager, you can come across an error when using an UpdatePanel. We’ve found out that this is due to the __ToolkitScriptManager__ having a bug with script combining. The bug is fixed one day after the release:

[http://ajaxcontroltoolkit.codeplex.com/workitem/27517](http://ajaxcontroltoolkit.codeplex.com/workitem/27517)

[http://ajaxcontroltoolkit.codeplex.com/releases/view/116091](http://ajaxcontroltoolkit.codeplex.com/releases/view/116091)

The problem can be reproduced in release mode when scripts are combined and after an AJAX request. The temporary workaround is to set the __CombineScripts__ property in the __ToolkitScriptManager__ tag to __false__. The issue is not reproducible into debug mode, because the script combining logic works only in release mode.

You can find additional information about the Telerik controls and AJAX Control Toolkit history in the following article:

[RadScriptManager Troubleshooting](http://www.telerik.com/help/aspnet-ajax/troubleshooting-radscriptmanager.html)

## Telerik controls integration with Kendo UI widgets

There are certain Telerik controls like RadHtmlChart, RadGauge, RadDiagram, RadMap, RadGannt, RadTreeMap, RadClientDataSource, RadClientExportManagerwhich are ASP.NET server-side wrappers of Kendo UI widgets. These controls already load jQuery and Kendo UI widget specific JavaScript files, soyou must ensure there aren't any script conflicts by using the same jQuery and Kendo UI versions for both suites. More information is available in the[RadHtmlChart Integration With KendoUI Widgets](80f05187-cf53-4f47-abb2-5d654024f064) help article.

# See Also

 * [Design-time Troubleshooting]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/design-time-troubleshooting%})

 * [Web Resources Troubleshooting]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/web-resources-troubleshooting%})

 * [ToolBox Troubleshooting]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/toolbox-troubleshooting%})

 * [Skins Troubleshooting]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/troubleshooting/skins-troubleshooting%})