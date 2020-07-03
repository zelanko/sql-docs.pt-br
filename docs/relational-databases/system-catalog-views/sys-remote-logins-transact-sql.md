---
title: sys. remote_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.remote_logins_TSQL
- remote_logins
- remote_logins_TSQL
- sys.remote_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_logins catalog view
ms.assetid: 38477e91-d084-4df7-b1de-b930c5580189
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 587e117ce58ca0beff93adc8be864bcf6777b416
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880006"
---
# <a name="sysremote_logins-transact-sql"></a>sys.remote_logins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada mapeamento de logon remoto. Essa exibição do catálogo é usada para mapear logons de entrada locais que alegam estar vindo de um servidor correspondente para um logon local real.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID do servidor em **Sys. Servers**. Esse nome é fornecido pela conexão no servidor "remoto".|  
|**remote_name**|**sysname**|Nome de logon que a conexão fornecerá para ser mapeada. Se for NULL, será usado o nome de logon que é especificado na conexão.|  
|**local_principal_id**|**int**|ID da entidade do servidor para quem o logon é mapeado. Se for 0, o logon remoto será mapeado para o logon com o mesmo nome.|  
|**modify_date**|**datetime**|Data em que o logon vinculado foi alterado pela última vez.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de servidores vinculados &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
