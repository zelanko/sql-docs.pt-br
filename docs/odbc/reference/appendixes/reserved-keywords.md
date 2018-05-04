---
title: Palavras-chave reservadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC function call reserved words [ODBC]
- reserved keywords [ODBC]
ms.assetid: 8eeede59-a828-44bf-866c-1ca9a77a2c5e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f62e74939ab7be81696f90b39af85239332a88c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keywords"></a>Palavras-chave reservadas
As palavras seguintes são reservadas para uso em chamadas de função ODBC. Essas palavras não restringem a gramática SQL mínima; No entanto, para garantir a compatibilidade com drivers que oferecem suporte à gramática SQL principal, aplicativos devem evitar usar qualquer uma dessas palavras-chave. O #**definir** valor SQL_ODBC_KEYWORDS contém uma lista separada por vírgulas destas palavras-chave.  
  
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
|CHARACTER|OCTET_LENGTH|  
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
|CURSOR|REAL|  
|DATE|REFERENCES|  
|DAY|RELATIVE|  
|DEALLOCATE|RESTRICT|  
|DEC|REVOKE|  
|DECIMAL|RIGHT|  
|DECLARE|ROLLBACK|  
|DEFAULT|ROWS|  
|DEFERRABLE|SCHEMA|  
|DEFERRED|SCROLL|  
|DELETE|SECOND|  
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
|FIRST|TIMESTAMP|  
|FLOAT|TIMEZONE_HOUR|  
|FOR|TIMEZONE_MINUTE|  
|FOREIGN|TO|  
|FORTRAN|TRAILING|  
|FOUND|TRANSACTION|  
|FROM|TRADUZIR|  
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
|IN|VALUE|  
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
