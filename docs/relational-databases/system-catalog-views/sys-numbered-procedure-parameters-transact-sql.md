---
title: numbered_procedure_parameters (Transact-SQL) | Microsoft Docs
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
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8510807f4e06cb1f880be1bb982eee59db6994f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada parâmetro de um procedimento numerado. Quando você cria um procedimento armazenado numerado, o procedimento básico é o número 1. Todos os procedimentos subsequentes têm números 2, 3 e assim por diante. **numbered_procedure_parameters** contém as definições de parâmetro para todos os procedimentos subsequentes, numerados como 2 e maior. Essa exibição não mostra parâmetros para o procedimento armazenado básico (número = 1). O procedimento armazenado básico é semelhante a um procedimento armazenado não numerado. Portanto, os parâmetros são representados em [sys. Parameters (Transact-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md).  
  
> [!IMPORTANT]  
>  Os procedimentos numerados são preteridos. O uso de procedimentos numerados é desaconselhável. Um evento DEPRECATION_ANNOUNCEMENT será acionado quando uma consulta que usa essa exibição do catálogo for compilada.  
  
> [!NOTE]  
>  Não há suporte para os parâmetros XML e CLR em procedimentos numerados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**procedure_number**|**smallint**|Número deste procedimento no objeto, 2 ou maior.|  
|**name**|**sysname**|Nome do parâmetro. É exclusivo dentro de **procedure_number**.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusivo dentro do **procedure_number**.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro|  
|**user_type_id**|**int**|ID do tipo do parâmetro, conforme definido pelo usuário.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro em bytes.<br /><br /> -1 = O tipo de dados de coluna é varchar(max), nvarchar(max) ou varbinary(max).|  
|**precisão**|**tinyint**|Precisão do parâmetro se tiver base numérica; Caso contrário, 0.|  
|**escala**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída ou retorno; do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = parâmetro é um parâmetro de referência de cursor.|  
  
> [!NOTE]  
>  Não há suporte para os parâmetros XML e CLR em procedimentos numerados.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
