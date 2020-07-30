---
title: sys. database_automatic_tuning_options (Transact-SQL) | Microsoft Docs
description: Saiba como exibir opções de ajuste automático em um banco de dados SQL. Consulte as permissões necessárias e exiba recursos adicionais disponíveis.
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4de2851505d7c5c240d792ecacdaa6bf3d1c6c3e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242946"
---
# <a name="sysdatabase_automatic_tuning_options-transact-sql"></a>tuning_options automático sys. Database \_ \_ (TRANSACT-SQL)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  Retorna as opções de ajuste automático para este banco de dados.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|O nome da opção de ajuste automático. Consulte [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) para obter as opções disponíveis.|  
|**desired_state**|**smallint**|Indica o modo de operação desejado para a opção de ajuste automático, definida explicitamente pelo usuário.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|Descrição textual do modo de operação desejado da opção de ajuste automático.<br />OFF<br />ATIVADO|  
|**actual_state**|**smallint**|Indica o modo de operação da opção de ajuste automático.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|Descrição textual do modo de operação real da opção de ajuste automático.<br />OFF<br />ATIVADO|  
|**motivo**|**smallint**|Indica por que os Estados reais e desejados são diferentes.<br />2 = DESABILITADO<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|Descrição textual do motivo pelo qual os Estados reais e desejados são diferentes.<br />DISABLED = a opção está desabilitada pelo sistema<br />QUERY_STORE_OFF = Repositório de Consultas está desativado<br />QUERY_STORE_READ_ONLY = Repositório de Consultas está no modo somente leitura<br />NOT_SUPPORTED = disponível somente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition| 
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys. database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
