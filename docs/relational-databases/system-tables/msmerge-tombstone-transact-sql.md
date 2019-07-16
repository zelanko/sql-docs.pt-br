---
title: MSmerge_tombstone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12caefe8b764090d46051912c876272c9efe86bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092665"
---
# <a name="msmergetombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_tombstone** tabela contém informações sobre linhas excluídas e permite que exclusões sejam propagadas para outros assinantes. Essa tabela é armazenada nos bancos de dados da publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|O identificador de linha.|  
|**tablenick**|**int**|O apelido da tabela.|  
|**type**|**tinyint**|O tipo de exclusão:<br /><br /> 1 = Exclusão de usuário.<br /><br /> 5 = A linha não mais pertence à partição filtrada.<br /><br /> 6 = Exclusão de sistema.|  
|**lineage**|**varbinary(249)**|Indica a versão do registro que foi excluído e quais atualizações eram conhecidas quando ele foi excluído. Permite regras de resolução consistente de um conflito quando um Assinante atualiza uma linha enquanto está sendo excluída em outro Assinante.|  
|**geração**|**int**|É atribuído quando uma linha é excluída. Se um assinante solicitar geração N, somente marcas para exclusão com geração > = N serão enviadas.|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifica o registro lógico ao qual uma linha excluída pertence.|  
|**logical_record_lineage**|**varbinary(501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das exclusões do registro lógico ao qual essa linha pertence.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
