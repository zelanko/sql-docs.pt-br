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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305208"
---
# <a name="data-type-conversions"></a>Conversões de tipo de dados
Os dados podem ser convertidos de um tipo para outro em uma das quatro vezes: quando os dados são transferidos de uma variável de aplicativo para outra (C para C), quando os dados em uma variável de aplicativo são enviados para um parâmetro de declaração (C para SQL), quando os dados em uma coluna de conjunto de resultados são retornados em uma variável de aplicativo (SQL para C), e quando os dados são transferidos de uma coluna de origem de dados para outra (SQL para SQL).  
  
 Qualquer conversão que ocorra quando os dados são transferidos de uma variável de aplicativo para outra está fora do escopo deste documento.  
  
 Quando um aplicativo vincula uma variável a uma coluna de conjunto de resultados ou parâmetro de declaração, o aplicativo especifica implicitamente uma conversão de tipo de dados na escolha do tipo de dados da variável de aplicação. Por exemplo, suponha que uma coluna contenha dados inteiros. Se o aplicativo vincular uma variável inteira à coluna, ele especificará que nenhuma conversão será feita; se o aplicativo vincular uma variável de caractere à coluna, ele especifica rá que os dados sejam convertidos de inteiro para caractere.  
  
 O ODBC define como os dados são convertidos entre cada tipo de dados SQL e C. Basicamente, o ODBC suporta todas as conversões razoáveis, como personagem para inteiro e inteiro para flutuar, e não suporta conversões mal definidas, como flutuar até o momento. Os drivers são necessários para suportar todas as conversões para cada tipo de dados SQL que eles suportam. Para obter uma lista completa de conversões entre os tipos de dados SQL e C, consulte [Conversão de dados de SQL para C Tipos de dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e conversão de dados de C para Tipos de Dados [SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no apêndice D: Tipos de dados.  
  
 O ODBC também define uma função escalar para converter dados de um tipo de dados SQL para outro. A função **escalar CONVERT** é mapeada pelo driver para a função escalar subjacente ou funções definidas para executar conversões na fonte de dados. Como essa função é mapeada para funções específicas do DBMS, o ODBC não define como essas conversões funcionam ou quais conversões devem ser suportadas. Um aplicativo descobre quais conversões são suportadas por um determinado driver e fonte de dados através das opções de SQL_CONVERT no **SQLGetInfo**. Para obter mais informações sobre a função **ESCALAR CONVERT,** consulte [Seqüências de escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [na função de conversão explícita do tipo de dados](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
