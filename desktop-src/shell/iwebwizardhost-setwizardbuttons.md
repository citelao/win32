---
Description: Updates the Back, Next, and Finish buttons in the client's wizard frame.
title: WebWizardHost.SetWizardButtons method
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
topic_type: 
- APIRef
- kbSyntax
api_name: 
- WebWizardHost.SetWizardButtons
api_type: 
- COM
api_location: 
- Shldisp.h
---

# WebWizardHost.SetWizardButtons method

Updates the **Back**, **Next**, and **Finish** buttons in the client's wizard frame.

## Syntax


```JScript
iRetVal = WebWizardHost.SetWizardButtons(
  vbEnableBack,
  vbEnableNext,
  vbLastPage
)
```



## Parameters

<dl> <dt>

*vbEnableBack* \[in\]
</dt> <dd>

Type: **Boolean**

Enables the **Back** button.

</dd> <dt>

*vbEnableNext* \[in\]
</dt> <dd>

Type: **Boolean**

Enables the **Next** button.

</dd> <dt>

*vbLastPage* \[in\]
</dt> <dd>

Type: **Boolean**

Enables the **Finish** button. States that this is the last server-side page.

</dd> </dl>

## Remarks

Be sure to implement handler functions in each server-side page for OnBack() and OnNext(), corresponding to the wizard buttons **Back** and **Next**. The OnBack() and OnNext() functions respond to **SetWizardButtons**. At the appropriate time, the OnNext() function calls **SetWizardButtons** with *vbLastPage*=**true**, which can enable a **Finish** button. OnNext() also calls [**FinalNext**](iwebwizardhost-finalnext.md) when a user clicks the **Finish** button.

## Requirements



|                                     |                                                                                        |
|-------------------------------------|----------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows XP \[desktop apps only\]<br/>                                            |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/>                                   |
| Header<br/>                   | <dl> <dt>Shldisp.h</dt> </dl>   |
| IDL<br/>                      | <dl> <dt>Shldisp.idl</dt> </dl> |



 

 



