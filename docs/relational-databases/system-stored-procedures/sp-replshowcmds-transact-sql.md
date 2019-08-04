---
title: sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96a32ea04fc53f1a0bf3a842a5e68cde5586ac29
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770878"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna os comandos para transações marcadas para replicação em formato legível. **sp_replshowcmds** pode ser executado somente quando as conexões de cliente (incluindo a conexão atual) não estão lendo transações replicadas do log. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @maxtrans = ] maxtrans`É o número de transações sobre as quais retornar informações. *maxtrans* é **int**, com um padrão de **1**, que especifica o número máximo de transações com replicação pendente para o qual **sp_replshowcmds** retorna informações.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_replshowcmds** é um procedimento de diagnóstico que retorna informações sobre o banco de dados de publicação do qual ele é executado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Número de sequência do comando.|  
|**originator_id**|**int**|ID do originador de comando, sempre **0**.|  
|**publisher_database_id**|**int**|ID do banco de dados do Publicador, sempre **0**.|  
|**article_id**|**int**|ID do artigo.|  
|**type**|**int**|Tipo de comando.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="remarks"></a>Comentários  
 **sp_replshowcmds** é usado na replicação transacional.  
  
 Usando o **sp_replshowcmds**, você pode exibir as transações que não estão distribuídas atualmente (as transações restantes no log de transações que não foram enviadas para o distribuidor).  
  
 Os clientes que executam o **sp_replshowcmds** e o **sp_replcmds** no mesmo banco de dados recebem o erro 18752.  
  
 Para evitar esse erro, o primeiro cliente deve se desconectar ou a função do cliente como um leitor de log deve ser liberada executando **sp_replflush**. Depois que todos os clientes tiverem se desconectado do leitor de log, o **sp_replshowcmds** poderá ser executado com êxito.  
  
> [!NOTE]  
>  **sp_replshowcmds** deve ser executado somente para solucionar problemas com a replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_replshowcmds**.  
  
## <a name="see-also"></a>Consulte também  
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
