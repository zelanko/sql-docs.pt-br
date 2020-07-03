---
title: sys. linked_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e7086cc86e6aa55b537050cc43d20e2512e36133
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892375"
---
# <a name="syslinked_logins-transact-sql"></a>sys.linked_logins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha por mapeamento de logon de servidor vinculado, para ser usado por RPC e consultas distribuídas de um servidor local para o servidor vinculado correspondente.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID do servidor em **Sys. Servers**.|  
|**local_principal_id**|**int**|Principal de Servidor ao qual o mapeamento se aplica.<br /><br /> 0 = curinga ou público.|  
|**uses_self_credential**|**bit**|Se for 1, o mapeamento indica que a sessão deve usar suas próprias credenciais; caso contrário, 0 indica que a sessão usa o nome e a senha fornecidos.|  
|**remote_name**|**sysname**|Nome de usuário remoto a ser usado ao se conectar. A senha também é armazenada, mas não exposta em interfaces de exibição do catálogo.|  
|**modify_date**|**datetime**|Data em que o logon vinculado foi alterado pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de servidores vinculados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
