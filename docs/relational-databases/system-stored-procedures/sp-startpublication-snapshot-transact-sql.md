---
description: sp_startpublication_snapshot (Transact-SQL)
title: sp_startpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_startpublication_snapshot
- sp_startpublication_snapshot_TSQL
helpviewer_keywords:
- sp_startpublication_snapshot
ms.assetid: 2cf568ee-0679-4d19-a394-27210bff61e5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6c43d44067e92a9ec606d08d9a458392d04c4e66
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551211"
---
# <a name="sp_startpublication_snapshot-transact-sql"></a>sp_startpublication_snapshot (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Usado para iniciar o trabalho Agente de Instantâneo que gera o instantâneo inicial para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_startpublication_snapshot [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'` É o nome de um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um valor padrão de NULL. Esse parâmetro não deve ser especificado para um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_startpublication_snapshot** é usado com todos os tipos de replicação.  
  
 Para um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador, esse procedimento armazenado é executado no distribuidor no banco de dados de distribuição.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_startpublication_snapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication_snapshot ](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication_snapshot ](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)  
  
  
