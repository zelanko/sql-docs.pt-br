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
ms.openlocfilehash: b72a821c56f35e1ea7f3542b5746c234012c2da0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68137768"
---
# <a name="sp_helpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as linhas na tabela de conflitos especificada. Esse procedimento armazenado é executado no computador onde a tabela de conflitos é armazenada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão **%** de. Se a publicação for especificada, serão retornados todos os conflitos qualificados pela publicação. Por exemplo, se a tabela de **MSmerge_conflict_Customers** tiver linhas de conflito para as publicações **wa** e **CA** , a passagem de um nome de publicação **CA** recupera os conflitos que pertencem à publicação de **autoridade de certificação** .  
  
`[ @conflict_table = ] 'conflict_table'`É o nome da tabela de conflitos. *conflict_table* é **sysname**, sem padrão. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, as tabelas de conflitos são nomeadas usando o artigo nomes de formato com **MSmerge_conflict\_publicação\_**, com uma tabela para cada artigo publicado.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de NULL.  
  
`[ @logical_record_conflicts = ] logical_record_conflicts`Indica se o conjunto de resultados contém informações sobre conflitos de registro lógico. *logical_record_conflicts* é **int**, com um valor padrão de 0. **1** significa que as informações de conflito de registro lógico são retornadas.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpmergeconflictrows** retorna um conjunto de resultados que consiste na estrutura de tabela base e essas colunas adicionais.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|Origem do conflito.|  
|**conflict_type**|**int**|Código que indica o tipo de conflito:<br /><br /> **1** = conflito de atualização: o conflito é detectado no nível de linha.<br /><br /> **2** = conflito de atualização de coluna: o conflito detectado no nível de coluna.<br /><br /> **3** = atualizar conflito de exclusão de WINS: a exclusão vence o conflito.<br /><br /> **4** = atualizar o conflito de exclusão do WINS: o ROWGUID excluído que perde o conflito é registrado nesta tabela.<br /><br /> **5** = falha ao carregar inserção: não foi possível aplicar a inserção do Assinante no Publicador.<br /><br /> **6** = falha ao inserir download: não foi possível aplicar a inserção do Publicador no Assinante.<br /><br /> **7** = falha ao excluir upload: a exclusão no Assinante não pôde ser carregada no Publicador.<br /><br /> **8** = falha ao excluir download: a exclusão no Publicador não pôde ser baixada para o Assinante.<br /><br /> **9** = falha na atualização do carregamento: não foi possível aplicar a atualização no Assinante no Publicador.<br /><br /> **10** = falha na atualização do download: a atualização no Publicador não pôde ser aplicada ao Assinante.<br /><br /> **12** = atualização do registro lógico WINS excluir: o registro lógico excluído que perde o conflito é registrado nesta tabela.<br /><br /> **13** = atualização de inserção de conflito de registro lógico: Insert em um registro lógico está em conflito com uma atualização.<br /><br /> **14** = registro lógico excluir conflito de atualização do WINS: o registro lógico atualizado que perde o conflito é registrado nesta tabela.|  
|**reason_code**|**int**|Código de erro que pode ser sensível ao contexto.|  
|**reason_text**|**varchar (720)**|Descrição de erro que pode ser sensível ao contexto.|  
|**pubid**|**uniqueidentifier**|Identificador da publicação.|  
|**MSrepl_create_time**|**datetime**|Hora em que as informações de conflitos foram adicionadas.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergeconflictrows** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** e a função **replmonitor** no banco de dados de distribuição podem executar **sp_helpmergeconflictrows**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir informações de conflito para publicações de mesclagem &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
