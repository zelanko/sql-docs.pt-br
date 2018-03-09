---
title: sp_helpdistributor_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributor_properties_TSQL
- sp_helpdistributor_properties
helpviewer_keywords:
- sp_helpdistributor_properties
ms.assetid: ee267724-3244-49eb-84c9-f38dbefdd639
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5ce0b5b3e7e7bdb03fd0e36927a48c9dfcc8e7a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributorproperties-transact-sql"></a>sp_helpdistributor_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna propriedades do Distribuidor. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistributor_properties   
```  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**heartbeat_interval**|**int**|O número máximo de minutos que um agente pode prosseguir sem registrar uma mensagem de progresso.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistributor_properties** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, membros do **db_owner** ou **replmonitor** função de banco de dados fixa no banco de dados de distribuição e os usuários a lista de acesso à publicação (PAL) para uma publicação que usa esse distribuidor pode executar **sp_helpdistributor_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_changedistributor_property &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)  
  
  
