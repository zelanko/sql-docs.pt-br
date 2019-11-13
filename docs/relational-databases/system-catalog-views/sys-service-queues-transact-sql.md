---
title: sys.service_queues (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_queues
- service_queues
- service_queues_TSQL
- sys.service_queues_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queues catalog view
ms.assetid: 9fd9fa76-6128-410c-896f-741e6050143a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38b5ac732926ae544dbad2cc22006c45533702c3
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982598"
---
# <a name="sysservice_queues-transact-sql"></a>sys.service_queues (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada objeto no banco de dados que é uma fila de serviço, com **Sys. Objects. Type** = sq.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<colunas herdadas >**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. &#40;Objects Transact&#41;-SQL](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**max_readers**|**smallint**|O número máximo dos leitores simultâneos permitidos na fila.|  
|**activation_procedure**|**nvarchar(776)**|O nome de três partes do procedimento de ativação.|  
|**execute_as_principal_id**|**int**|A identificação do principal de banco de dados EXECUTE AS.<br /><br /> NULL por padrão ou se EXECUTE AS CALLER.<br /><br /> ID da entidade de segurança especificada se EXECUTE AS SELF EXECUTE AS \<> principal.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**is_activation_enabled**|**bit**|1 = Ativação está habilitada.|  
|**is_receive_enabled**|**bit**|1 = Recebimento está habilitado.|  
|**is_enqueue_enabled**|**bit**|1 = Enfileiramento está habilitado.|  
|**is_retention_enabled**|**bit**|1 = Mensagens são retidas até o fim do diálogo.|  
|**is_poison_message_handling_enabled**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> 1 = A manipulação de mensagens suspeitas está habilitada.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
