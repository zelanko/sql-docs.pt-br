---
title: sp_repldone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cd38269fabba59d257e41141141764b6d4919d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771111"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Atualiza o registro que identifica a última transação distribuída do servidor. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!CAUTION]  
>  Se você executar o **sp_repldone** manualmente, poderá invalidar a ordem e a consistência das transações entregues. **sp_repldone** só deve ser usado para solucionar problemas de replicação, conforme indicado por um profissional de suporte de replicação experiente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @xactid = ] xactid`É o LSN (número de sequência de log) do primeiro registro da última transação distribuída do servidor. *xactid* é **binary (10)** , sem padrão.  
  
`[ @xact_seqno = ] xact_seqno`É o LSN do último registro para a última transação distribuída do servidor. *xact_seqno* é **binary (10)** , sem padrão.  
  
`[ @numtrans = ] numtrans`É o número de transações distribuídas. *numtrans* é **int**, sem padrão.  
  
`[ @time = ] time`É o número de milissegundos, se fornecido, necessário para distribuir o último lote de transações. o *tempo* é **int**, sem padrão.  
  
`[ @reset = ] reset`É o status de redefinição. *Reset* é **int**, sem padrão. Se **1**, todas as transações replicadas no log serão marcadas como distribuídas. Se for **0**, o log de transações será redefinido para a primeira transação replicada e nenhuma das transações replicadas será marcada como distribuída. *Reset* é válido somente quando *xactid* e *xact_seqno* são nulos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_repldone** é usado na replicação transacional.  
  
 **sp_repldone** é usado pelo processo de leitor de log para controlar quais transações foram distribuídas.  
  
 Com o **sp_repldone**, você pode informar manualmente ao servidor que uma transação foi replicada (enviada para o distribuidor). Ele também permite alterar a transação marcada como a próxima a ser replicada. Você pode avançar ou retroceder na lista de transações replicadas. (Todas as transações menores ou iguais àquela transação serão marcadas como distribuídas.)  
  
 Os parâmetros necessários *xactid* e *xact_seqno* podem ser obtidos usando **sp_repltrans** ou **sp_replcmds**.  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_repldone**.  
  
## <a name="examples"></a>Exemplos  
 Quando *xactid* é nulo, *xact_seqno* é nulo e *Reset* é **1**, todas as transações replicadas no log são marcadas como distribuídas. Isso é útil quando há transações replicadas no log de transações que não são mais válidas e você quer truncar o log, por exemplo:  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  Esse procedimento pode ser usado em situações emergenciais para permitir o truncamento do log de transações quando houver replicação pendente de transações.  
  
## <a name="see-also"></a>Consulte também  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
