---
description: Conversões de tipo de dados
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
ms.openlocfilehash: 92c31cb12c7bb02cf8e108251ae5ebd6f12aed5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429338"
---
# <a name="data-type-conversions"></a>Conversões de tipo de dados
Os dados podem ser convertidos de um tipo para outro em uma das quatro vezes: quando os dados são transferidos de uma variável de aplicativo para outra (C para C), quando os dados em uma variável de aplicativo são enviados a um parâmetro de instrução (C para SQL), quando os dados em uma coluna de conjunto de resultados são retornados em uma variável de aplicativo (SQL para SQL), e quando os dados são transferidos de uma coluna de fonte de dados para outra (SQL to  
  
 Qualquer conversão que ocorre quando os dados são transferidos de uma variável de aplicativo para outra está fora do escopo deste documento.  
  
 Quando um aplicativo associa uma variável a um parâmetro de instrução ou coluna do conjunto de resultados, o aplicativo especifica implicitamente uma conversão de tipo de dados em sua escolha do tipo de dados da variável do aplicativo. Por exemplo, suponha que uma coluna contenha dados inteiros. Se o aplicativo associar uma variável de inteiro à coluna, ele especifica que nenhuma conversão foi feita; Se o aplicativo associar uma variável de caractere à coluna, ele especificará que os dados serão convertidos de inteiro em caractere.  
  
 O ODBC define como os dados são convertidos entre cada tipo de dados SQL e C. Basicamente, o ODBC dá suporte a todas as conversões razoáveis, como Character para Integer e Integer para float e não oferece suporte a conversões mal definidas, como float to date. Os drivers são necessários para dar suporte a todas as conversões para cada tipo de dados SQL ao qual dão suporte. Para obter uma lista completa de conversões entre os tipos de dados SQL e C, consulte [convertendo dados de tipos de dados SQL para c](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e [convertendo dados dos tipos de dados c para SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice D: tipos de dados.  
  
 O ODBC também define uma função escalar para converter dados de um tipo de dados SQL para outro. A função **Convert** escalar é mapeada pelo driver para a função escalar subjacente ou funções definidas para executar conversões na fonte de dados. Como essa função é mapeada para funções específicas de DBMS, o ODBC não define como essas conversões funcionam ou quais conversões devem ter suporte. Um aplicativo descobre quais conversões são suportadas por um determinado driver e fonte de dados por meio das opções de SQL_CONVERT no **SQLGetInfo**. Para obter mais informações sobre a função **Convert** escalar, consulte [sequências de escape em ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e função de [conversão de tipo de dados explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
