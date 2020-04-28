---
title: sp_enum_proxy_for_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 93a55b28325bd9b04af569120ad34baeb689e8f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124655"
---
# <a name="sp_enum_proxy_for_subsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as permissões para que os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent acessem subsistemas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] proxy_id`O número de identificação do proxy para o qual listar informações. O *proxy_id* é **int**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
`[ @proxy_name = ] 'proxy_name'`O nome do proxy para o qual listar informações. O *proxy_name* é **sysname**, com um padrão de NULL. A *ID* ou a *proxy_name* pode ser especificada.  
  
`[ @subsystem_id = ] subsystem_id`O número de identificação do subsistema para o qual listar informações. O *subsystem_id* é **int**, com um padrão de NULL. O *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
`[ @subsystem_name = ] 'subsystem_name'`O nome do subsistema para o qual listar informações. O *subsystem_name* é **sysname**, com um padrão de NULL. O *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Número de identificação do subsistema.|  
|**subsystem_name**|**sysname**|O nome do subsistema.|  
|**proxy_id**|**int**|Número de identificação de proxy.|  
|**proxy_name**|**sysname**|O nome do proxy.|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Comentários  
 Quando nenhum parâmetro é fornecido, **sp_enum_proxy_for_subsystem** lista informações sobre todos os proxies na instância para cada subsistema.  
  
 Quando uma ID de proxy ou um nome de proxy é fornecido, **sp_enum_proxy_for_subsystem** lista os subsistemas aos quais o proxy tem acesso. Quando uma ID de subsistema ou nome de subsistema é fornecido, **sp_enum_proxy_for_subsystem** lista os proxies que têm acesso a esse subsistema.  
  
 Quando informações de proxy e informações de subsistema são fornecidas, o conjunto de resultados retornará uma linha se o proxy especificado tiver acesso ao subsistema especificado.  
  
 Esse procedimento armazenado está localizado no **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-associations"></a>a. Listando todas as associações  
 O exemplo a seguir lista todas as permissões estabelecidas entre proxies e subsistemas para a instância atual.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. Determinando se um proxy tem acesso a um subsistema específico  
 O exemplo a seguir retornará uma linha se o proxy `Catalog application proxy` tiver acesso ao subsistema `ActiveScripting`. Caso contrário, o exemplo retorna um conjunto de resultados vazio.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_grant_proxy_to_subsystem](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
