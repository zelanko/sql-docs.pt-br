---
title: Propriedade SecureConnectionLevel (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fdb8fc97b8b2403366e19456b7c744012ee9007f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570257"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>Propriedade de ConfigurationSetting – SecureConnectionLevel
  Retorna o nível de conexão segura especificado no arquivo RSReportServer.config. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um valor **inteiro** que representa o nível de conexão segura. Os valores de retorno indicam se o SSL está configurado ou não. Um valor maior ou igual a 1 indica que o SSL está ativado. Um valor de 0 indica que o SSL está desativado.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Comentários

No SQL Server 2008 R2, o SecureConnectionLevel é transformado em uma opção de ativar/desativar. Para obter mais informações, consulte [Método ConfigurationSetting – SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md).

## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
