---
title: MSdbms_datatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 65110b04cec21d1b6d5b840fb9b3cc10d4f98e45
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807044"
---
# <a name="msdbmsdatatype-transact-sql"></a>MSdbms_datatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdbms_datatype** tabela contém a lista completa de tipos de dados nativos em cada sistema de gerenciamento de banco de dados com suporte (DBMS) usado como um publicador ou assinante em replicação de banco de dados heterogênea. Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**datatype_id**|**int**|Identifica cada tipo de dados exclusivo.|  
|**dbms_id**|**int**|Identifica o DBMS ao qual o tipo pertence.|  
|**type**|**sysname**|Nome do tipo de dados (nativo).|  
|**createparams**|**int**|Bitmap que descreve qual a combinação de comprimento, precisão e escala é aplicável a cada tipo de dados, incluindo:<br /><br /> **0x1** = precisão.<br /><br /> **0x2** = escala.<br /><br /> **0x4** = comprimento.|  
  
## <a name="remarks"></a>Comentários  
 Esta tabela contém entradas para tipos de dados do SQL Server porque uma instância do SQL Server pode se inscrever em um banco de dados do SQL Server e publicar para um assinante não SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
