---
title: sp_helpserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0b385ddfdb140f38614e4082b45ada8a8140e4f4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre um determinado servidor de replicação ou remoto, ou sobre todos os servidores de ambos os tipos. Fornece o nome do servidor, o nome da rede do servidor, o status de replicação do servidor, o número de identificação do servidor e o nome de agrupamento. Também fornece valores de tempo limite para se conectar a servidores vinculados ou fazer consultas neles.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server =** ] **'***server***'**  
 É o servidor sobre o qual as informações são relatadas. Quando *servidor* não for especificado, relatórios sobre todos os servidores em **Master.sys**. *servidor* é **sysname**, com um padrão NULL.  
  
 [  **@optname =** ] **'***opção***'**  
 É a opção que descreve o servidor. *opção* é **varchar (** 35 **)**, com um padrão NULL, e deve ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**compatível com agrupamento**|Afeta a execução da consulta distribuída nos servidores vinculados. Se esta opção for definida como verdadeira,|  
|**Acesso a dados**|Habilita e desabilita um servidor vinculado para o acesso às consultas distribuídas.|  
|**dist**|Distribuidor.|  
|**dpub**|Editor remoto para este Distribuidor.|  
|**validação de esquema lenta**|Ignora a verificação de esquema de tabelas remotas no início da consulta.|  
|**pub**|Editor.|  
|**rpc**|Habilita o RPC a partir do servidor especificado.|  
|**RPC out**|Habilita o RPC para o servidor especificado.|  
|**sub**|Assinante.|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**usar agrupamento remoto**|Usa o agrupamento de uma coluna remota em vez do servidor local.|  
  
 [  **@show_topology =** ] **'***show_topology***'**  
 É a relação do servidor especificado com outros servidores. *show_topology* é **varchar (** 1 **)**, com um padrão NULL. Se *show_topology* não é igual a **t** ou for NULL, **sp_helpserver** retornará as colunas listadas na seção de conjuntos de resultados. Se *show_topology* é igual a **t**, além das colunas listadas nos conjuntos de resultados, **sp_helpserver** também retorna **topx** e **topy** informações.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de servidor.|  
|**network_name**|**sysname**|Nome da rede do servidor.|  
|**status**|**varchar (** 70 **)**|Status do servidor.|  
|**id**|**char (** 4 **)**|Número de identificação do servidor.|  
|**collation_name**|**sysname**|Agrupamento do servidor.|  
|**connect_timeout**|**Int**|O valor do tempo limite para conexão com um servidor vinculado.|  
|**query_timeout**|**Int**|O valor do tempo limite para as consultas em servidor vinculado.|  
  
## <a name="remarks"></a>Remarks  
 Um servidor pode ter mais de um status.  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão é verificada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-information-about-all-servers"></a>A. Exibindo informações sobre todos os servidores  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
