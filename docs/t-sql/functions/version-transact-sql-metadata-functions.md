---
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ed3eab701a8edbbf118e228bd90080a61a214b32
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67927436"
---
# <a name="version---transact-sql-metadata-functions"></a>Versão – Funções de metadados do Transact-SQL
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 Retorna a versão do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] executada no dispositivo.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="general-remarks"></a>Comentários gerais  
Um nome de tabela deve ser especificado em uma cláusula [FROM](../../t-sql/queries/from-transact-sql.md) para que essa função retorne resultados. Uma linha de resultados será retornada para cada linha no conjunto de resultados da consulta; use [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) para limitar o número de linhas retornadas.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o número de versão.  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>Consulte Também 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
