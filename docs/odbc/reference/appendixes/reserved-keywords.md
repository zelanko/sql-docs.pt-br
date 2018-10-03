---
title: Palavras-chave reservadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC function call reserved words [ODBC]
- reserved keywords [ODBC]
ms.assetid: 8eeede59-a828-44bf-866c-1ca9a77a2c5e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d77d6632d689a1f169c61cb636e3bc89a900419
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626334"
---
# <a name="reserved-keywords"></a>Palavras-chave reservadas
As palavras seguintes são reservadas para uso em chamadas de função ODBC. Essas palavras não restringem a gramática SQL mínima; No entanto, para garantir a compatibilidade com drivers que dão suporte à gramática principal do SQL, aplicativos devem evitar usar qualquer uma dessas palavras-chave. O #**definir** valor SQL_ODBC_KEYWORDS contém uma lista separada por vírgulas dessas palavras-chave.  
  
|||  
|-|-|  
|ABSOLUTE|IS|  
|ACTION|ISOLATION|  
|ADA|JOIN|  
|ADD|KEY|  
|ALL|LANGUAGE|  
|ALLOCATE|LAST|  
|ALTER|LEADING|  
|AND|LEFT|  
|ANY|LEVEL|  
|ARE|LIKE|  
|AS|LOCAL|  
|ASC|LOWER|  
|ASSERTION|MATCH|  
|AT|MAX|  
|AUTHORIZATION|MIN|  
|AVG|MINUTE|  
|BEGIN|MODULE|  
|BETWEEN|MONTH|  
|BIT|NAMES|  
|FUNÇÃO BIT_LENGTH|NATIONAL|  
|BOTH|NATURAL|  
|BY|NCHAR|  
|CASCADE|NEXT|  
|CASCADED|Não|  
|CASE|Nenhuma|  
|CAST|NOT|  
|CATALOG|NULL|  
|CHAR|NULLIF|  
|CHAR_LENGTH|NUMERIC|  
|CHARACTER|FUNÇÃO OCTET_LENGTH|  
|CHARACTER_LENGTH|OF|  
|CHECK|ON|  
|CLOSE|ONLY|  
|COALESCE|OPEN|  
|COLLATE|OPÇÃO|  
|COLLATION|OU|  
|COLUMN|ORDER|  
|COMMIT|OUTER|  
|CONNECT|OUTPUT|  
|CONNECTION|SOBREPOSIÇÕES|  
|CONSTRAINT|PAD|  
|CONSTRAINTS|PARTIAL|  
|CONTINUE|PASCAL|  
|CONVERT|POSIÇÃO|  
|CORRESPONDING|PRECISION|  
|COUNT|PREPARE|  
|CREATE|PRESERVE|  
|CROSS|PRIMARY|  
|CURRENT|PRIOR|  
|CURRENT_DATE|PRIVILEGES|  
|CURRENT_TIME|PROCEDURE|  
|CURRENT_TIMESTAMP|PUBLIC|  
|CURRENT_USER|READ|  
|CURSOR|real|  
|DATE|REFERENCES|  
|DAY|RELATIVE|  
|DEALLOCATE|RESTRICT|  
|DEC|REVOKE|  
|DECIMAL|RIGHT|  
|DECLARE|ROLLBACK|  
|DEFAULT|ROWS|  
|DEFERRABLE|SCHEMA|  
|DEFERRED|SCROLL|  
|Delete (excluir)|SECOND|  
|DESC|SECTION|  
|DESCRIBE|SELECT|  
|DESCRIPTOR|SESSION|  
|DIAGNOSTICS|SESSION_USER|  
|DISCONNECT|SET|  
|DISTINCT|SIZE|  
|DOMAIN|SMALLINT|  
|DOUBLE|SOME|  
|DROP|SPACE|  
|ELSE|SQL|  
|END|SQLCA|  
|END-EXEC|SQLCODE|  
|ESCAPE|SQLERROR|  
|EXCEPT|SQLSTATE|  
|EXCEPTION|SQLWARNING|  
|EXEC|SUBSTRING|  
|Execute|SUM|  
|EXISTS|SYSTEM_USER|  
|EXTERNAL|TABLE|  
|EXTRACT|TEMPORARY|  
|FALSE|THEN|  
|FETCH|TIME|  
|FIRST|timestamp|  
|FLOAT|TIMEZONE_HOUR|  
|FOR|TIMEZONE_MINUTE|  
|FOREIGN|TO|  
|FORTRAN|TRAILING|  
|FOUND|TRANSACTION|  
|FROM|TRANSLATE|  
|FULL|TRANSLATION|  
|GET|TRIM|  
|GLOBAL|TRUE|  
|GO|UNION|  
|GOTO|UNIQUE|  
|GRANT|UNKNOWN|  
|GROUP|UPDATE|  
|HAVING|UPPER|  
|HOUR|USAGE|  
|IDENTITY|Usuário|  
|IMMEDIATE|USING|  
|IN|Value|  
|INCLUDE|VALUES|  
|INDEX|VARCHAR|  
|INDICATOR|VARYING|  
|INITIALLY|VIEW|  
|INNER|WHEN|  
|INPUT|WHENEVER|  
|INSENSITIVE|WHERE|  
|INSERT|com|  
|INT|WORK|  
|INTEGER|WRITE|  
|INTERSECT|YEAR|  
|INTERVAL|ZONE|  
|INTO||
