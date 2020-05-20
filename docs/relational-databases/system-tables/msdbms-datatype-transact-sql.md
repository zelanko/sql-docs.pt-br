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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 299272377d8bbc55781d671a94240d6c309877ec
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832320"
---
# <a name="msdbms_datatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSdbms_datatype** contém a lista completa de tipos de dados nativos em cada DBMS (sistema de gerenciamento de banco de dado) com suporte usado como Publicador ou Assinante na replicação de banco de dados heterogêneo. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifica cada tipo de dados exclusivo.|  
|**dbms_id**|**int**|Identifica o DBMS ao qual o tipo pertence.|  
|**tipo**|**sysname**|Nome do tipo de dados (nativo).|  
|**createparams**|**int**|Bitmap que descreve qual a combinação de comprimento, precisão e escala é aplicável a cada tipo de dados, incluindo:<br /><br /> **0x1** = precisão.<br /><br /> **0x2** = escala.<br /><br /> **0x4** = comprimento.|  
  
## <a name="remarks"></a>Comentários  
 Essa tabela contém entradas para tipos de dados SQL Server porque uma instância do SQL Server pode assinar um banco de dados não SQL Server e publicar em um Assinante não SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
