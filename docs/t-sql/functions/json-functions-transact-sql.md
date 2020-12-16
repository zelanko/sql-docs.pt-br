---
description: Funções JSON (Transact-SQL)
title: Funções JSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017
ms.openlocfilehash: c55ffdeec513c71c89cd5ed4bb8ef9f6e88e7330
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478607"
---
# <a name="json-functions-transact-sql"></a>Funções JSON (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

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
