---
title: IHpublishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
author: stevestein
ms.author: sstein
ms.openlocfilehash: 92f0c507b15e5a582fbcc1a12b1bccd77d08f7de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990162"
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublishers** tabela do sistema contém uma linha para cada publicador não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identifica um editor não SQL Server.|  
|**fornecedor**|**sysname**|O nome do fornecedor para o banco de dados do SQL Server.|  
|**publisher_guid**|**uniqueidentifier**|Um GUID que identifica o Editor não SQL Server.|  
|**flush_request_time**|**datetime**|Indica a data de hora de ocorrência da última alteração nos metadados do artigo que solicitaram que o Log Reader Agent atualizasse seu cache de metadados.|  
|**version**|**sysname**|Uma cadeia de caracteres de texto que caracteriza a versão do publicador não SQL Server.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
