---
title: SqlgetTypeinfo (visual FoxPro ODBC Driver) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299516"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Retorna informações sobre os tipos de dados suportados por uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL. A tabela a seguir lista os tipos de dados Do DBC e o tipo de dados Visual FoxPro correspondente.  
  
|Tipo ODBC|Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|Sem suporte. Não há nenhum tipo Visual FoxPro de 64 bits.|  
|SQL_BIT|Lógico|  
|SQL_CHAR|Caractere|  
|SQL_DATE|Data|  
|SQL_DECIMAL|Numérico|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Integer|  
|SQL_LONGVARBINARY|Memorando (Binário)|  
|SQL_LONGVARCHAR|Memo|  
|SQL_NUMERIC|Numérico*, Moeda, Flutuação|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Integer|  
|SQL_TIME|Sem suporte. Não há nenhum tipo *de tempo* Visual FoxPro.|  
|SQL_TIMESTAMP|Datetime|  
|SQL_TINYINT|Integer|  
|SQL_VARBINARY|Memorando (Binário)*, Geral|  
|SQL_VARCHAR|Caractere|  
  
 *Tipo padrão  
  
 Para obter mais informações sobre os tipos de dados do Visual FoxPro, consulte [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obter mais informações sobre essa função, consulte [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) na *referência do programador ODBC*.
