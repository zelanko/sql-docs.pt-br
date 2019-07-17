---
title: sysarticlecolumns (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a0505b8316254090fe5f2310fa68011d8289679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129547"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (exibição de sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **sysarticlecolumns** exibição expõe informações adicionais sobre colunas em artigos publicados. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**int**|Identifica uma coluna em um artigo.|  
|**is_udt**|**int**|Indica se a coluna é uma coluna UDT (User-Defined Data Type). Um valor de **1** indica uma coluna UDT.|  
|**is_xml**|**int**|Se a coluna é uma **xml** coluna. Um valor de **1** indica uma **xml** coluna.|  
|**is_max**|**int**|Se a coluna é uma coluna de tipo de dados de valor grande (**varchar (max)** , **nvarchar (max)** ou **varbinary (max)** ). Um valor de **1** indica uma coluna de valor grande.|  
  
## <a name="see-also"></a>Consulte também  
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
