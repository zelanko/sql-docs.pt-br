---
title: 'Apêndice E: Funções Escalares | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292486"
---
# <a name="appendix-e-scalar-functions"></a>Apêndice E: Funções escalares
A ODBC especifica os seguintes tipos de funções escalares, com informações detalhadas sobre cada um desses tipos de função fornecidas nas seções correspondentes deste apêndice. As descrições da função incluem sintaxe associada.  
  
 Este apêndice contém os seguintes tópicos.  
  
-   [Funções de corda](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funções numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funções de hora, data e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funções do sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Função de conversão de tipo de dados explícitos](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Função CAST do SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 O ODBC não determina um tipo de dados para valores de retorno de funções escalares porque as funções são muitas vezes específicas da fonte de dados. Os aplicativos devem usar a função ESCALAR CONVERT sempre que possível para forçar a conversão do tipo de dados.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funções Escalares ODBC e SQL-92  
 As tabelas neste apêndice incluem funções que foram adicionadas no ODBC 3.0 para se alinhar em SQL-92. Essas funções adicionadas para um determinado tipo de função escalar, como definido no ODBC, são indicadas em cada seção.  
  
 ODBC e SQL-92 classificam suas funções escalares de forma diferente. A ODBC classifica funções escalares por tipo de argumento; O SQL-92 classifica-os pelo valor de retorno. Por exemplo, a função EXTRACT é classificada como uma função de data de data por ODBC, porque o argumento extrato-campo é uma palavra-chave de data-hora e o argumento da fonte de extração é uma expressão de data ou intervalo. SQL-92, por outro lado, classifica EXTRACT como uma função escalar numérica, porque o valor de retorno é um numérico.  
  
 Um aplicativo pode determinar quais funções escalares um driver suporta chamando **SQLGetInfo**. Os tipos de informações estão incluídos tanto para o ODBC quanto para classificações SQL-92 de funções escalares. Como essas classificações são diferentes, o suporte para algumas funções escalares pode ser indicado em tipos de informações que não correspondem ao ODBC e ao SQL-92. Por exemplo, o suporte ao EXTRACT no ODBC é indicado pelo SQL_TIMEDATE_FUNCTIONS tipo de informação; o suporte para EXTRACT no SQL-92, por outro lado, é indicado pelo SQL_SQL92_NUMERIC_VALUE_FUNCTIONS tipo de informação.
