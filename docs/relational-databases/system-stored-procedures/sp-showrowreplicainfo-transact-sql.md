---
title: sp_showrowreplicainfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords: sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d584c011b61c8b8ad9e3fc55f10a1e7a2512fa97
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre uma linha em uma tabela que está sendo usada como um artigo em replicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@ownername** =] **'***ownername***'**  
 É o nome do proprietário da tabela. *ownername* é **sysname**, com um padrão NULL. Esse parâmetro é útil para diferenciar tabelas se um banco de dados contiver várias tabelas com o mesmo nome, mas cada tabela tiver um proprietário diferente.  
  
 [  **@tablename =**] **'***tablename***'**  
 É o nome da tabela que contém a linha para a qual as informações são retornadas. *TableName* é **sysname**, com um padrão NULL.  
  
 [  **@rowguid =**] *rowguid*  
 É o identificador exclusivo da linha. *ROWGUID* é **uniqueidentifier**, sem padrão.  
  
 [  **@show** =] **'***Mostrar***'**  
 Determina a quantidade de informações a serem retornadas no conjunto de resultados. *Mostrar* é **nvarchar (20)** com um padrão de ambos. Se **linha**, somente informações de versão de linha são retornadas. Se **colunas**, somente informações de versão de coluna são retornadas. Se **ambos**, linhas e as informações de coluna são retornadas.  
  
## <a name="result-sets-for-row-information"></a>Conjuntos de resultado para informações de linha  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão de linha.|  
|**DB_NAME**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**current_state**|**nvarchar(9)**|Retorna informações sobre o estado atual da linha.<br /><br /> **y** -dados de linha representam o estado atual da linha.<br /><br /> **n**-Dados de linha não representam o estado atual da linha.<br /><br /> **\<n / a >** : não aplicável.<br /><br /> **\<desconhecido >** -não é possível determinar o estado atual.|  
|**rowversion_table**|**nchar(17)**|Indica se as versões de linha são armazenadas no [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabela ou o [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabela.|  
|**comentário**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de linha. Geralmente, esse campo fica vazio.|  
  
## <a name="result-sets-for-column-information"></a>Conjuntos de resultado para informações de coluna  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão da coluna.|  
|**DB_NAME**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**colName**|**sysname**|Nome da coluna de artigo que a entrada de versão da coluna representa.|  
|**comentário**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de coluna. Geralmente, esse campo fica vazio.|  
  
## <a name="result-set-for-both"></a>Conjunto de resultados para ambas  
 Se o valor **ambos** é escolhido para *Mostrar*, linha e coluna conjuntos de resultados será retornado.  
  
## <a name="remarks"></a>Comentários  
 **sp_showrowreplicainfo** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 **sp_showrowreplicainfo** só pode ser executado por membros do **db_owner** função de banco de dados fixa no banco de dados de publicação ou por membros da lista de acesso à publicação (PAL) no banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Detectar e resolver conflitos de replicação de mesclagem](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
