---
title: sys. sysconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a945b5027afdaf58d5abc266f37d8c8823947b73
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém mapeamentos de restrições aos objetos que possuem as restrições no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**Int**|Número de restrição.|  
|**id**|**Int**|ID da tabela que possui a restrição.|  
|**colid**|**smallint**|ID da coluna na qual a restrição é definida.<br /><br /> 0 = Restrição de tabela|  
|**spare1**|**tinyint**|Reservado|  
|**status**|**Int**|Máscara de pseudobit que indica o status. Os possíveis valores incluem os seguintes:<br /><br /> 1 = Restrição PRIMARY KEY<br /><br /> 2 = Restrição UNIQUE KEY<br /><br /> 3 = Restrição FOREIGN KEY<br /><br /> 4 = Restrição CHECK<br /><br /> 5 = Restrição DEFAULT<br /><br /> 16 = Restrição em nível de coluna<br /><br /> 32 = Restrição em nível de tabela|  
|**ações**|**Int**|Reservado|  
|**error**|**Int**|Reservado|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
