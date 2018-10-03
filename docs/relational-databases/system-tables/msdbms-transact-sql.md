---
title: MSdbms (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSdbms_TSQL
- MSdbms
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms system table
ms.assetid: 2be631bf-de09-4e7a-9ccb-d6c37b81c237
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f8d3ff30aaf780fbbda4058d8c3ca0815b2120c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651024"
---
# <a name="msdbms-transact-sql"></a>MSdbms (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdbms** tabela contém uma lista mestre de todas as versões dos sistemas de gerenciamento de banco de dados (DBMS) com suporte para replicação de banco de dados heterogênea. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**dbms_id**|**int**|Identifica cada DBMS exclusivo e versão.|  
|**DBMS**|**sysname**|O nome do DBMS.<br /><br /> MSSQLSERVER<br /><br /> DB2<br /><br /> ORACLE<br /><br /> SYBASE|  
|**version**|**varchar(10)**|A versão do DBMS.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
