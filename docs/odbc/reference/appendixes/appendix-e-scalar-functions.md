---
title: 'Apêndice E: funções escalares | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb5f16485312979e9fb2ad6b3a95dacb79b695d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996173"
---
# <a name="appendix-e-scalar-functions"></a>Apêndice E: Funções escalares
O ODBC especifica os seguintes tipos de funções escalares, com informações detalhadas sobre cada um desses tipos de função fornecidos nas seções correspondentes deste apêndice. As descrições de função incluem a sintaxe associada.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Funções de cadeia de caracteres](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funções numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funções de hora, data e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funções do sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Função de conversão de tipo de dados explícitos](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Função CAST do SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 O ODBC não exige um tipo de dados para valores de retorno de funções escalares porque as funções geralmente são específicas da fonte de dados. Os aplicativos devem usar a função CONVERT escalar sempre que possível para forçar a conversão do tipo de dados.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funções escalares ODBC e SQL-92  
 As tabelas neste apêndice incluem funções que foram adicionadas no ODBC 3,0 para serem alinhadas com o SQL-92. Essas funções adicionadas a um tipo específico de função escalar, conforme definido no ODBC, são indicadas em cada seção.  
  
 ODBC e SQL-92 classificam suas funções escalares de forma diferente. O ODBC classifica funções escalares por tipo de argumento; O SQL-92 os classifica por valor de retorno. Por exemplo, a função EXTRACT é classificada como uma função timedate pelo ODBC, porque o argumento Extract-Field é uma palavra-chave DateTime e o argumento Extract-Source é uma expressão DateTime ou Interval. O SQL-92, por outro lado, classifica a EXTRAção como uma função escalar numérica, pois o valor de retorno é numérico.  
  
 Um aplicativo pode determinar a quais funções escalares um driver dá suporte chamando **SQLGetInfo**. Os tipos de informações são incluídos para as classificações de ODBC e SQL-92 de funções escalares. Como essas classificações são diferentes, o suporte para algumas funções escalares pode ser indicado em tipos de informações que não correspondem ao ODBC e ao SQL-92. Por exemplo, o suporte para extrair em ODBC é indicado pelo tipo de informação SQL_TIMEDATE_FUNCTIONS; o suporte para EXTRAção em SQL-92, por outro lado, é indicado pelo tipo de informação SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
