---
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b9e2a370c9acc9c22dac7e5e60ceb10e08e46ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68137624"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre todas as solicitações de status recebidas pelos participantes em uma topologia de replicação ponto a ponto, em que essas solicitações foram iniciadas executando [sp_requestpeerresponse &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) em qualquer banco de dados publicado na topologia. Esse procedimento armazenado é executado no banco de dados de publicação em um Publicador que participa de uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação em uma topologia ponto a ponto para a qual as solicitações de status foram enviadas. a *publicação* é **sysname**, sem padrão.  
  
`[ @description = ] 'description'`Valor que pode ser usado para identificar solicitações de status individuais, o que permite filtrar respostas retornadas com base nas informações definidas pelo usuário fornecidas ao chamar [sp_requestpeerresponse &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). a *Descrição* é **nvarchar (4000)**, com um padrão **%** de. Por padrão, todas as solicitações de status para a publicação são retornadas. Esse parâmetro é usado para retornar apenas solicitações de status com uma descrição correspondente ao valor fornecido na *Descrição*, em que as cadeias de caracteres são correspondidas usando uma cláusula [like &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md) .  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|Identifica uma solicitação.|  
|**documento**|**sysname**|Nome da publicação para a qual a solicitação de status foi enviada.|  
|**sent_date**|**datetime**|Data e hora de envio da solicitação de status.|  
|**ndescrição**|**nvarchar(4000)**|Informações definidas pelo usuário que podem ser usadas para identificar solicitações de status individuais.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helppeerrequests** é usado em replicação transacional ponto a ponto.  
  
 **sp_helppeerrequests** é usado ao restaurar um banco de dados publicado em uma topologia ponto a ponto.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_deletepeerrequesthistory](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppeerresponses](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
