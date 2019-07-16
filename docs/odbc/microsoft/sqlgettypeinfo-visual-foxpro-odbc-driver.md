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
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898625"
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
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Inteiro|  
|SQL_LONGVARBINARY|Memorando (binário)|  
|SQL_LONGVARCHAR|Memorando|  
|SQL_NUMERIC|Numérico *, moeda, Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Inteiro|  
|SQL_TIME|Sem suporte. Não há nenhum Visual FoxPro *tempo* tipo.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Inteiro|  
|SQL_VARBINARY|Memorando (binário) *, geral|  
|SQL_VARCHAR|Caractere|  
  
 \* Tipo de padrão  
  
 Para obter mais informações sobre tipos de dados do Visual FoxPro, consulte [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obter mais informações sobre essa função, consulte [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) na *referência do programador de ODBC*.
