---
title: Conversões de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 590bd488ae87e8e871837c3055a3225794850d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077010"
---
# <a name="data-type-conversions"></a>Conversões de tipo de dados
Dados podem ser convertidos de um tipo para outro em um dos quatro vezes: quando dados são transferidos da variável de um aplicativo para outro (C para C), quando os dados em uma variável de aplicativo são enviados para um parâmetro de instrução (C to SQL), quando os dados em uma coluna do conjunto de resultados são retornados no uma variável de aplicativo (SQL para C), e quando os dados são transferidos da coluna de origem de dados para outro SQL (SQL).  
  
 Qualquer conversão que ocorre quando dados são transferidos da variável de um aplicativo para outro está fora do escopo deste documento.  
  
 Quando um aplicativo está associado a uma variável para um parâmetro de coluna ou a instrução de conjunto de resultados, o aplicativo especifica implicitamente uma conversão de tipo de dados de sua escolha do tipo de dados da variável de aplicativo. Por exemplo, suponha que uma coluna contém dados de inteiro. Se o aplicativo associar uma variável de inteiro para a coluna, ela especifica que nenhuma conversão a ser feita; Se o aplicativo associar uma variável de caractere para a coluna, ela especifica que os dados de ser convertido de inteiro em caractere.  
  
 ODBC define como os dados são convertidos entre cada tipo de dados SQL e C. Basicamente, o ODBC dá suporte a todas as conversões razoáveis, como o caractere para inteiro e inteiro em float e não oferece suporte a conversões mal definidas, como float para data. Drivers são necessários para dar suporte a todas as conversões para cada tipo de dados SQL que dar suporte a eles. Para obter uma lista completa de conversões entre tipos de dados SQL e C, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e [Convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice d: Tipos de dados.  
  
 O ODBC também define uma função escalar para converter dados de um tipo de dados SQL para outro. O **converter** função escalar é mapeada pelo driver para a função escalar subjacente ou funções definidas para executar conversões na fonte de dados. Como essa função é mapeada para funções específicas do DBMS, ODBC não definem como funcionam essas conversões ou conversões de quais devem ter suporte. Um aplicativo descobre quais conversões são suportadas por uma fonte de dados e driver específica por meio das opções de SQL_CONVERT no **SQLGetInfo**. Para obter mais informações sobre o **converter** função escalar, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [função de conversão de tipo de dados explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
