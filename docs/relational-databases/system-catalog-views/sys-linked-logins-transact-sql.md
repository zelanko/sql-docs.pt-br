---
title: linked_logins (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.linked_logins
- sys.linked_logins_TSQL
- linked_logins_TSQL
- linked_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.linked_logins catalog view
ms.assetid: af57bf0c-a265-410f-9bab-63b78569b4a6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ca2137294edf7a24c0ad5b167c5e1037a86cab1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="syslinkedlogins-transact-sql"></a>sys.linked_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por mapeamento de logon de servidor vinculado, para ser usado por RPC e consultas distribuídas de um servidor local para o servidor vinculado correspondente.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID do servidor em **sys**.|  
|**local_principal_id**|**int**|Principal de Servidor ao qual o mapeamento se aplica.<br /><br /> 0 = curinga ou público.|  
|**uses_self_credential**|**bit**|Se for 1, o mapeamento indica que a sessão deve usar suas próprias credenciais; caso contrário, 0 indica que a sessão usa o nome e a senha fornecidos.|  
|**remote_name**|**sysname**|Nome de usuário remoto a ser usado ao se conectar. A senha também é armazenada, mas não exposta em interfaces de exibição do catálogo.|  
|**modify_date**|**datetime**|Data em que o logon vinculado foi alterado pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de servidores vinculados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
