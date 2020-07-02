---
title: MSrepl_queuedtraninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 762caa6d11de7917ab56192bcf8e6dc0ce80f043
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633399"
---
# <a name="msrepl_queuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A tabela de **MSreplication_queuedtraninfo** é usada pelo processo de replicação para armazenar informações sobre os comandos na fila emitidos por todas as assinaturas de atualização enfileiradas que estão usando a atualização em fila baseada em SQL. Essa tabela é armazenada no banco de dados de Assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**programa**|**sysname**|O nome do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**documento**|**sysname**|O nome da publicação.|  
|**transid**|**sysname**|A ID da transação na qual o comando enfileirado foi executado.|  
|**maxorderkey**|**bigint**|Interno-somente uso.|  
|**commandcount**|**bigint**|Interno-somente uso.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
