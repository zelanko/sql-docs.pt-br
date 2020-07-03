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
ms.openlocfilehash: 16da7db2dcf42ebfa00d634814f27839a3988a71
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889191"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O modo de exibição de **MSdatatype_mappings** mapeia SQL Server tipos de dados para tipos de dados usados por DBMS (sistemas de gerenciamento de banco de dados) não SQL Server. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|É o nome do DBMS. Abaixo estão os possíveis valores e suas descrições.<br /><br /> **MSSQLSERVER**: o destino é um banco de dados SQL Server.<br />**Oracle**: o destino é um banco de dados Oracle.<br />**DB2**: o destino é um banco de dados IBM DB2.<br />**Sybase**: o destino é um banco de dados Sybase.|  
|**sql_type**|**nvarchar(128)**|É o tipo de dados SQL Server.|  
|**dest_type**|**nvarchar(128)**|É o nome do tipo de dados não SQL Server.|  
|**dest_prec**|**bigint**|É a precisão do tipo de dados não SQL Server.|  
|**dest_create_params**|**int**|Somente para uso interno.|  
|**dest_nullable**|**bit**|Se o tipo de dados não SQL Server oferecer suporte a um valor NULL.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
