---
title: sysarticleupdates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72316742aeb0674af092605609b870f0b412aded
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101614"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada artigo com suporte para assinaturas de atualização imediata. Essa tabela é armazenada no banco de dados replicado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A coluna de identidade, fornecendo um número de identificação exclusivo para o artigo.|  
|**pubid**|**int**|A ID da publicação à qual o artigo pertence.|  
|**sync_ins_proc**|**int**|A ID do procedimento armazenado que manuseia Inserir Transações de Sincronização.|  
|**sync_upd_proc**|**int**|A ID do procedimento armazenado que manuseia Atualizar Transações de Sincronização.|  
|**sync_del_proc**|**int**|A ID do procedimento armazenado que manuseia Excluir Transações de Sincronização.|  
|**autogen**|**bit**|Indica que são gerados procedimentos armazenados automaticamente:<br /><br /> **0** = false, não automático.<br /><br /> **1** = verdadeiro, automático.|  
|**sync_upd_trig**|**int**|A ID do gatilho de versão automática na tabela de artigo.|  
|**conflict_tableid**|**int**|A ID para a tabela de conflitos.|  
|**ins_conflict_proc**|**int**|A ID do procedimento usado para gravar o conflito para o **conflict_table**.|  
|**identity_support**|**bit**|Especifica se o tratamento do intervalo de identidade automático está habilitado quando a atualização na fila é usada. **0** significa que não há nenhuma identidade de intervalo de suporte.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
