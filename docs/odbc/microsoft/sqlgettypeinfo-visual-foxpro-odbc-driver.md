---
title: SQLGetTypeInfo (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05cc6dc2647b5297b8d7176cd4bc70261b78cb71
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181417"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 1  
  
 Retorna informações sobre os tipos de dados compatíveis com uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL. A tabela a seguir lista os tipos de dados ODBC e o tipo de dados correspondente do Visual FoxPro.  
  
|Tipo de ODBC|Tipo do Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|Sem suporte. Não há nenhum tipo de 64 bits do Visual FoxPro.|  
|SQL_BIT|Logical|  
|SQL_CHAR|Caractere|  
|SQL_DATE|data|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memorando (binário)|  
|SQL_LONGVARCHAR|Memorando|  
|SQL_NUMERIC|Numérico *, moeda, Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Sem suporte. Não há nenhum Visual FoxPro *tempo* tipo.|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memorando (binário) *, geral|  
|SQL_VARCHAR|Caractere|  
  
 * Tipo de padrão  
  
 Para obter mais informações sobre tipos de dados do Visual FoxPro, consulte [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obter mais informações sobre essa função, consulte [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) na *referência do programador de ODBC*.
