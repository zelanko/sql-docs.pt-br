---
title: sys. syscharsets (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs: TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3cd92e352a937831427bcf90165c5d17ced8e11
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada conjunto de caracteres e ordem de classificação definidos para uso pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Uma das ordens de classificação é marcada no **sysconfigures** como a ordem de classificação padrão. Ela é a única realmente utilizada.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**tipo**|**smallint**|Tipo de entidade que a linha representa:<br /><br /> 1001 = Conjunto de caracteres.<br /><br /> 2001 = Ordem de classificação.|  
|**id**|**tinyint**|ID exclusivo para o conjunto de caracteres ou ordem de classificação. Note que as ordens de classificação e os conjuntos de caracteres não podem compartilhar o mesmo número de ID. O intervalo de ID de 1 a 240 está reservado para uso do [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|**CSID**|**tinyint**|Se a linha representar um conjunto de caracteres, este campo não será utilizado. Se a linha representar uma ordem de classificação, este campo será a ID do conjunto de caracteres em que se baseia a ordem de classificação. Supõe-se que exista uma linha de conjunto de caracteres com esta ID nesta tabela.|  
|**status**|**smallint**|Bits de informação sobre o status do sistema interno.|  
|**name**|**sysname**|Nome exclusivo para o conjunto de caracteres ou ordem de classificação. Este campo deve conter só letras A-Z ou a-z, números 0 - 9 e sublinhados (_) e deve se iniciar com uma letra.|  
|**Descrição**|**nvarchar(255)**|Descrição opcional dos recursos do conjunto de caracteres ou ordem de classificação.|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**definição**|**imagem**|Definição interna do conjunto de caracteres ou ordem de classificação. A estrutura dos dados neste campo depende do tipo.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
