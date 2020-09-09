---
title: Procedimentos armazenados estendidos (Transact-SQL)
description: Saiba mais sobre os procedimentos armazenados estendidos que você pode usar ao trabalhar com bancos de dados habilitados para Stretch. Consulte como reconciliar colunas e executar outras tarefas.
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 975255806d8a031d1998d85778d89ccbf97a806f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545815"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database procedimentos armazenados estendidos (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

 Esta seção descreve os procedimentos armazenados estendidos relacionados a Stretch Database.  
  
## <a name="in-this-section"></a>Nesta seção  
[Sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) Remove a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto do Azure.

[Sys. sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Obtém o número de horas de dados migrados que SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se uma restauração for necessária.
  
 [Sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) Restaura a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Reconcilia a ID de lote armazenada na tabela SQL Server habilitada para Stretch para os dados migrados mais recentemente com a ID de lote armazenada na tabela remota do Azure. 
 
[Sys. sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) Reconcilia as colunas na tabela remota do Azure para as colunas na tabela de SQL Server habilitada para Stretch.
 
 [Sys. sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) Enfileira uma tarefa de esquema para reconciliar índices na tabela remota.
 
 [Sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) Especifica se as consultas em relação ao banco de dados atual habilitado para Stretch e suas tabelas retornam tanto local quanto remoto (o padrão) ou somente dados locais.
 
 [Sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) Define o número de horas de dados migrados que SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do banco de dados remoto do Azure, se uma restauração for necessária.
 
 [Sys. sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) Testa a conexão de SQL Server para o servidor remoto do Azure e relata problemas que podem impedir a migração de dados.
 
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
