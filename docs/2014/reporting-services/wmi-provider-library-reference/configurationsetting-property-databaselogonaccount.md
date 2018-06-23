---
title: Propriedade DatabaseLogonAccount (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 75a929c87f963f102535c7fbe015a4bb49e6278f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019053"
---
# <a name="databaselogonaccount-property-wmi-msreportserverconfigurationsetting"></a>Propriedade DatabaseLogonAccount (WMI MSReportServer_ConfigurationSetting)
  Especifica a conta de logon que o servidor de relatório usa para se conectar ao banco de dados do servidor de relatório. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto `String` que representa o nome da conta do logon.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 Os valores válidos para essa propriedade variam dependendo do valor da [DatabaseLogonType](configurationsetting-property-databaselogontype.md) propriedade.  
  
 Essa propriedade será ignorada se o [DatabaseLogonType](configurationsetting-property-databaselogontype.md) está definida como `2 (Service)`.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  