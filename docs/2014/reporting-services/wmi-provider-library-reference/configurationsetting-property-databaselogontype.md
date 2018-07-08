---
title: Propriedade DatabaseLogonType (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
caps.latest.revision: 24
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 001eee372f6c35a6938f3e5c99b9e82524285d25
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166127"
---
# <a name="databaselogontype-property-wmi-msreportserverconfigurationsetting"></a>Propriedade DatabaseLogonType (WMI MSReportServer_ConfigurationSetting)
  Especifica se o servidor de relatório usa uma conta de serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, uma conta do usuário do Windows ou um logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto `integer` que representa o tipo de logon.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 Os valores são:  
  
-   0 para logon do Windows  
  
-   1 para logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 para fazer logon como um serviço  
  
 Se você especificar 0 (Windows), você deve definir o valor [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) propriedade para uma conta de usuário válida do Windows correspondente.  
  
 Se você especificar 1 (SQL Server), verifique se o valor da [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) corresponde à válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
 Se você especificar 2 (serviço Windows), o servidor de relatório usará uma conta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e a conta de serviço do Windows para acessar o banco de dados do servidor de relatório. A propriedade DatabaseLogonAccount é ignorada.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros de MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
