---
title: sp_helpmergeconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1de46c12b0e05b592489e557a80138996ad9767f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528788"
---
# <a name="sphelpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as linhas na tabela de conflitos especificada. Esse procedimento armazenado é executado no computador onde a tabela de conflitos é armazenada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, com um padrão de **%**. Se a publicação for especificada, serão retornados todos os conflitos qualificados pela publicação. Por exemplo, se o **MSmerge_conflict_Customers** tabela tem linhas de conflito para o **WA** e o **autoridade de certificação** publicações, passando um nome de publicação **autoridade de certificação**  recuperará os conflitos que pertencem à **autoridade de certificação** publicação.  
  
`[ @conflict_table = ] 'conflict_table'` É o nome da tabela de conflitos. *conflict_table* está **sysname**, sem padrão. Na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, tabelas de conflitos são nomeadas usando nomes de formato com **MSmerge_conflict\__publicação\_artigo_**, com uma tabela para cada artigo publicado.  
  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicador. *publisher_db* é **sysname**, com um padrão NULL.  
  
`[ @logical_record_conflicts = ] logical_record_conflicts` Indica se o conjunto de resultados contém informações sobre conflitos de registro lógico. *logical_record_conflicts* está **int**, com um valor padrão de 0. **1** significa que as informações de conflitos de registro lógico são retornadas.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpmergeconflictrows** retorna um conjunto de resultados consistindo da estrutura da tabela base e essas colunas adicionais.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|Origem do conflito.|  
|**conflict_type**|**int**|Código que indica o tipo de conflito:<br /><br /> **1** = conflito de atualização: O conflito é detectado no nível de linha.<br /><br /> **2** = conflito de atualização de coluna: O conflito é detectado no nível de coluna.<br /><br /> **3** = conflito de atualização do Wins de exclusão: A exclusão ganha o conflito.<br /><br /> **4** = conflito de exclusão do Wins de atualização: O rowguid excluído que perde o conflito é registrado nessa tabela.<br /><br /> **5** = Falha na inserção do carregamento: A inserção do assinante não puderam ser aplicada no publicador.<br /><br /> **6** = Falha na inserção do download: A inserção do publicador não pôde ser aplicada no assinante.<br /><br /> **7** = Falha na exclusão do carregamento: A exclusão no assinante não pôde ser carregada no publicador.<br /><br /> **8** = Falha na exclusão do download: A exclusão no publicador não pôde ser baixada no assinante.<br /><br /> **9** = Falha na atualização do carregamento: A atualização do assinante não puderam ser aplicada no publicador.<br /><br /> **10** = Falha na atualização do download: A atualização no publicador não pôde ser aplicada ao assinante.<br /><br /> **12** = atualização de registro lógico vence exclusão: O registro lógico excluído que perde o conflito é registrado nessa tabela.<br /><br /> **13** = atualização de inserção de conflito de registro lógico: Inserir um registro lógico está em conflito com uma atualização.<br /><br /> **14** = conflito de atualização do Wins de exclusão de registro lógico: O registro lógico atualizado que perde o conflito é registrado nessa tabela.|  
|**reason_code**|**int**|Código de erro que pode ser sensível ao contexto.|  
|**reason_text**|**varchar(720)**|Descrição de erro que pode ser sensível ao contexto.|  
|**pubid**|**uniqueidentifier**|Identificador da publicação.|  
|**MSrepl_create_time**|**datetime**|Hora em que as informações de conflitos foram adicionadas.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergeconflictrows** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa, o **db_owner** função de banco de dados fixa e a **replmonitor** no banco de dados de distribuição podem executar **sp_helpmergeconflictrows**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir informações sobre conflitos para publicações de mesclagem &#40;programação de Transact-SQL de replicação&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
