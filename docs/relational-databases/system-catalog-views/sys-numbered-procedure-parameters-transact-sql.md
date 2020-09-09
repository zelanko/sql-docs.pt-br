---
description: sys.numbered_procedure_parameters (Transact-SQL)
title: sys. numbered_procedure_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4bb67e0f0063c9ed7469b0a3d9e29a29b8117e22
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539590"
---
# <a name="sysnumbered_procedure_parameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada parâmetro de um procedimento numerado. Quando você cria um procedimento armazenado numerado, o procedimento básico é o número 1. Todos os procedimentos subsequentes têm números 2, 3 e assim por diante. **Sys. numbered_procedure_parameters** contém as definições de parâmetro para todos os procedimentos subsequentes, numerados 2 e maiores. Essa exibição não mostra parâmetros para o procedimento armazenado básico (número = 1). O procedimento armazenado básico é semelhante a um procedimento armazenado não numerado. Portanto, seus parâmetros são representados em [Sys. Parameters (Transact-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md).  
  
> [!IMPORTANT]  
>  Os procedimentos numerados são preteridos. O uso de procedimentos numerados é desaconselhável. Um evento DEPRECATION_ANNOUNCEMENT será acionado quando uma consulta que usa essa exibição do catálogo for compilada.  
  
> [!NOTE]  
>  Não há suporte para os parâmetros XML e CLR em procedimentos numerados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**procedure_number**|**smallint**|Número deste procedimento no objeto, 2 ou maior.|  
|**name**|**sysname**|Nome do parâmetro. É exclusivo dentro de **procedure_number**.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusivo dentro do **procedure_number**.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro|  
|**user_type_id**|**int**|ID do tipo do parâmetro, conforme definido pelo usuário.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro em bytes.<br /><br /> -1 = O tipo de dados de coluna é varchar(max), nvarchar(max) ou varbinary(max).|  
|**precisão**|**tinyint**|Precisão do parâmetro se for baseado em numeric; caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída ou retorno; do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = o parâmetro é um parâmetro de referência de cursor.|  
  
> [!NOTE]  
>  Não há suporte para os parâmetros XML e CLR em procedimentos numerados.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
