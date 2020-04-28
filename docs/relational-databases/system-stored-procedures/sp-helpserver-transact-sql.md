---
title: sp_helpserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
author: stevestein
ms.author: sstein
ms.openlocfilehash: 844e96d765f9ed06f88b140b906b78eb4ea16ea0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67997437"
---
# <a name="sp_helpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre um determinado servidor de replicação ou remoto, ou sobre todos os servidores de ambos os tipos. Fornece o nome do servidor, o nome da rede do servidor, o status de replicação do servidor, o número de identificação do servidor e o nome de ordenação. Também fornece valores de tempo limite para se conectar a servidores vinculados ou fazer consultas neles.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server = ] 'server'`É o servidor sobre quais informações são relatadas. Quando o *servidor* não for especificado, os relatórios sobre todos os servidores em **Master. sys. Servers**. o *servidor* é **sysname**, com um padrão de NULL.  
  
`[ @optname = ] 'option'`É a opção que descreve o servidor. a *opção* é **varchar (** 35 **)**, com um padrão de NULL e deve ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**compatível com agrupamento**|Afeta a execução da consulta distribuída nos servidores vinculados. Se esta opção for definida como verdadeira,|  
|**acesso a dados**|Habilita e desabilita um servidor vinculado para o acesso às consultas distribuídas.|  
|**dist**|Distribuidor.|  
|**dpub**|Editor remoto para este Distribuidor.|  
|**validação de esquema lenta**|Ignora a verificação de esquema de tabelas remotas no início da consulta.|  
|**pub**|Editor.|  
|**rpc**|Habilita o RPC a partir do servidor especificado.|  
|**saída de RPC**|Habilita o RPC para o servidor especificado.|  
|**projeto**|Farão.|  
|**sistema**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**usar agrupamento remoto**|Usa a ordenação de uma coluna remota em vez do servidor local.|  
  
`[ @show_topology = ] 'show_topology'`É a relação do servidor especificado com outros servidores. *show_topology* é **varchar (** 1 **)**, com um padrão de NULL. Se *show_topology* não for igual a **t** ou for nulo, **sp_helpserver** retornará colunas listadas na seção conjuntos de resultados. Se *show_topology* for igual a **t**, além das colunas listadas nos conjuntos de resultados, **sp_helpserver** também retornará informações de **topx** e **Topy** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de servidor.|  
|**network_name**|**sysname**|Nome da rede do servidor.|  
|**status**|**varchar (** 70 **)**|Status do servidor.|  
|**id**|**Char (** 4 **)**|Número de identificação do servidor.|  
|**collation_name**|**sysname**|Ordenação do servidor.|  
|**connect_timeout**|**int**|O valor do tempo limite para conexão com um servidor vinculado.|  
|**query_timeout**|**int**|O valor do tempo limite para as consultas em servidor vinculado.|  
  
## <a name="remarks"></a>Comentários  
 Um servidor pode ter mais de um status.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é verificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-information-about-all-servers"></a>a. Exibindo informações sobre todos os servidores  
 O exemplo a seguir exibe informações sobre todos os servidores usando `sp_helpserver` sem nenhum parâmetro.  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. Exibindo informações sobre um servidor específico  
 O exemplo a seguir exibe todas as informações sobre o servidor `SEATTLE2`.  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addsubscriber](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscriber](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_serveroption](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
