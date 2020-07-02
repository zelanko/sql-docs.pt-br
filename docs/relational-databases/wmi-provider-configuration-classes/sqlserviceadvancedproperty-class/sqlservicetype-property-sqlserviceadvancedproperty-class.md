---
title: Propriedade SqlServiceType (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b604f9e653f114879979ea3ad6546a201d090d38
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759805"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>Propriedade SqlServiceType (classe SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o tipo do serviço gerenciado associado com a propriedade avançada.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa uma propriedade avançada.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o tipo de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
  
  
