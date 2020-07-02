---
title: Restrições de sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysconstraints
- sys.sysconstraints
- sysconstraints_TSQL
- sys.sysconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconstraints compatibility view
- sysconstraints system table
ms.assetid: f2b2e2ad-ba24-48a1-913c-8ee4e0895dc4
author: rothja
ms.author: jroth
ms.openlocfilehash: b3ee1ce24876eab6689da7432329a2788ce70c34
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85663352"
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém mapeamentos de restrições aos objetos que possuem as restrições no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|Número de restrição.|  
|**id**|**int**|ID da tabela que possui a restrição.|  
|**colid**|**smallint**|ID da coluna na qual a restrição é definida.<br /><br /> 0 = Restrição de tabela|  
|**spare1**|**tinyint**|Reservado|  
|**status**|**int**|Máscara de pseudobit que indica o status. Os possíveis valores incluem os seguintes:<br /><br /> 1 = Restrição PRIMARY KEY<br /><br /> 2 = Restrição UNIQUE KEY<br /><br /> 3 = Restrição FOREIGN KEY<br /><br /> 4 = Restrição CHECK<br /><br /> 5 = Restrição DEFAULT<br /><br /> 16 = Restrição em nível de coluna<br /><br /> 32 = Restrição em nível de tabela|  
|**actions**|**int**|Reservado|  
|**error**|**int**|Reservado|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
