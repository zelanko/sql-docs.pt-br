---
title: Funções JSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5b83e6f6eefce1cf56b71e7d433dca19cb4575d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109424"
---
# <a name="json-functions-transact-sql"></a>Funções JSON (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Use as funções descritas nas páginas nesta seção para validar ou alterar o texto JSON ou para extrair valores simples ou complexos.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[ISJSON](../../t-sql/functions/isjson-transact-sql.md)|Testa se uma cadeia de caracteres contém um JSON válido.|  
|[JSON_VALUE](../../t-sql/functions/json-value-transact-sql.md)|Extrai um valor escalar de uma cadeia de caracteres JSON.|  
|[JSON_QUERY](../../t-sql/functions/json-query-transact-sql.md)|Extrai um objeto ou uma matriz de uma cadeia de caracteres JSON.|  
|[JSON_MODIFY](../../t-sql/functions/json-modify-transact-sql.md)|Atualiza o valor de uma propriedade em uma cadeia de caracteres JSON e retorna a cadeia de caracteres JSON atualizada.|

 Para obter mais informações sobre o suporte interno para JSON no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md).  

## <a name="see-also"></a>Consulte Também

 - [Validar, consultar e alterar dados JSON com funções internas &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)
 - [Expressões de caminho JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)
 - [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
