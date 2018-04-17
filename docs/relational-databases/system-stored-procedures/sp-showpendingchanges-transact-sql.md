---
title: sp_showpendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54a87a2162049fe6e3ec450a60836afffa406973
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spshowpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados que mostra as alterações esperando para ser replicadas. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @destination_server **=** ] **'***destination_server***'**  
 É o nome do servidor onde as alterações replicadas são aplicadas. *destination_server* é **sysname**, com o valor padrão de NULL.  
  
 [ @publication **=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um valor padrão de NULL. Quando *publicação* for especificado, resultados são limitados somente para a publicação especificada.  
  
 [ @article **=** ] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, com um valor padrão de NULL. Quando *artigo* for especificado, resultados são limitados somente para o artigo especificado.  
  
 [ @show_rows **=** ] *show_rows*  
 Especifica se o conjunto de resultados contém informações mais específicas sobre alterações pendentes, com um valor padrão de **0**. Se um valor de **1** for especificado, o conjunto de resultados contém as colunas is_delete e rowguid.  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|O nome do servidor para o qual as alterações estão sendo replicadas.|  
|pub_name|**sysname**|O nome da publicação.|  
|destination_db_name|**sysname**|O nome do banco de dados para o qual as alterações estão sendo replicadas.|  
|is_dest_subscriber|**bit**|Indica que as alterações estão sendo replicadas para um Assinante. Um valor de **1** indica que as alterações estão sendo replicadas para um assinante. **0** significa que as alterações estão sendo replicadas para um publicador.|  
|article_name|**sysname**|O nome do artigo para a tabela onde as alterações foram originadas.|  
|pending_deletes|**Int**|O número de exclusões esperando para serem replicadas.|  
|pending_ins_and_upd|**Int**|O número de inserções e atualizações esperando para serem replicadas.|  
|is_delete|**bit**|Indica se a alteração pendente é uma exclusão. Um valor de **1** indica que a alteração é uma exclusão. Requer um valor de **1** para @show_rows.|  
|rowguid|**uniqueidentifier**|A GUID que identifica a linha que foi alterada. Requer um valor de **1** para @show_rows.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_showpendingchanges é usado em replicação de mesclagem.  
  
 sp_showpendingchanges é usado na solução de problemas de replicação de mesclagem.  
  
 O resultado de sp_showpendingchanges não inclui linhas em geração 0.  
  
 Quando um artigo especificado para *artigo* não pertence à publicação especificada para *publicação,* uma contagem de 0 é retornada para for pending_deletes e pending_ins_and_upd.  
  
## <a name="permissions"></a>Permissões  
 Somente membros da função de servidor fixa sysadmin ou função de banco de dados db_owner podem executar sp_showpendingchanges.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
