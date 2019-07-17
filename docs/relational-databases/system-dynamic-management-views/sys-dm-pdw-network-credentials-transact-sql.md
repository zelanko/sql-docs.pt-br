---
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b75eb53da9961025e3310f27e4a12608dd4fda78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899356"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Retorna uma lista de todas as credenciais de rede armazenada do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] appliance para todos os servidores de destino. Os resultados são listados para o nó de controle e cada nó de computação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Id numérico exclusivo associado ao nó.|  
|target_server_name|**nvarchar(32)**|Endereço IP do servidor de destino que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] acessará usando as credenciais de nome de usuário e senha.|  
|Nome de Usuário|**nvarchar(32)**|O nome de usuário para o qual a senha é armazenada.|  
|last_modified|**datetime**|Data e hora da última operação que modificou a credencial.|  
  
## <a name="permissions"></a>Permissões  
 Requer VIEW SERVER STATE.  
  
## <a name="general-remarks"></a>Comentários gerais  
 É a chave para este modo de exibição de gerenciamento dinâmico *pdw_node_id* plus *target_server_name*.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
