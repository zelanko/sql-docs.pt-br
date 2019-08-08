---
title: sp_helpdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0681e82f9e36fd2a2f66bb8b7d3faa2f07a72f13
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770938"
---
# <a name="sp_helpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Lista informações sobre o distribuidor, o banco de dados de distribuição, [!INCLUDE[msCoName](../../includes/msconame-md.md)] o diretório de trabalho e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a conta de usuário do agente. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação ou em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor' OUTPUT`É o nome do distribuidor. O distribuidor é **sysname**, com um padrão **%** de, que é o único valor que retorna um conjunto de resultados.  
  
`[ @distribdb = ] 'distribdb' OUTPUT`É o nome do banco de dados de distribuição. *distribdb* é **sysname**, com um padrão de **%** , que é o único valor que retorna um conjunto de resultados.  
  
`[ @directory = ] 'directory' OUTPUT`É o diretório de trabalho. o *diretório* é **nvarchar (255)** , com um padrão **%** de, que é o único valor que retorna um conjunto de resultados.  
  
`[ @account = ] 'account' OUTPUT`É a [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta de usuário do Windows. a *conta*é **nvarchar (255)** , com um padrão **%** de, que é o único valor que retorna um conjunto de resultados.  
  
`[ @min_distretention = ] _min_distretentionOUTPUT`É o período mínimo de retenção de distribuição, em horas. *min_distretention* é **int**, com um padrão de **-1**.  
  
`[ @max_distretention = ] _max_distretentionOUTPUT`É o período máximo de retenção de distribuição, em horas. *max_distretention* é **int**, com um padrão de **-1**.  
  
`[ @history_retention = ] _history_retentionOUTPUT`É o período de retenção do histórico, em horas. *history_retention* é **int**, com um padrão de **-1**.  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT`É o nome do agente de limpeza de histórico. *history_cleanupagent* é **nvarchar (100)** , com um padrão de **%** , que é o único valor que retorna um conjunto de resultados.  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT`É o nome do agente de limpeza de distribuição. *distrib_cleanupagent* é **nvarchar (100)** , com um padrão de **%** , que é o único valor que retorna um conjunto de resultados.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
`[ @local = ] 'local'`É se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o deve obter valores de servidor local. *local* é **nvarchar (5)** , com um padrão de NULL.  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT`É o nome do servidor que emite chamadas de procedimento remoto. *rpcsrvname* é **sysname**, com um padrão de **%** , que é o único valor que retorna um conjunto de resultados.  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT`É o tipo de editor do Publicador. *publisher_type* é **sysname**, com um padrão de **%** , que é o único valor que retorna um conjunto de resultados.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**distribuidor**|**sysname**|Nome do Distribuidor.|  
|**banco de dados de distribuição**|**sysname**|Nome do banco de dados de distribuição.|  
|**directory**|**nvarchar(255)**|Nome do diretório de trabalho.|  
|**account**|**nvarchar(255)**|Nome da conta de usuário do Windows|  
|**retenção mínima de distrib**|**int**|Período mínimo de retenção de distribuição.|  
|**retenção máxima de distrib**|**int**|Período máximo de retenção de distribuição.|  
|**retenção de histórico**|**int**|Período de retenção do histórico|  
|**Agente de limpeza de histórico**|**nvarchar(100)**|Nome do agente de limpeza do histórico.|  
|**Agente de limpeza de distribuição**|**nvarchar(100)**|Nome do agente de limpeza da Distribuição.|  
|**nome do servidor RPC**|**sysname**|Nome do Distribuidor local ou remoto.|  
|**nome de logon RPC**|**sysname**|Logon usado para chamadas de procedimento remoto ao Distribuidor remoto.|  
|**tipo de editor**|**sysname**|Tipo de Publicador, que pode ser um dos seguintes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **GATEWAY ORACLE**|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistributor** é usado em todos os tipos de replicação.  
  
 Se um ou mais parâmetros de saída forem especificados durante a execução de **sp_helpdistributor**, todos os parâmetros de saída definidos como NULL serão atribuídos aos valores na saída e nenhum conjunto de resultados será retornado. Se nenhum parâmetro de saída for especificado, um conjunto de resultados será retornado.  
  
## <a name="permissions"></a>Permissões  
 As seguintes colunas de conjunto de resultados ou parâmetros de saída são retornados aos membros da função de servidor fixa **sysadmin** no Publicador e à função de banco de dados fixa **db_owner** no banco de dados de publicação:  
  
|Coluna de conjunto de resultados|Parâmetro de saída|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|nenhum|  
  
 A coluna de conjunto de resultados seguinte é retornada aos usuários na lista de acesso à publicação no Distribuidor:  
  
-   directory  
  
 As colunas de conjunto de resultados a seguir são retornadas a todos os usuários.  
  
|Coluna de conjunto de resultados|Parâmetro de saída|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|distribution database|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
