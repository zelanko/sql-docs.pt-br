---
description: MSmerge_contents (Transact-SQL)
title: MSmerge_contents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 32041fc09c105509e050aa230ab05d1e8b3de6e6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547079"
---
# <a name="msmerge_contents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_contents** contém uma linha para cada linha modificada no banco de dados atual desde que foi publicada. Essa tabela é usada pelo processo de mesclagem para determinar as linhas que foram alteradas. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|O apelido da tabela publicada.|  
|**ROWGUID**|**uniqueidentifier**|O identificador para a linha determinada.|  
|**geração**|**bigint**|A geração da linha identificada pelo **tablenick** e **ROWGUID**.|  
|**partchangegen**|**bigint**|A geração associada à última alteração de dados que poderia ter sido alterada se a linha pertencesse a uma publicação filtrada.|  
|**linhagem**|**varbinary (501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das alterações nessa linha.|  
|**colvl**|**varbinary (7489)**|As informações de versão da coluna.|  
|**marcador**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifica a linha pai de nível superior em **MSmerge_contents** (por **ROWGUID**) para cada linha filho correspondente em um registro lógico.|  
|**logical_record_lineage**|**varbinary (501)**|O apelido do Assinante, pares de números de versão que são usados para manter um histórico das alterações na linha pai de alto nível em um registro lógico. Para todas as linhas filho em um registro lógico, esse valor é NULL.|  
|**logical_relation_change_gen**|**bigint**|O valor de geração associado à última alteração que causou realinhamento no registro lógico, onde uma linha existente foi movida para dentro ou fora de um registro lógico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
