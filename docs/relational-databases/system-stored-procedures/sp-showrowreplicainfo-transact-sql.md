---
title: sp_showrowreplicainfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d009b05fea2a2c587f97dc4b2416588932ad0bc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530358"
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre uma linha em uma tabela que está sendo usada como um artigo em replicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ownername = ] 'ownername'` É o nome do proprietário. *ownername* está **sysname**, com um padrão NULL. Esse parâmetro é útil para diferenciar tabelas se um banco de dados contiver várias tabelas com o mesmo nome, mas cada tabela tiver um proprietário diferente.  
  
`[ @tablename = ] 'tablename'` É o nome da tabela que contém a linha para o qual as informações são retornadas. *TableName* está **sysname**, com um padrão NULL.  
  
`[ @rowguid = ] rowguid` É o identificador exclusivo da linha. *ROWGUID* está **uniqueidentifier**, sem padrão.  
  
`[ @show = ] 'show'` Determina a quantidade de informações a serem retornadas no conjunto de resultados. *Mostrar* está **nvarchar (20)** com um padrão de ambos. Se **linha**, somente informações de versão de linha são retornadas. Se **colunas**, somente informações de versão de coluna são retornadas. Se **ambos**, linhas e de informações da coluna são retornadas.  
  
## <a name="result-sets-for-row-information"></a>Conjuntos de resultado para informações de linha  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão de linha.|  
|**db_name**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**current_state**|**nvarchar(9)**|Retorna informações sobre o estado atual da linha.<br /><br /> **y** -dados de linha representam o estado atual da linha.<br /><br /> **n** -dados de linha não representam o estado atual da linha.<br /><br /> **\<n/a >** – não aplicável.<br /><br /> **\<desconhecido >** -não é possível determinar o estado atual.|  
|**rowversion_table**|**nchar(17)**|Indica se as versões de linha são armazenadas do [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabela ou o [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabela.|  
|**comment**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de linha. Geralmente, esse campo fica vazio.|  
  
## <a name="result-sets-for-column-information"></a>Conjuntos de resultado para informações de coluna  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão da coluna.|  
|**db_name**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**colname**|**sysname**|Nome da coluna de artigo que a entrada de versão da coluna representa.|  
|**comment**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de coluna. Geralmente, esse campo fica vazio.|  
  
## <a name="result-set-for-both"></a>Conjunto de resultados para ambas  
 Se o valor **ambos** é escolhido para *Mostrar*, linha e coluna de conjuntos de resultados será retornado.  
  
## <a name="remarks"></a>Comentários  
 **sp_showrowreplicainfo** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 **sp_showrowreplicainfo** só pode ser executado por membros dos **db_owner** função de banco de dados fixa do banco de dados de publicação ou por membros da lista de acesso de publicação (PAL) o banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Detectar e resolver conflitos de replicação de mesclagem](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
