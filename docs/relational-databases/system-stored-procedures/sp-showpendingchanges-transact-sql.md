---
title: sp_showpendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9ddc7ad352b16b32cbb1a090e3ed2976cf161599
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633973"
---
# <a name="sp_showpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna um conjunto de resultados que mostra as alterações esperando para ser replicadas. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  Este procedimento fornece uma aproximação do número de alterações e as linhas que são envolvidas nessas alterações. Por exemplo, o procedimento recupera informações do Publicador ou Assinante, mas não de ambos ao mesmo tempo. As informações armazenadas no outro nó podem resultar em um conjunto menor de alterações a sincronizar do que o estimado pelo procedimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @destination_server = ] 'destination_server'`É o nome do servidor onde as alterações replicadas são aplicadas. *destination_server* é **sysname**, com o valor padrão de NULL.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um valor padrão de NULL. Quando a *publicação* é especificada, os resultados são limitados apenas à publicação especificada.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, com um valor padrão de NULL. Quando o *artigo* é especificado, os resultados são limitados apenas ao artigo especificado.  
  
`[ @show_rows = ] 'show_rows'`Especifica se o conjunto de resultados contém informações mais específicas sobre as alterações pendentes, com um valor padrão de **0**. Se um valor de **1** for especificado, o conjunto de resultados conterá as colunas is_delete e ROWGUID.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|O nome do servidor para o qual as alterações estão sendo replicadas.|  
|pub_name|**sysname**|O nome da publicação.|  
|destination_db_name|**sysname**|O nome do banco de dados para o qual as alterações estão sendo replicadas.|  
|is_dest_subscriber|**bit**|Indica que as alterações estão sendo replicadas para um Assinante. Um valor de **1** indica que as alterações estão sendo replicadas para um assinante. **0** significa que as alterações estão sendo replicadas para um Publicador.|  
|article_name|**sysname**|O nome do artigo para a tabela onde as alterações foram originadas.|  
|pending_deletes|**int**|O número de exclusões esperando para serem replicadas.|  
|pending_ins_and_upd|**int**|O número de inserções e atualizações esperando para serem replicadas.|  
|is_delete|**bit**|Indica se a alteração pendente é uma exclusão. Um valor de **1** indica que a alteração é uma exclusão. Requer um valor de **1** para @show_rows .|  
|rowguid|**uniqueidentifier**|A GUID que identifica a linha que foi alterada. Requer um valor de **1** para @show_rows .|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_showpendingchanges é usado em replicação de mesclagem.  
  
 sp_showpendingchanges é usado na solução de problemas de replicação de mesclagem.  
  
 O resultado de sp_showpendingchanges não inclui linhas em geração 0.  
  
 Quando um artigo especificado para o *artigo* não pertence à publicação especificada para *publicação,* uma contagem de 0 é retornada para pending_deletes e pending_ins_and_upd.  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin ou função de banco de dados db_owner podem executar sp_showpendingchanges.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
