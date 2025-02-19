---
title: Assign devices to servicing channels for Windows 10 updates (Windows 10)
description: Learn how to assign devices to servicing channels for Windows 10 updates locally, by using Group Policy, and by using MDM
ms.prod: w10
ms.mktglfcycl: deploy
author: jaimeo
ms.localizationpriority: medium
ms.author: jaimeo
ms.reviewer: 
manager: laurawi
ms.topic: article
ms.custom:
- seo-marvel-apr2020
---

# Assign devices to servicing channels for Windows 10 updates


**Applies to**

- Windows 10


> **Looking for consumer information?** See [Windows Update: FAQ](https://support.microsoft.com/help/12373/windows-update-faq) 

>[!TIP]
>If you're not familiar with the Windows 10 servicing or release channels, read [Servicing Channels](waas-overview.md#servicing-channels) first.
>
>Due to [naming changes](waas-overview.md#naming-changes), older terms like CB and CBB might still be displayed in some of our products, such as in Group Policy. If you encounter these terms, "CB" refers to the Semi-Annual Channel (Targeted)--which is no longer used--while "CBB" refers to the Semi-Annual Channel.

The Semi-Annual Channel is the default servicing channel for all Windows 10 devices except devices with the LTSB edition installed. The following table shows the servicing channels available to each Windows 10 edition. 

| Windows 10 edition | Semi-Annual Channel | Long-Term Servicing Channel | Insider Program |
| --- | --- | --- | --- |
| Home | ![no.](images/crossmark.png) | ![no](images/crossmark.png) | ![yes](images/checkmark.png) |
| Pro | ![yes.](images/checkmark.png) | ![no](images/crossmark.png) | ![yes](images/checkmark.png) |
| Enterprise  | ![yes.](images/checkmark.png) | ![no](images/crossmark.png) | ![yes](images/checkmark.png) |
| Enterprise LTSB  | ![no.](images/crossmark.png) | ![yes](images/checkmark.png) | ![no](images/crossmark.png) |
| Pro Education | ![yes.](images/checkmark.png) | ![no](images/crossmark.png) | ![yes](images/checkmark.png) |
| Education  | ![yes.](images/checkmark.png) | ![no](images/crossmark.png) | ![yes](images/checkmark.png) |


>[!NOTE]
>The LTSB edition of Windows 10 is only available through the [Microsoft Volume Licensing Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).



## Assign devices to Semi-Annual Channel

>[!IMPORTANT]
>Due to [naming changes](waas-overview.md#naming-changes), older terms like CB and CBB might still be displayed in some of our products, such as in Group Policy. If you encounter these terms, "CB" refers to the Semi-Annual Channel (Targeted)--which is no longer used--while "CBB" refers to the Semi-Annual Channel.

>[!NOTE]
>Devices will automatically recieve updates from the Semi-Annual Channel, unless they are configured to recieve preview updates through the Windows Insider Program.

**To assign devices to the Semi-Annual Channel by using Group Policy**


- In Windows 10, version 1607 and later releases:

    Computer Configuration > Administrative Templates > Windows Components > Windows Update > Defer Windows Updates > **Select when Feature Updates are received** - enable policy and set branch readiness level to the Semi-Annual Channel
    
**To assign devices to the Semi-Annual Channel by using MDM**


- In Windows 10, version 1607 and later releases:

    ../Vendor/MSFT/Policy/Config/Update/**BranchReadinessLevel**
    

## Enroll devices in the Windows Insider Program

To get started with the Windows Insider Program for Business, you will need to follow a few steps:

1. On the [Windows Insider](https://insider.windows.com) website, go to **For Business > Getting Started** to [register your organizational Azure AD account](https://insider.windows.com/insidersigninaad/).
2. **Register your domain**. Rather than have each user register individually for Insider Preview builds, administrators can [register their domain](https://insider.windows.com/for-business-organization-admin/) and control settings centrally.</br>**Note:** The signed-in user needs to be a **Global Administrator** of the Azure AD domain in order to be able to register the domain.
3. Make sure the **Allow Telemetry** setting is set to **2** or higher.
4. Starting with Windows 10, version 1709, set policies to manage preview builds and their delivery:

The **Manage preview builds** setting gives administrators control over enabling or disabling preview build installation on a device. You can also decide to stop preview builds once the release is public.
* Group Policy: **Computer Configuration/Administrative Templates/Windows Components/Windows Update/Windows Update for Business** - *Manage preview builds*
* MDM: **Update/ManagePreviewBuilds**

The **Branch Readiness Level** settings allow you to choose between preview flight rings, and allows you to defer or pause the delivery of updates.
* Group Policy: **Computer Configuration/Administrative Templates/Windows Components/Windows Update/ Windows Update for Business** - *Select when Preview Builds and Feature Updates are received*
* MDM: **Update/BranchReadinessLevel**

For more information, see [Windows Insider Program for Business](/windows-insider/at-work-pro/wip-4-biz-get-started)

## Block access to Windows Insider Program

To prevent devices in your organization from being enrolled in the Insider Program for early releases of Windows 10:

- Group Policy: Computer Configuration\Administrative Templates\Windows Components\Data Collection and Preview Builds\\**Toggle user control over Insider builds**
- MDM: Policy CSP - [System/AllowBuildPreview](/windows/client-management/mdm/policy-configuration-service-provider#System_AllowBuildPreview)

>[!IMPORTANT]
>Starting with Windows 10, version 1709, this policy is replaced by **Manage preview builds** policy.
> * Group Policy: **Computer Configuration/Administrative Templates/Windows Components/Windows Update/Windows Update for Business** - *Manage preview builds*
> * MDM: **Update/ManagePreviewBuilds**


## Switching channels

During the life of a device, it might be necessary or desirable to switch between the available channels. Depending on the channel you are using, the exact mechanism for doing this can be different; some will be simple, others more involved.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">From this channel</th>
<th align="left">To this channel</th>
<th align="left">You need to</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left" rowspan="3">Windows Insider Program</td>
</tr>
<tr class="even">
<td align="left">Semi-Annual Channel</td>
<td align="left">Not directly possible</td>
</tr>
<tr class="odd">
<td align="left">Long-Term Servicing Channel</td>
<td align="left">Not directly possible (requires wipe-and-load).</td>
</tr>
<tr class="odd">
<td align="left" rowspan="3">Semi-Annual Channel</td>
<td align="left">Insider</td>
<td align="left">Use the Settings app to enroll the device in the Windows Insider Program.</td>
</tr>
<tr class="even">
</tr>
<tr class="odd">
<td align="left">Long-Term Servicing Channel</td>
<td align="left">Not directly possible (requires wipe-and-load).</td>
</tr>
<tr class="even">
<td align="left" rowspan="3">Long-Term Servicing Channel</td>
<td align="left">Insider</td>
<td align="left">Use media to upgrade to the latest Windows Insider Program build.</td>
<tr class="even">
<td align="left">Semi-Annual Channel</td>
<td align="left">Use media to upgrade. Note that the Semi-Annual Channel build must be a later build.</td>
</tr>
</tbody>
</table>

## Block user access to Windows Update settings

In Windows 10, administrators can control user access to Windows Update.

Administrators can disable the "Check for updates" option for users by enabling the Group Policy setting under **Computer Configuration\Administrative Templates\Windows Components\Windows update\Remove access to use all Windows update features**. Any background update scans, downloads, and installations will continue to work as configured. We don't recomment this setting if you have configured the device to "notify" to download or install as this policy will prevent the user from being able to do so.

>[!NOTE]
> Starting with Windows 10, any Group Policy user configuration settings for Windows Update are no longer supported.

## Steps to manage updates for Windows 10

|&nbsp; |&nbsp; |
| --- | --- |
| ![done.](images/checklistdone.png) | [Learn about updates and servicing channels](waas-overview.md) |
| ![done.](images/checklistdone.png) | [Prepare servicing strategy for Windows 10 updates](waas-servicing-strategy-windows-10-updates.md) |
| ![done.](images/checklistdone.png) | [Build deployment rings for Windows 10 updates](waas-deployment-rings-windows-10-updates.md) |
| ![done.](images/checklistdone.png) | Assign devices to servicing channels for Windows 10 updates (this topic) |
| ![to do.](images/checklistbox.gif) | [Optimize update delivery for Windows 10 updates](waas-optimize-windows-10-updates.md) |
| ![to do.](images/checklistbox.gif) | [Deploy updates using Windows Update for Business](waas-manage-updates-wufb.md)</br>or [Deploy Windows 10 updates using Windows Server Update Services](waas-manage-updates-wsus.md)</br>or [Deploy Windows 10 updates using Microsoft Endpoint Configuration Manager](/mem/configmgr/osd/deploy-use/manage-windows-as-a-service) |

## Related topics

- [Update Windows 10 in the enterprise](index.md) 
- [Configure Delivery Optimization for Windows 10 updates](waas-delivery-optimization.md)
- [Configure BranchCache for Windows 10 updates](waas-branchcache.md)
- [Configure Windows Update for Business](waas-configure-wufb.md)
- [Integrate Windows Update for Business with management solutions](waas-integrate-wufb.md)
- [Walkthrough: use Group Policy to configure Windows Update for Business](waas-wufb-group-policy.md)
- [Walkthrough: use Intune to configure Windows Update for Business](/intune/windows-update-for-business-configure)
- [Manage device restarts after updates](waas-restart.md)
