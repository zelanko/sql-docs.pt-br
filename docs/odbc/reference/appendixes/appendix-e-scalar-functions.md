---
title: 'Apêndice e: Funções escalares | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 71c80efdb2f4a87537d472ee4b6dc6bdc65af70f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540515"
---
# <a name="appendix-e-scalar-functions"></a>Apêndice e: Funções escalares
ODBC Especifica os seguintes tipos de funções escalares, com informações detalhadas sobre cada um desses tipos de função fornecidos nas seções correspondentes neste apêndice. As descrições de função incluem sintaxe associada.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Funções de cadeia de caracteres](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funções numéricas](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funções de hora, data e intervalo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funções do Sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Função de conversão de tipo de dados explícitos](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Função CAST do SQL-92](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC não exige um tipo de dados para valores de retorno de funções escalares, como as funções são geralmente específico de fonte de dados. Aplicativos devem usar a função escalar CONVERT sempre que possível forçar a conversão de tipo de dados.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funções escalares ODBC e SQL-92  
 As tabelas neste apêndice incluem funções que foram adicionadas no ODBC 3.0 para se alinhar com o SQL-92. Essas funções adicionadas para um determinado tipo de função escalar, conforme definido no ODBC, são indicadas em cada seção.  
  
 ODBC e SQL-92 classificam suas funções escalares de maneira diferente. ODBC classifica as funções escalares por tipo de argumento; SQL-92 classifica-os pelo valor de retorno. Por exemplo, a função EXTRACT é classificada como uma função timedate por ODBC, porque o argumento de extrair campo é uma palavra-chave de data e hora e o argumento de origem de extração é uma expressão de data e hora ou intervalo. SQL-92, classifica por outro lado, EXTRAIR como uma função escalar numérica, porque o valor de retorno é um numérico.  
  
 Um aplicativo pode determinar quais um driver oferece suporte ao chamar as funções escalares **SQLGetInfo**. Tipos de informações são incluídos para ODBC e SQL-92 classificações de funções escalares. Como essas classificações são diferentes, o suporte para algumas funções escalares pode ser indicado em tipos de informações que não correspondem a ODBC e SQL-92. Por exemplo, suporte para EXTRAÇÃO no ODBC é indicado pelo tipo de informações de SQL_TIMEDATE_FUNCTIONS; suporte para EXTRAÇÃO no SQL-92, por outro lado, é indicado por tipo de informação SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
