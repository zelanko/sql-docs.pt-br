---
title: Stretch Database (Transact-SQL) de procedimentos armazenados estendido | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c2278b57646040fe70dd154ba0c0be7d02557ff7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416515"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database (Transact-SQL) de procedimentos armazenados estendido
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Esta seção descreve os procedimentos armazenados estendidos que estão relacionados ao Stretch Database.  
  
## <a name="in-this-section"></a>Nesta seção  
[sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) remove a conexão autenticada entre um banco de dados local habilitado para Stretch e o banco de dados remoto do Azure.

[sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) obtém o número de horas de dados migrados que o SQL Server retém em uma tabela de preparo para ajudar a garantir uma restauração completa do Azure banco de dados remoto, se a restauração é necessária.
  
 [sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) restaura a conexão autenticada entre o banco de dados local habilitado para Stretch e o banco de dados remoto.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Reconcilia o ID do lote armazenado na tabela do SQL Server habilitados para Stretch para os dados migrados recentemente com a ID de lote armazenada na tabela remota do Azure. 
 
[sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) reconcilia as colunas na tabela do Azure remota para as colunas na a tabela do SQL Server habilitados para Stretch.
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) enfileira uma tarefa de esquema para reconciliar índices na tabela remota.
 
 [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) Especifica se as consultas em relação a habilitados para Stretch banco de dados atual e suas tabelas retornam dados locais e remotos (o padrão) ou apenas os dados locais.
 
 [sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) define o número de horas de dados migrados que o SQL Server mantém em uma tabela de preparo para ajudar a garantir uma restauração completa do Azure banco de dados remoto, se a restauração é necessária.
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) testa a conexão do SQL Server para o servidor remoto do Azure e reporta problemas que podem impedir que a migração de dados.
 
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
