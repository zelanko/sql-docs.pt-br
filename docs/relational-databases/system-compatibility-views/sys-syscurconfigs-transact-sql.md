---
description: sys.syscurconfigs (Transact-SQL)
title: sys.syscurconfigs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: c5c83219c93c24929b257989a034f283cf2ac5b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423320"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma entrada para cada opção de configuração atual. Além disso, esta exibição contém quatro entradas que descrevem a estrutura da configuração. **syscurconfigs** é criado dinamicamente quando consultado por um usuário. Para obter mais informações, consulte [sys.sysconfigura &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Valor modificável pelo usuário para a variável. Isso só será usado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se RECONFIGURE tiver sido executado.|  
|**config**|**smallint**|Número variável de configuração.|  
|**mente**|**nvarchar(255)**|Explicação da opção de configuração.|  
|**status**|**smallint**|Bitmap indicando o status da opção. Os possíveis valores incluem os seguintes:<br /><br /> 0 = Estático. A definição entra em vigor quando o servidor é reinicializado.<br /><br /> 1 = Dinâmico. A variável é implementada quando a instrução RECONFIGURE é executada.<br /><br /> 2 = Avançado. A variável é exibida somente quando a **opção Mostrar opções avançadas** está definida.<br /><br /> 3 = Dinâmico e avançado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
