---
title: MSdbms_datatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype
- MSdbms_datatype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype system table
ms.assetid: 606168cc-79a8-442f-ab43-936f8f884d72
author: stevestein
ms.author: sstein
ms.openlocfilehash: 301aa5af9aa34031f381235341f1e7d461675432
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907508"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSdbms_datatype** contém a lista completa de tipos de dados nativos em cada DBMS (sistema de gerenciamento de banco de dado) com suporte usado como Publicador ou Assinante na replicação de banco de dados heterogêneo. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifica cada tipo de dados exclusivo.|  
|**dbms_id**|**int**|Identifica o DBMS ao qual o tipo pertence.|  
|**tipo**|**sysname**|Nome do tipo de dados (nativo).|  
|**createparams**|**int**|Bitmap que descreve qual a combinação de comprimento, precisão e escala é aplicável a cada tipo de dados, incluindo:<br /><br /> **0x1** = precisão.<br /><br /> **0x2** = escala.<br /><br /> **0x4** = comprimento.|  
  
## <a name="remarks"></a>Comentários  
 Essa tabela contém entradas para tipos de dados SQL Server porque uma instância do SQL Server pode assinar um banco de dados não SQL Server e publicar em um Assinante não SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
