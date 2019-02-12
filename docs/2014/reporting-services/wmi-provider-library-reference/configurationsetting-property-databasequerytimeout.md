---
title: Propriedade DatabaseQueryTimeout (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseQueryTimeout Property
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cf21ba6211a016676ea7d1f2547bf4d96b1e6fb4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023758"
---
# <a name="databasequerytimeout-property-wmi-msreportserverconfigurationsetting"></a>Propriedade DatabaseQueryTimeout (WMI MSReportServer_ConfigurationSetting)
  Especifica o número de segundos que devem decorrer antes de o servidor de relatório assumir que o comando falhou ou demorou demais para executar. O servidor de relatório está cronometrando a consulta no catálogo de SQL, não uma fonte de dados para o relatório. Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto `integer` sem-sinal de 32 bits que representa o número de segundos que a consulta tem permissão para executar.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
