---
title: sys. sp_rda_reconcile_indexes (Transact-SQL) | Microsoft Docs
description: Saiba mais sobre sys. sp_rda_reconcile_indexes. Consulte como usar este procedimento armazenado Transact-SQL para enfileirar uma tarefa de esquema para reconciliar índices em uma tabela remota.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2d224f5ea2b20f684fdd9e484304639114fd2d2e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544663"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>sys. sp_rda_reconcile_indexes (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Enfileira uma tarefa de esquema para reconciliar índices na tabela remota. Depois que essa tarefa for concluída com êxito, a tabela remota terá os mesmos índices que existem na tabela local habilitada para Stretch.  
  
 Se houver outra tarefa na fila para reconciliar índices quando você chamar **sp_rda_reconcile_indexes**, esse procedimento armazenado não enfileirará uma tarefa duplicada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @objname =] *' objname '*  
 É o nome qualificado ou não qualificado da tabela habilitada para Stretch para a qual você deseja reconciliar índices. As aspas serão necessárias apenas se você especificar um objeto qualificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou >0 (falha)  
  
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
