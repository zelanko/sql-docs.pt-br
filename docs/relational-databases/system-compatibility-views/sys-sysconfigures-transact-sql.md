---
description: sys.sysconfigures (Transact-SQL)
title: sys.sysconfigura (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysconfigures
- sysconfigures
- sys.sysconfigures_TSQL
- sysconfigures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconfigures compatibility view
- sysconfigures system table
ms.assetid: 146bf10a-c898-4676-a2a1-673fb1cee7a2
author: rothja
ms.author: jroth
ms.openlocfilehash: f67d5742c5de1f806194090ebe366693cc8c9457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482144"
---
# <a name="syssysconfigures-transact-sql"></a>sys.sysconfigures (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada opção de configuração definida por um usuário. **sysconfigures** contém as opções de configuração que são definidas antes da inicialização mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , além de quaisquer opções de configuração dinâmica definidas desde então.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**value**|**int**|Valor modificável pelo usuário para a variável. Isso só será usado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] se RECONFIGURE tiver sido executado.|  
|**config**|**int**|Número variável de configuração.|  
|**mente**|**nvarchar(255)**|Explicação da opção de configuração.|  
|**status**|**smallint**|Bitmap que indica o status da opção. Os possíveis valores incluem os seguintes:<br /><br /> 0 = Estático. A definição entra em vigor quando o servidor é reinicializado.<br /><br /> 1 = Dinâmico. A variável é implementada quando a instrução RECONFIGURE é executada.<br /><br /> 2 = Avançado. A variável é exibida somente quando a **opção Mostrar opções avançadas** está definida. A definição entra em vigor quando o servidor é reinicializado.<br /><br /> 3 = Dinâmico e avançado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
