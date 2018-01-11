---
title: Propriedade DatabaseLogonAccount (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname: DatabaseLogonAccount
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: "24"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: efbde911a4fe861310abb2678723c5e3696d95e0
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-property---databaselogonaccount"></a>Propriedade de ConfigurationSetting – DatabaseLogonAccount
  Especifica a conta de logon que o servidor de relatório usa para se conectar ao banco de dados do servidor de relatório. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **String** que representa o nome da conta do logon.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 Valores válidos para esta propriedade variarão dependendo do valor da propriedade [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) .  
  
 Essa propriedade será ignorada se a propriedade [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) for definida como **2 (Service)**.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
