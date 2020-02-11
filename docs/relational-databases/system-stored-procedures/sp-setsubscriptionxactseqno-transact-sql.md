---
title: sp_setsubscriptionxactseqno (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27a7f35a915e2bff62932124aef64984a63cbd0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68021078"
---
# <a name="sp_setsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado durante a solução de problemas para especificar a última transação entregue usando o LSN (número de sequência de log), permitindo que o Agente de Distribuição comece a entregar na próxima transação. Após a reinicialização, o Agente de Distribuição retorna transações maiores do que esta marca d' água (LSN) do cache do banco de dados de distribuição (msrepl_commands). Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura. Sem suporte para Assinantes não SQLServer.  
  
> [!CAUTION]  
>  O uso incorreto desse procedimento armazenado ou a especificação incorreta de um valor LSN pode fazer com que o Agente de Distribuição reverta as alterações que já tinham sido aplicadas no Assinante ou ignore todas as alterações restantes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão. Para um Publicador não SQL Server, *publisher_db* é o nome do banco de dados de distribuição.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão. Quando o Agente de Distribuição é compartilhado por mais de uma publicação, você deve especificar um valor de todos para *publicação*.  
  
`[ @xact_seqno = ] xact_seqno`É o LSN da próxima transação no distribuidor a ser aplicado ao Assinante. *xact_seqno* é **varbinary (16)**, sem padrão.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**ORIGINAL XACT_SEQNO**|**varbinary (16)**|É o LSN original da próxima transação a ser aplicada no Assinante.|  
|**UPDATED XACT_SEQNO**|**varbinary (16)**|É o LSN atualizado da próxima transação a ser aplicada no Assinante.|  
|**SUBSCRIPTION STREAM COUNT**|**int**|O número de fluxos de assinatura usado durante a última sincronização.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_setsubscriptionxactseqno** é usado na replicação transacional.  
  
 **sp_setsubscriptionxactseqno** não pode ser usada em uma topologia de replicação transacional ponto a ponto.  
  
 **sp_setsubscriptionxactseqno** pode ser usado para ignorar uma transação específica que está causando um erro quando se aplica ao Assinante. Quando houver uma falha e após o Agente de Distribuição parar, chame [sp_helpsubscriptionerrors &#40;&#41;do Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) no distribuidor para recuperar o valor de xact_seqno da transação com falha e, em seguida, chame **sp_setsubscriptionxactseqno**, passando esse valor para *xact_seqno*. Isso assegurará que somente os comandos após esse LSN sejam processados.  
  
 Especifique um valor de **0** para *xact_seqno* para entregar todos os comandos pendentes no banco de dados de distribuição para o Assinante.  
  
 **sp_setsubscriptionxactseqno** poderá falhar se o agente de distribuição usar fluxos de várias assinaturas.  
  
 Quando esse erro ocorre, você deve executar o Agente de Distribuição com um fluxo de uma única assinatura. Para obter mais informações, consulte [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_setsubscriptionxactseqno**.  
  
## <a name="see-more"></a>Ver mais

[Blog: como ignorar uma transação](https://repltalk.com/2019/05/28/how-to-skip-a-transaction/)  
