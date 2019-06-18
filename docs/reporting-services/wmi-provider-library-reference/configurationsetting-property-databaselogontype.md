---
title: Propriedade DatabaseLogonType (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseLogonType
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 078c430e2300a0b80f85357f9f962e8e2dd72838
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570903"
---
# <a name="configurationsetting-property---databaselogontype"></a>Propriedade de ConfigurationSetting – DatabaseLogonType
  Especifica se o servidor de relatório usa uma conta de serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, uma conta do usuário do Windows ou um logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar o banco de dados do servidor de relatório. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **integer** que representa o tipo de logon.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 Os valores são:  
  
-   0 para logon do Windows  
  
-   1 para logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 para fazer logon como um serviço  
  
 Se você especificar 0 (Windows), deverá definir o valor na propriedade [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) com uma conta de usuário válida e correspondente do Windows.  
  
 Se especificar 1 (SQL Server), certifique-se de que o valor de [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) corresponda a um logon válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se você especificar 2 (serviço Windows), o servidor de relatório usará uma conta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e a conta de serviço do Windows para acessar o banco de dados do servidor de relatório. A propriedade DatabaseLogonAccount é ignorada.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
