---
description: sp_showrowreplicainfo (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a46fd42c9caa69e808635fc9dcc5125403697a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543021"
---
# <a name="sp_showrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe informações sobre uma linha em uma tabela que está sendo usada como um artigo em replicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ownername = ] 'ownername'` É o nome do proprietário da tabela. *OwnerName* é **sysname**, com um padrão de NULL. Esse parâmetro é útil para diferenciar tabelas se um banco de dados contiver várias tabelas com o mesmo nome, mas cada tabela tiver um proprietário diferente.  
  
`[ @tablename = ] 'tablename'` É o nome da tabela que contém a linha para a qual as informações são retornadas. *TableName* é **sysname**, com um padrão de NULL.  
  
`[ @rowguid = ] rowguid` É o identificador exclusivo da linha. *ROWGUID* é **uniqueidentifier**, sem padrão.  
  
`[ @show = ] 'show'` Determina a quantidade de informações a serem retornadas no conjunto de resultados. *show* é **nvarchar (20)** com um padrão de ambos. Se for **linha**, apenas as informações de versão de linha serão retornadas. Se houver **colunas**, somente as informações de versão de coluna serão retornadas. Se **ambas**, as informações de linha e coluna forem retornadas.  
  
## <a name="result-sets-for-row-information"></a>Conjuntos de resultado para informações de linha  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão de linha.|  
|**db_name**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**current_state**|**nvarchar (9)**|Retorna informações sobre o estado atual da linha.<br /><br /> os dados de linha **y** representam o estado atual da linha.<br /><br /> os dados de **n** linhas não representam o estado atual da linha.<br /><br /> **\<n/a>** -Não aplicável.<br /><br /> **\<unknown>** -O estado atual não pode ser determinado.|  
|**rowversion_table**|**nchar (17)**|Indica se as versões de linha são armazenadas na tabela de [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) ou na tabela [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) .|  
|**mente**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de linha. Geralmente, esse campo fica vazio.|  
  
## <a name="result-sets-for-column-information"></a>Conjuntos de resultado para informações de coluna  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nome do servidor que hospeda o banco de dados que fez a entrada da versão da coluna.|  
|**db_name**|**sysname**|Nome do banco de dados que fez essa entrada.|  
|**db_nickname**|**binary(6)**|Apelido do banco de dados que fez essa entrada.|  
|**version**|**int**|Versão da entrada.|  
|**ColName**|**sysname**|Nome da coluna de artigo que a entrada de versão da coluna representa.|  
|**mente**|**nvarchar(255)**|Informações adicionais sobre essa entrada de versão de coluna. Geralmente, esse campo fica vazio.|  
  
## <a name="result-set-for-both"></a>Conjunto de resultados para ambas  
 Se o valor for escolhido para *Mostrar*, os conjuntos de resultados de linha e de **coluna serão retornados** .  
  
## <a name="remarks"></a>Comentários  
 **sp_showrowreplicainfo** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 **sp_showrowreplicainfo** só pode ser executado por membros da função de banco de dados fixa **db_owner** no banco de dados de publicação ou por membros da PAL (lista de acesso à publicação) no banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Detectar e resolver conflitos de replicação de mesclagem](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
