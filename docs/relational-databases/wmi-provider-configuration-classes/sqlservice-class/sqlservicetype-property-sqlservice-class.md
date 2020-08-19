---
description: Propriedade SqlServiceType (classe SqlService)
title: Propriedade SqlServiceType (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: dbff2968-3011-41d6-a141-52d814af0213
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 91c54b33387dec747aca2c5b9c274bb709057821
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446130"
---
# <a name="sqlservicetype-property-sqlservice-class"></a>Propriedade SqlServiceType (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o tipo do serviço gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SqlServiceType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o tipo de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="remarks"></a>Comentários  
 Os valores retornados podem ser um destes  
  
|Type|Definição|  
|----------|----------------|  
|*1*|MSSQLSERVER é o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*2*|SQLSERVERAGENT é o serviço de Agente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*3*|MSFTESQL é o serviço do Mecanismo de Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*4*|MsDtsServer é o serviço do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .|  
|*5*|MSSQLServerOLAPService é o serviço do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|*6*|ReportServer é o serviço do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|  
|*7*|SQLBrowser é o serviço do Navegador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*8*|NsService é o [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] serviço de notificação.|  
|*9*|MSSQLFDLauncher é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço iniciador do daemon de filtro de texto completo.|  
|*10*|SQLPBENGINE é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço de mecanismo polybase.|  
|*11*|SQLPBDMS é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço de movimentação de dados do polybase.|  
|*12*|MSSQLLaunchpad é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço Launchpad.|  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
