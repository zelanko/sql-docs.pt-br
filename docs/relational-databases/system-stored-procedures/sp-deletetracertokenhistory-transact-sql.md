---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a7f70f5cd56867add98150d471d61cbc70faad0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111920"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Remove registros de token de rastreamento a [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) e [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) tabelas do sistema. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>Argumentos

`@publication= 'publication'`  
É o nome da publicação na qual o token de rastreamento foi inserido. O tipo de dados é **sysname**. Este parâmetro é obrigatório.

`[ @tracer_id= ] tracer_id`  
É a ID do token de rastreamento a ser excluído. O tipo de dados é **int**. O valor padrão é *null*. Se *nulo*, todos os tokens de rastreamento que pertencem à publicação serão excluídos.

`[ @cutoff_date= ] cutoff_date`  
Tokens de rastreamento inseridos na publicação antes dessa data serão excluídos. O tipo de dados é **datetime**. O valor padrão é *null*.

`[ @publisher= ] 'publisher'`  
É o nome do Publicador. O tipo de dados é **sysname**. O valor padrão é *null*.

> [!NOTE]
> Esse parâmetro só deve ser especificado para não - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores ou ao executar o procedimento armazenado do distribuidor.

`[ @publisher_db= ] 'publisher_db'`  
É o nome do banco de dados de publicação. O tipo de dados é **sysname**. O valor padrão é NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.

> [!NOTE]
> Esse parâmetro deve ser especificado ao executar o procedimento armazenado do distribuidor.

## <a name="return-code-values"></a>Valores do código de retorno

**0** (êxito) ou **1** (falha)

## <a name="remarks"></a>Comentários

**sp_deletetracertokenhistory** é usado em replicação transacional.  

Um erro ocorrerá se você especificar ambos os parâmetros *tracer_id* e *cutoff_date*.

Se você não executa **sp_deletetracertokenhistory** para excluir os metadados de token de rastreamento, as informações serão excluídas quando ocorre a limpeza de histórico agendada regularmente.

IDs de token de rastreamento podem ser determinadas executando [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ou consultando os [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabela do sistema.

## <a name="permissions"></a>Permissões

Somente a equipe a seguir têm autoridade para executar **sp_deletetracertokenhistory**:

- Os membros de **replmonitor** funções, no banco de dados de distribuição
- Os membros de **sysadmin** função de servidor fixa.
- Os membros de **db_owner** função de banco de dados fixa, no banco de dados de publicação.
- O **db_owner** do banco de dados fixado.

## <a name="see-also"></a>Consulte também

[Medir a latência e validar as conexões para a replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
