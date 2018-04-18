---
title: Stretch Database (Transact-SQL) de procedimentos armazenados estendido | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68ef74d212ac3ad0e4ec7da5866390df8c8bce7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>O Stretch Database (Transact-SQL) de procedimentos armazenados estendido
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Esta seção descreve os procedimentos armazenados estendidos que estão relacionados ao Stretch Database.  
  
## <a name="in-this-section"></a>Nesta seção  
[sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) remove a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto do Azure.

[sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) obtém o número de horas de dados migrados que o SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se a restauração é necessária.
  
 [sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Reconcilia a ID do lote armazenada na tabela do SQL Server habilitados para ampliação para os dados migrados mais recentemente com a ID de lote armazenada na tabela remota do Azure. 
 
[sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) reconcilia as colunas na tabela do Azure remota para as colunas da a tabela do SQL Server habilitado para Stretch.
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) filas de uma tarefa de esquema para reconciliar índices na tabela remota.
 
 [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) Especifica se as consultas em relação a ampliação habilitada banco de dados atual e suas tabelas retornam dados locais e remotos (o padrão) ou apenas os dados locais.
 
 [sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) define o número de horas de dados migrados que o SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se a restauração é necessária.
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) testa a conexão do SQL Server para o servidor remoto do Azure e reporta problemas que podem impedir que a migração de dados.
 
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
