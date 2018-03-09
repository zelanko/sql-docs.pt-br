---
title: sp_replcmds (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords: sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 279d002e0a088386440cd978410476dee8def3ac
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os comandos para transações marcadas para replicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  O **sp_replcmds** procedimento deve ser executado apenas para solucionar problemas de replicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@maxtrans=**] *maxtrans*  
 É o número de transações para retornar informações sobre. *maxtrans* é **int**, com um padrão de **1**, que especifica a próxima transação à espera de distribuição.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id do artigo**|**int**|A ID do artigo.|  
|**partial_command**|**bit**|Indica se este é um comando parcial ou não.|  
|**command**|**varbinary(1024)**|O valor do comando.|  
|**Xactid**|**binary(10)**|ID da transação.|  
|**xact_seqno**|**varbinary (16)**|O número de sequência da transação.|  
|**publication_id**|**int**|A ID da publicação.|  
|**command_id**|**int**|ID do comando na [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
|**command_type**|**int**|Tipo de comando.|  
|**originator_srvname**|**sysname**|Servidor onde a transação originou.|  
|**originator_db**|**sysname**|Banco de dados onde a transação originou.|  
|**pkHash**|**int**|Somente para uso interno.|  
|**originator_publication_id**|**int**|ID da publicação de origem da transação.|  
|**originator_db_version**|**int**|Versão do banco de dados onde a transação originou.|  
|**originator_lsn**|**varbinary (16)**|Identifica o LSN (número de sequência de log) para o comando na publicação de origem.|  
  
## <a name="remarks"></a>Comentários  
 **sp_replcmds** é usado pelo processo do leitor de log na replicação transacional.  
  
 Replicação trata o primeiro cliente que executa o **sp_replcmds** dentro de um determinado banco de dados como o leitor de log.  
  
 Esse procedimento pode gerar comandos para tabelas qualificadas pelo proprietário ou pode não qualificar o nome da tabela (o padrão). A adição de nomes das tabelas qualificados permite a replicação de dados de tabelas de propriedade de um usuário específico em um banco de dados para tabelas de propriedade do mesmo usuário em outro banco de dados.  
  
> [!NOTE]  
>  Como o nome da tabela no banco de dados de origem é qualificado pelo nome do proprietário, o proprietário da tabela no banco de dados de destino deve ter o mesmo nome do proprietário.  
  
 Os clientes que tentam executar **sp_replcmds** dentro do mesmo banco de dados recebem erro 18752 até que o primeiro cliente se desconecta. Depois que o primeiro cliente se desconecta, outro cliente pode executar **sp_replcmds**, e se torna o novo leitor de log.  
  
 Um aviso mensagem 18759 será adicionada para ambos os [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] do log de aplicativo do Windows se **sp_replcmds** não consegue replicar um comando de texto como o ponteiro de texto não foi recuperar na mesma transação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_replcmds**.  
  
## <a name="see-also"></a>Consulte também  
 [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
