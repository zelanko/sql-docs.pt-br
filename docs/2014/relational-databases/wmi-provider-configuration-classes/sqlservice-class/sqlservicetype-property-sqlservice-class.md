---
title: Propriedade SqlServiceType (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SqlServiceType Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SqlServiceType property
ms.assetid: dbff2968-3011-41d6-a141-52d814af0213
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d3fd5a90ba479ef8075e45dcaab16475c0284f19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62912150"
---
# <a name="sqlservicetype-property-sqlservice-class"></a>Propriedade SqlServiceType (classe SqlService)
  Obtém o tipo do serviço gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SqlServiceType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o tipo de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="remarks"></a>Comentários  
 Os valores retornados podem ser um destes  
  
|Type|Definição|  
|----------|----------------|  
|*1*|MSSQLSERVER é o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*2*|SQLSERVERAGENT é o serviço de Agente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*Beta*|MSFTESQL é o serviço do Mecanismo de Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*quatro*|MsDtsServer é o serviço do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .|  
|*05*|MSSQLServerOLAPService é o serviço do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|*6*|ReportServer é o serviço do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|  
|*7*|SQLBrowser é o serviço do Navegador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
