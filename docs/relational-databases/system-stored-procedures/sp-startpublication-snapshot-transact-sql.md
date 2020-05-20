---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 70423377372a4ff41b5bd90487bd2080fec96edc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820295"
---
# <a name="sp_startpublication_snapshot-transact-sql"></a>sp_startpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para iniciar o trabalho Agente de Instantâneo que gera o instantâneo inicial para uma publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_startpublication_snapshot [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'`É o nome de um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um valor padrão de NULL. Esse parâmetro não deve ser especificado para um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_startpublication_snapshot** é usado com todos os tipos de replicação.  
  
 Para um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador, esse procedimento armazenado é executado no distribuidor no banco de dados de distribuição.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_startpublication_snapshot**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e aplicar o instantâneo inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication_snapshot](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)  
  
  
