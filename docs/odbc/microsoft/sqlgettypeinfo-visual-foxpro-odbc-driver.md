---
title: SQLGetTypeInfo (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23db0350f0f7271f85e2bc5c6a9e6c8767443a85
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "81299516"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Retorna informações sobre os tipos de dados com suporte por uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL. A tabela a seguir lista os tipos de dados ODBC e o tipo de dados do Visual FoxPro correspondente.  
  
|Tipo de ODBC|Tipo do Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|Sem suporte. Não há nenhum tipo de Visual FoxPro de 64 bits.|  
|SQL_BIT|Lógico|  
|SQL_CHAR|Caractere|  
|SQL_DATE|Data|  
|SQL_DECIMAL|Numérico|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memorando (binário)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numérico *, moeda, float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Sem suporte. Não há nenhum tipo de *tempo* do Visual FoxPro.|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memorando (binário) *, geral|  
|SQL_VARCHAR|Caractere|  
  
 * Tipo padrão  
  
 Para obter mais informações sobre os tipos de dados do Visual FoxPro, consulte [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obter mais informações sobre essa função, consulte [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) na *referência do programador de ODBC*.
