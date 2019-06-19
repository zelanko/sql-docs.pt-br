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
manager: craigg
ms.openlocfilehash: d521a16fa7c18e67e1929cb0e38aecf862d6c18a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822644"
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
`[ @proxy_id = ] proxy_id` O número de identificação do proxy para listar informações. O *proxy_id* é **int**, com um padrão NULL. Ambos os *id* ou o *proxy_name* pode ser especificado.  
  
`[ @proxy_name = ] 'proxy_name'` O nome do proxy para listar informações. O *proxy_name* é **sysname**, com um padrão NULL. Ambos os *id* ou o *proxy_name* pode ser especificado.  
  
`[ @subsystem_id = ] subsystem_id` O número de identificação do subsistema para listar informações. O *subsystem_id* é **int**, com um padrão NULL. Ambos os *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
`[ @subsystem_name = ] 'subsystem_name'` O nome do subsistema para listar informações. O *subsystem_name* é **sysname**, com um padrão NULL. Ambos os *subsystem_id* ou o *subsystem_name* pode ser especificado.  
  
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
 Quando nenhum parâmetro for fornecido, **sp_enum_proxy_for_subsystem** lista informações sobre todos os proxies na instância para cada subsistema.  
  
 Quando uma id de proxy ou nome de proxy é fornecido, **sp_enum_proxy_for_subsystem** lista os subsistemas proxy tem acessem. Quando uma id de subsistema ou nome de subsistema é fornecido, **sp_enum_proxy_for_subsystem** lista os proxies que têm acesso a esse subsistema.  
  
 Quando informações de proxy e informações de subsistema são fornecidas, o conjunto de resultados retornará uma linha se o proxy especificado tiver acesso ao subsistema especificado.  
  
 Esse procedimento armazenado está localizado em **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão os membros de **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-associations"></a>A. Listando todas as associações  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
