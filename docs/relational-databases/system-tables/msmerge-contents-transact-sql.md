---
title: MSmerge_contents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48c2320fa26b86f9ee221a65e3a81eb809021cf4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="msmergecontents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_contents** tabela contém uma linha para cada linha modificada no banco de dados atual desde que foi publicado. Essa tabela é usada pelo processo de mesclagem para determinar as linhas que foram alteradas. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**Int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**Geração**|**bigint**|A geração da linha identificada pelo **tablenick** e **rowguid**.|  
|**partchangegen**|**bigint**|A geração associada à última alteração de dados que poderia ter sido alterada se a linha pertencesse a uma publicação filtrada.|  
|**linhagem**|**varbinary(501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das alterações nessa linha.|  
|**colvl**|**varbinary(7489)**|As informações de versão da coluna.|  
|**Marcador**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifica a linha pai de alto nível em **MSmerge_contents** (por **rowguid**) para cada linha filho correspondente em um registro lógico.|  
|**logical_record_lineage**|**varbinary(501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das alterações na linha pai de alto nível em um registro lógico. Para todas as linhas filho em um registro lógico, esse valor é NULL.|  
|**logical_relation_change_gen**|**bigint**|O valor de geração associado à última alteração que causou realinhamento no registro lógico, onde uma linha existente foi movida para dentro ou fora de um registro lógico.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
