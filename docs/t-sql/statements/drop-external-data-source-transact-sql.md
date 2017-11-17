---
title: REMOVER a fonte de dados externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6657a09ca9f3e1e700e078d707c92c495e444d42
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-data-source-transact-sql"></a>FONTE de dados externa DROP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Remove uma fonte de dados externa do PolyBase.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *external_data_source_name*  
 O nome da fonte de dados externa para descartar.  
  
## <a name="metadata"></a>Metadados  
 Para exibir uma lista de dados externos fontes usam a exibição do sistema sys.external_data_sources.  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>Permissões  
 Requer ALTER qualquer fonte de dados externa.  
  
## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado no objeto de fonte de dados externa.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Descartar uma fonte de dados externa não remove os dados externos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-basic-syntax"></a>A. Usando a sintaxe básica  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  


