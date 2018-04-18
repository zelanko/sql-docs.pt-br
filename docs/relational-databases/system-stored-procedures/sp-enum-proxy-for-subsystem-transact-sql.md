---
title: sp_enum_proxy_for_subsystem (Transact-SQL) | Microsoft Docs
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
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8551a807fd916c80909e281c8ddd6bc785315573
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as permissões para que os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent acessem subsistemas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id** =] *proxy_id*  
 O número de identificação do proxy para o qual as informações serão listadas. O *proxy_id* é **int**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
 [ **@proxy_name** =] **'***proxy_name***'**  
 O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão NULL. Ambos o *id* ou *proxy_name* pode ser especificado.  
  
 [ **@subsystem_id** =] *subsystem_id*  
 O número de identificação do subsistema para o qual as informações serão listadas. O *subsystem_id* é **int**, com um padrão NULL. Ambos os *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
 [ **@subsystem_name** = ] **'***subsystem_name***'**  
 O nome do subsistema para o qual as informações serão listadas. O *subsystem_name* é **sysname**, com um padrão NULL. Ambos os *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**Int**|Número de identificação do subsistema.|  
|**subsystem_name**|**sysname**|O nome do subsistema.|  
|**proxy_id**|**Int**|Número de identificação de proxy.|  
|**proxy_name**|**sysname**|O nome do proxy.|  
  
## <a name="remarks"></a>Remarks  
 Quando nenhum parâmetro for fornecido, **sp_enum_proxy_for_subsystem** lista informações sobre todos os proxies na instância para todo subsistema.  
  
 Quando um id de proxy ou nome de proxy é fornecido, **sp_enum_proxy_for_subsystem** subsistemas de listas que o proxy tem acessem. Quando um id de subsistema ou nome de subsistema é fornecido, **sp_enum_proxy_for_subsystem** lista os proxies que têm acesso a esse subsistema.  
  
 Quando informações de proxy e informações de subsistema são fornecidas, o conjunto de resultados retornará uma linha se o proxy especificado tiver acesso ao subsistema especificado.  
  
 Esse procedimento armazenado está localizado em **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-associations"></a>A. Listando todas as associações  
 O exemplo a seguir lista todas as permissões estabelecidas entre proxies e subsistemas para a instância atual.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. Determinando se um proxy tem acesso a um subsistema específico  
 O exemplo a seguir retornará uma linha se o proxy `Catalog application proxy` tiver acesso ao subsistema `ActiveScripting`. Caso contrário, o exemplo retorna um conjunto de resultados vazio.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
