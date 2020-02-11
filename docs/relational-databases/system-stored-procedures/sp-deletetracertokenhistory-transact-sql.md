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
ms.openlocfilehash: cf591964e5dfef0536c79b0b35e5918d4f46d972
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771138"
---
# <a name="sp_deletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Remove registros de token de rastreamento das [MStracer_tokens &#40;Transact-sql&#41;](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) e MStracer_history &#40;tabelas do sistema [de&#41;Transact-SQL](../../relational-databases/system-tables/mstracer-history-transact-sql.md) . Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação, ou no Distribuidor, no banco de dados de distribuição.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

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
É o nome da publicação na qual o token de rastreamento foi inserido. O tipo de dados é **sysname**. Este parâmetro é necessário.

`[ @tracer_id= ] tracer_id`  
É a ID do token de rastreamento a ser excluído. O tipo de dados é **int**. O valor padrão é *NULL*. Se for *NULL*, todos os tokens de rastreamento que pertencem à publicação serão excluídos.

`[ @cutoff_date= ] cutoff_date`  
Tokens de rastreamento inseridos na publicação antes dessa data são excluídos. O tipo de dados é **DateTime**. O valor padrão é *NULL*.

`[ @publisher= ] 'publisher'`  
É o nome do Publicador. O tipo de dados é **sysname**. O valor padrão é *NULL*.

> [!NOTE]
> Esse parâmetro só deve ser especificado para não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores ou ao executar o procedimento armazenado do distribuidor.

`[ @publisher_db= ] 'publisher_db'`  
É o nome do banco de dados de publicação. O tipo de dados é **sysname**. O valor padrão é NULL. Esse parâmetro será ignorado se o procedimento armazenado for executado no Publicador.

> [!NOTE]
> Esse parâmetro deve ser especificado ao executar o procedimento armazenado do distribuidor.

## <a name="return-code-values"></a>Valores do código de retorno

**0** (êxito) ou **1** (falha)

## <a name="remarks"></a>Comentários

**sp_deletetracertokenhistory** é usado na replicação transacional.  

Ocorrerá um erro se você especificar os parâmetros *tracer_id* e *cutoff_date*.

Se você não executar **sp_deletetracertokenhistory** para excluir os metadados do token de rastreamento, as informações serão excluídas quando ocorrer a limpeza do histórico agendado regularmente.

As IDs de token de rastreamento podem ser determinadas executando [sp_helptracertokens &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) ou consultando a tabela do sistema [&#40;MStracer_tokens&#41;Transact-SQL](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) .

## <a name="permissions"></a>Permissões

Somente a equipe a seguir tem autoridade para executar **sp_deletetracertokenhistory**:

- Membros das funções **replmonitor** , no banco de dados de distribuição
- Membros da função de servidor fixa **sysadmin** .
- Os membros da função de banco de dados fixa **db_owner** no banco de dados de publicação.
- O **db_owner** do banco de dados fixo.

## <a name="see-also"></a>Consulte Também

[Medir a latência e validar conexões para replicação transacional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[&#41;&#40;Transact-SQL de sp_helptracertokenhistory](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
