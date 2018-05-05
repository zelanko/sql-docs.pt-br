---
title: Conversões de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04dd1614247067e3920958f9d1733a3ef91d792c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-conversions"></a>Conversões de tipo de dados
Dados podem ser convertidos de um tipo para outro em um dos quatro vezes: quando dados são transferidos da variável de um aplicativo para outro (C para C), quando dados em uma variável de aplicativo são enviados para um parâmetro de instrução (C para SQL), quando os dados em uma coluna do conjunto de resultados são retornados no uma variável de aplicativo (SQL para C), e quando os dados são transferidos da coluna de origem de dados para outro (SQL para SQL).  
  
 Qualquer conversão que ocorre quando dados são transferidos da variável de um aplicativo para outro está fora do escopo deste documento.  
  
 Quando um aplicativo associar uma variável para um parâmetro de coluna ou instrução de conjunto de resultados, o aplicativo especifica implicitamente uma conversão de tipo de dados de sua escolha do tipo de dados da variável de aplicativo. Por exemplo, suponha que uma coluna contém dados de número inteiro. Se o aplicativo associa uma variável de inteiro para a coluna, ela especifica que nenhuma conversão ser feito; Se o aplicativo associa uma variável de caractere para a coluna, especifica que os dados de ser convertida de inteiro em caractere.  
  
 ODBC define como os dados são convertidos entre cada tipo de dados SQL e C. Basicamente, ODBC oferece suporte a todas as conversões razoáveis, como caractere de inteiro e inteiro em flutuante e não oferece suporte a conversões bem-definido, como float para data. Drivers são necessários para dar suporte a todas as conversões para cada tipo de dados SQL que dão suporte. Para obter uma lista completa das conversões entre tipos de dados SQL e C, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) e [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice d: os tipos de dados.  
  
 O ODBC também define uma função escalar para converter dados de um tipo de dados do SQL para outro. O **converter** função escalar é mapeada pelo driver para a função escalar subjacente ou funções definidas para realizar conversões na fonte de dados. Porque essa função é mapeada para funções específicas de DBMS, ODBC não define como funcionam essas conversões ou quais conversões devem ter suporte. Um aplicativo descobre que conversões são suportados por uma determinado driver e fonte de dados através das opções de SQL_CONVERT no **SQLGetInfo**. Para obter mais informações sobre o **converter** função escalar, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [função de conversão de tipo de dados explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
