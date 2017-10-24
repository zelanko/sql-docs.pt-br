---
title: "VERSÃO (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1905ef3b0f31e91d6cec00c0314770b7686e8c51
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="version---transact-sql-metadata-functions"></a>Versão - Transact SQL metadados funções
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 Retorna a versão do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] executado no dispositivo.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="general-remarks"></a>Comentários gerais  
Um nome de tabela deve ser especificado em uma [FROM](../../t-sql/queries/from-transact-sql.md) cláusula para esta função retornar resultados. Uma linha de resultados será retornada para cada linha no conjunto de resultados de consulta; Use [superior (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) para limitar o número de linhas retornadas.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o número de versão.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>Consulte também 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  

