---
description: sp_linkedservers (Transact-SQL)
title: sp_linkedservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_linkedservers
- sp_linkedservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_linkedservers
ms.assetid: d8f82f78-8a1f-4831-bcee-7c36c6e7dfbb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a998aa0bb5deab2b29b2133de95e0b3169602bb7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546008"
---
# <a name="sp_linkedservers-transact-sql"></a>sp_linkedservers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna a lista de servidores vinculados definida no servidor local.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_linkedservers  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**SRV_NAME**|**sysname**|Nome do servidor vinculado.|  
|**SRV_PROVIDERNAME**|**nvarchar (** 128 **)**|Nome amigável do provedor de OLE DB que gerencia o acesso ao servidor vinculado especificado.|  
|**SRV_PRODUCT**|**nvarchar (** 128 **)**|Nome de produto do servidor vinculado.|  
|**SRV_DATASOURCE**|**nvarchar (** 4000 **)**|Propriedade da fonte de dados OLE DB que corresponde ao servidor vinculado especificado.|  
|**SRV_PROVIDERSTRING**|**nvarchar (** 4000 **)**|Propriedade de cadeia de caracteres do provedor OLE DB que corresponde ao servidor vinculado.|  
|**SRV_LOCATION**|**nvarchar (** 4000 **)**|Propriedade de local OLE DB que corresponde ao servidor vinculado especificado.|  
|**SRV_CAT**|**sysname**|Propriedade de catálogo OLE DB que corresponde ao servidor vinculado especificado.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_catalogs ](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_column_privileges ](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_columns_ex ](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_foreignkeys ](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_indexes ](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_primarykeys ](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_table_privileges ](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_tables_ex ](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de consultas distribuídas &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
