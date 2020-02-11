---
title: sys. sysdepends (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysdepends_TSQL
- sysdepends
- sysdepends_TSQL
- sys.sysdepends
dev_langs:
- TSQL
helpviewer_keywords:
- sysdepends system table
- sys.sysdepends compatibility view
ms.assetid: f9c182cb-386f-4e72-859f-9f1115b389f9
author: rothja
ms.author: jroth
ms.openlocfilehash: 5d928926294bb3e80f860a535a266b5c106e3f18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053502"
---
# <a name="syssysdepends-transact-sql"></a>sys.sysdepends (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações de dependência entre objetos (exibições, procedimentos e gatilhos) no banco de dados e os objetos (tabelas, exibições e procedimentos) contidos em suas definições.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|ID do objeto.|  
|**depid**|**int**|ID de objeto dependente.|  
|**number**|**smallint**|Número de procedimento.|  
|**depnumber**|**smallint**|Número de procedimento dependente.|  
|**Estado**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deptype**|**tinyint**|Identifica o tipo de objeto dependente:<br /><br /> 0 = Objeto ou coluna (somente referências não associadas a esquema<br /><br /> 1 = Objeto ou coluna (somente referências associadas a esquema)|  
|**depdbid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**depsiteid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selall**|**bit**|1 = O objeto é usado em uma instrução SELECT *.<br /><br /> 0 = Não.|  
|**resultobj**|**bit**|1 = O objeto está sendo atualizado.<br /><br /> 0 = Não.|  
|**readobj**|**bit**|1 = O objeto está sendo lido.<br /><br /> 0 = Não.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_depends](../../relational-databases/system-stored-procedures/sp-depends-transact-sql.md)   
 [sys. sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
