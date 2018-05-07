---
title: sp_help_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 236a10fd52508781e503cc2844a49315fe57422e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelptargetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista todos os servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@server_name=** ] **'***server_name***'**  
 O nome do servidor do qual retornar informações. *server_name* é **nvarchar (30)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *nome_do_servidor* não for especificado, **sp_help_targetserver** retorna o conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**Int**|Número de identificação do servidor.|  
|**server_name**|**nvarchar(30)**|Nome de servidor.|  
|**local**|**nvarchar(200)**|Localização do servidor especificado.|  
|**time_zone_adjustment**|**Int**|Ajuste de fuso horário, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data do alistamento do servidor especificado.|  
|**last_poll_date**|**datetime**|Data da última vez em que o servidor foi  sondado para trabalhos.|  
|**status**|**Int**|Status do servidor especificado.|  
|**unread_instructions**|**Int**|Indica se o servidor tem ordens não lidas. Se todas as linhas tiverem sido baixadas, esta coluna é **0**.|  
|**local_time**|**datetime**|Data e hora locais do servidor de destino, baseadas na hora local do servidor de destino até a última sondagem do servidor mestre.|  
|**enlisted_by_nt_user**|**nvarchar(100)**|Usuário de Microsoft Windows que inscreveu o servidor de destino.|  
|**poll_interval**|**Int**|Frequência em segundos com que o servidor de destino sonda o serviço Master SQLServer Agent para baixar trabalhos e carregar o status dos trabalhos.|  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. Listando informações para todos os servidores de destino registrados  
 O exemplo a seguir lista as informações de todos os servidores de destino registrados.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. Listando informações de um servidor de destino específico.  
 O exemplo a seguir lista as informações do servidor de destino `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
