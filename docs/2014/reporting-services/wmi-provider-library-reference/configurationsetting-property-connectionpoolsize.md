---
title: Propriedade ConnectionPoolSize (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- ConnectionPoolSize
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ConnectionPoolSize property
ms.assetid: b80c8e5d-b725-4fe4-aec6-02fb18ec4434
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 24a180fde90ff406d40a0f0c89bf82dfe5138b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097868"
---
# <a name="connectionpoolsize-property-wmi-msreportserver_configurationsetting"></a>Propriedade ConnectionPoolSize (WMI MSReportServer_ConfigurationSetting)
  O tamanho do pool de conexão usado pelo servidor de relatório para se comunicar com a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados do servidor de relatório. Somente leitura.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## <a name="property-values"></a>Valores da propriedade  
 Um objeto **inteiro** somente leitura que retorna um valor de `768`.  
  
## <a name="example-code"></a>Código de exemplo  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Membros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
