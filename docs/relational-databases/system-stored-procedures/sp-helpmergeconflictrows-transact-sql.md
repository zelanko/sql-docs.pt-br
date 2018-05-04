---
title: sp_helpmergeconflictrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4f659af9b6ba2ea785d344311c9d7471dc25a26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **%**. Se a publicação for especificada, serão retornados todos os conflitos qualificados pela publicação. Por exemplo, se o **MSmerge_conflict_Customers** tabela tem linhas de conflito para o **WA** e **CA** publicações, passando um nome de publicação **autoridade de certificação**  recuperará os conflitos que pertencem ao **CA** publicação.  
  
 [  **@conflict_table=**] **'***conflict_table***'**  
 É o nome da tabela de conflito. *conflict_table* é **sysname**, sem padrão. Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, as tabelas de conflitos são nomeadas usando nomes de formato com **msmerge_conflict _* publicação *_* artigo *, com uma tabela para cada publicação artigo.  
  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um padrão NULL.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados publicador. *publisher_db* é **sysname**, com um padrão NULL.  
  
 [  **@logical_record_conflicts=** ] *logical_record_conflicts*  
 Indica se o conjunto de resultados contém informações sobre conflitos de registro lógico. *logical_record_conflicts* é **int**, com um valor padrão de 0. **1** significa que as informações de conflitos de registro lógico são retornadas.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpmergeconflictrows** retorna um conjunto de resultados consistindo da estrutura da tabela base e essas colunas adicionais.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|Origem do conflito.|  
|**conflict_type**|**Int**|Código que indica o tipo de conflito:<br /><br /> **1** = conflito de atualização: O conflito é detectado no nível de linha.<br /><br /> **2** = conflito de atualização de coluna: O conflito é detectado no nível de coluna.<br /><br /> **3** = conflito de atualização exclusão Wins: A exclusão ganha o conflito.<br /><br /> **4** = conflito de exclusão vence atualização: O rowguid excluído que perde o conflito é registrado nessa tabela.<br /><br /> **5** = carregar Falha na inserção: A inserção do assinante não puderam ser aplicada no publicador.<br /><br /> **6** = baixar Falha na inserção: A inserção do publicador não pôde ser aplicada no assinante.<br /><br /> **7** = carregar Falha na exclusão: A exclusão no assinante não pôde ser carregada no publicador.<br /><br /> **8** = baixar Falha na exclusão: não foi possível baixar a exclusão no publicador ao assinante.<br /><br /> **9** = carregar Falha na atualização: A atualização do assinante não puderam ser aplicada no publicador.<br /><br /> **10** = baixar Falha na atualização: A atualização do publicador não pôde ser aplicada ao assinante.<br /><br /> **12** = lógico registro atualização vence exclusão: O registro lógico excluído que perde o conflito é registrado nessa tabela.<br /><br /> **13** = lógico registro conflito inserção de atualização: inserir em um registro lógico conflita com uma atualização.<br /><br /> **14** = lógico registro Wins atualização conflito de exclusão: O registro lógico atualizado que perde o conflito é registrado nessa tabela.|  
|**reason_code**|**Int**|Código de erro que pode ser sensível ao contexto.|  
|**reason_text**|**varchar(720)**|Descrição de erro que pode ser sensível ao contexto.|  
|**pubid**|**uniqueidentifier**|Identificador da publicação.|  
|**MSrepl_create_time**|**datetime**|Hora em que as informações de conflitos foram adicionadas.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergeconflictrows** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor a **db_owner** fixo de função de banco de dados e o **replmonitor** no banco de dados de distribuição podem executar **sp_helpmergeconflictrows**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir informações de conflito para publicações de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
