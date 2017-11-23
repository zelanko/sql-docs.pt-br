---
title: dbo.slo_service_objectives (banco de dados do SQL Azure) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5330bc8977c0e043f27cb5f035510c5da007e0c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Esse recurso está em um estado de visualização e foi preterido no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
  
 Retorna informações sobre o objetivo de nível de serviço (SLO) no servidor atual.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|ID do objetivo de nível de serviço.|  
|name|**sysname**|Nome do objetivo de nível de serviço.|  
|descrição|**nvarchar**|Descrição do objetivo de nível de serviço.|  
|create_date|**DateTimeOffset(7)**|data de criação de objeto de nível de serviço no servidor.|  
|is_system|**bit**|1 = objetivo de nível de serviço do sistema|  
|is_default|**bit**|1 = o objetivo de nível de serviço é o SLO padrão.|  
|state|**tinyint**|1 = o objetivo de nível de serviço está ativado.<br /><br /> 2 = o objetivo de nível de serviço está desativado.|  
|state_desc|**nvarchar**|Descrição do objetivo de nível de serviço.|  
|metadata_version|**decimal**|Versão do objetivo de nível de serviço.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
