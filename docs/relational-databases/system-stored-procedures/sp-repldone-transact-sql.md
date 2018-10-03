---
title: sp_repldone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2343d19e81d7d32ee0d4cf9ddf818b2f27a77191
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743448"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza o registro que identifica a última transação distribuída do servidor. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!CAUTION]  
>  Se você executar **sp_repldone** manualmente, você poderá invalidar a ordem e a consistência das transações entregues. **sp_repldone** só deve ser usado para solucionar problemas de replicação conforme direcionado por um profissional de suporte de replicação experiente.  
  
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
 [  **@xactid=**] *xactid*  
 É o número de sequência de log (LSN) do primeiro registro para a última transação distribuída do servidor. *Xactid* está **binário (10)**, sem padrão.  
  
 [  **@xact_seqno=**] *xact_seqno*  
 É o LSN do último registro para a última transação distribuída do servidor. *xact_seqno* está **binário (10)**, sem padrão.  
  
 [  **@numtrans=**] *numtrans*  
 É o número de transações distribuídas. *numtrans* está **int**, sem padrão.  
  
 [  **@time=**] *tempo*  
 É o número de milissegundos, se fornecido, necessário para distribuir o último lote de transações. *tempo* está **int**, sem padrão.  
  
 [  **@reset=**] *redefinir*  
 É o status de redefinição. *Redefinir* está **int**, sem padrão. Se **1**, replicados de todas as transações no log serão marcadas como distribuídas. Se **0**, o log de transações será redefinido para a primeira transação replicada e não há transações replicadas são marcadas como distribuídas. *Redefinir* é válido somente quando ambos *xactid* e *xact_seqno* são NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_repldone** é usado em replicação transacional.  
  
 **sp_repldone** é usado pelo processo do leitor de log para controlar quais transações foram distribuídas.  
  
 Com o **sp_repldone**, você pode informar manualmente ao servidor que uma transação tenha sido replicada (enviada ao distribuidor). Ele também permite alterar a transação marcada como a próxima a ser replicada. Você pode avançar ou retroceder na lista de transações replicadas. (Todas as transações menores ou iguais àquela transação serão marcadas como distribuídas.)  
  
 Os parâmetros necessários *xactid* e *xact_seqno* pode ser obtida usando **sp_repltrans** ou **sp_replcmds**.  
  
## <a name="permissions"></a>Permissões  
 Membros do **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_repldone**.  
  
## <a name="examples"></a>Exemplos  
 Quando *xactid* for NULL, *xact_seqno* for NULL, e *redefinir* é **1**, replicados de todas as transações no log serão marcadas como distribuídas. Isso é útil quando há transações replicadas no log de transações que não são mais válidas e você quer truncar o log, por exemplo:  
  
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
  
  
