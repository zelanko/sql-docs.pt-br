---
title: sys.database_automatic_tuning_options (Transact-SQL) | Microsoft Docs
description: "Saiba como exibir as opções de ajuste automático em um banco de dados SQL"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs: TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: "24"
author: jovanpop-msft
ms.author: jovanpop
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44cc105b0edfa6c71b114800ce5be7538f9393a1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys\_automático\_tuning_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Retorna as opções de ajuste automático do banco de dados.  

|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (128)**|O nome da opção de ajuste automático. Consulte [ALTER DATABASE SET AUTOMATIC_TUNING &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) para as opções disponíveis.|  
|**desired_state**|**smallint**|Indica o modo de operação desejado para a opção de ajuste automático, explicitamente definido pelo usuário.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar (60)**|Descrição textual do modo de operação desejado da opção de ajuste automático.<br />OFF<br />ON|  
|**actual_state**|**smallint**|Indica o modo de operação da opção de ajuste automático.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar (60)**|Descrição textual do modo de operação real da opção de ajuste automático.<br />OFF<br />ON|  
|**motivo**|**smallint**|Indica por que os estados desejados e reais são diferentes.<br />2 = DESABILITADO<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar (60)**|Descrição textual do motivo por que os estados desejados e reais são diferentes.<br />DESABILITADO = opção está desabilitada pelo sistema<br />QUERY_STORE_OFF = repositório de consultas está desativado<br />QUERY_STORE_READ_ONLY = Query Store está no modo somente leitura<br />NOT_SUPPORTED = disponível apenas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition| 
  
## <a name="permissions"></a>Permissões  
 Requer o `VIEW DATABASE STATE` permissão.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [database_query_store_options &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
