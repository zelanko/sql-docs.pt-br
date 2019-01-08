---
title: MSdatatype_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5af1233e81c996e98287a637e01ad1d249671303
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785088"
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdatatype_mappings** exibição mapeia tipos de dados do SQL Server para tipos de dados usados pelos sistemas de gerenciamento de banco de dados do SQL Server (DBMS). Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|É o nome do DBMS. Abaixo estão os valores possíveis e suas descrições.<br /><br /> **MSSQLSERVER**: O destino é um banco de dados do SQL Server.<br />**ORACLE**: O destino é um banco de dados Oracle.<br />**DB2**: O destino é um banco de dados IBM DB2.<br />**SYBASE**: O destino é um banco de dados Sybase.|  
|**sql_type**|**nvarchar(128)**|É o tipo de dados do SQL Server.|  
|**dest_type**|**nvarchar(128)**|É o nome do tipo de dados não SQL Server.|  
|**dest_prec**|**bigint**|É a precisão do tipo de dados não SQL Server.|  
|**dest_create_params**|**int**|Somente para uso interno.|  
|**dest_nullable**|**bit**|É se o tipo de dados não SQL Server dá suporte a um valor NULL.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
