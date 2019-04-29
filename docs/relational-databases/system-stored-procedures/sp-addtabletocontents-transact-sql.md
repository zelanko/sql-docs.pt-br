---
title: sp_addtabletocontents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 991ee7139ae4a323a1d426d1882e4f6b3a4df871
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049714"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Insere referências em tabelas de controle de mesclagem para linhas em uma tabela de origem atualmente não incluída nas tabelas de controle. Use esta opção se você carregou em massa uma grande quantidade de dados usando **bcp**, que não será acionado gatilhos de controle de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_name = ] 'table_name'` É o nome da tabela. *table_name* está **sysname**, sem padrão.  
  
`[ @owner_name = ] 'owner_name'` É o nome do proprietário da tabela. *owner_name* está **sysname**, com um padrão NULL.  
  
`[ @filter_clause = ] 'filter_clause'` Especifica uma cláusula de filtro que controla quais linhas dos dados recém-carregados devem ser adicionadas às tabelas de controle de mesclagem. *filter_clause* está **nvarchar (4000)**, com um valor padrão de NULL. Se *filter_clause* é **nulo**, em massa de todas as linhas carregadas são adicionadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addtabletocontents** só é usado em replicação de mesclagem.  
  
 As linhas a *table_name* são referenciados por seus **rowguidcol** e as referências são adicionadas às tabelas de controle de mesclagem. **sp_addtabletocontents** deve ser usado após a cópia em massa dados em uma tabela é publicada usando replicação de mesclagem. Esse procedimento armazenado inicia o controle das linhas copiadas e assegura que as novas linhas sejam incluídas na próxima sincronização.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addtabletocontents**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
