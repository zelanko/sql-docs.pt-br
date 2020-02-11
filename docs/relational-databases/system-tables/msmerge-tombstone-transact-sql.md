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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68092665"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSmerge_tombstone** contém informações sobre linhas excluídas e permite que as exclusões sejam propagadas para outros assinantes. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|O identificador de linha.|  
|**tablenick**|**int**|O apelido da tabela.|  
|**tipo**|**tinyint**|O tipo de exclusão:<br /><br /> 1 = Exclusão de usuário.<br /><br /> 5 = A linha não mais pertence à partição filtrada.<br /><br /> 6 = Exclusão de sistema.|  
|**linhagem**|**varbinary (249)**|Indica a versão do registro que foi excluído e quais atualizações eram conhecidas quando ele foi excluído. Permite regras de resolução consistente de um conflito quando um Assinante atualiza uma linha enquanto está sendo excluída em outro Assinante.|  
|**geração**|**int**|É atribuído quando uma linha é excluída. Se um assinante solicitar a geração N, somente marcas para exclusão com >de geração = N serão enviadas.|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifica o registro lógico ao qual uma linha excluída pertence.|  
|**logical_record_lineage**|**Varbinary (501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das exclusões do registro lógico ao qual essa linha pertence.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
