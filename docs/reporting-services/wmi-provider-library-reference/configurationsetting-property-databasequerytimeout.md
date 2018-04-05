---
title: Propriedade DatabaseQueryTimeout (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7d581a0b435bfca1bd376d9eacb9256a7fca13c1
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-property---databasequerytimeout"></a>Propriedade de ConfigurationSetting – DatabaseQueryTimeout
  Especifica o número de segundos que devem decorrer antes de o servidor de relatório assumir que o comando falhou ou demorou demais para executar. O servidor de relatório está cronometrando a consulta no catálogo de SQL, não uma fonte de dados para o relatório. Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **inteiro** sem sinal de 32 bits que representa o número de segundos que a consulta tem permissão para executar.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
