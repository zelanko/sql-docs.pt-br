---
title: "Usos de dados de catálogo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c77be1b431a7f7e2cf8c040df7ceb9a9feaf321a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="uses-of-catalog-data"></a>Usos de dados do catálogo
Aplicativos usam dados de catálogo em uma variedade de maneiras. Aqui estão alguns usos comuns:  
  
-   **Construindo instruções SQL em tempo de execução.** Aplicativos verticais, como um aplicativo de entrada de pedidos, contêm instruções de SQL embutido. As tabelas e colunas que são usadas pelo aplicativo corrigidas antecipadamente, assim como as instruções que acessam essas tabelas. Por exemplo, um aplicativo de entrada de ordem geralmente contém um único com parâmetros **inserir** instrução para adicionar novos pedidos no sistema.  
  
     Aplicativos genéricos, como um programa de planilha que usa ODBC para recuperar dados, geralmente construir instruções SQL em tempo de execução com base na entrada do usuário. Esse aplicativo pode exigir que o usuário digitar os nomes das tabelas e colunas a serem usadas. No entanto, seria mais fácil para o usuário se o aplicativo exibido listas de tabelas e colunas das quais o usuário pode fazer seleções. Para criar essas listas, o aplicativo deve chamar o **SQLTables** e **SQLColumns** funções de catálogo.  
  
-   **Construindo instruções SQL durante o desenvolvimento.** Ambientes de desenvolvimento de aplicativo normalmente permite que o programador a criar consultas de banco de dados durante o desenvolvimento de um programa. As consultas são embutidos em código no aplicativo que está sendo criado.  
  
     Também podem usar esses ambientes **SQLTables** e **SQLColumns** para criar listas das quais o programador pode fazer seleções. Também podem usar esses ambientes **SQLPrimaryKeys** e **SQLForeignKeys** para determinar automaticamente e mostrar relações entre as tabelas selecionadas e usar **SQLStatistics** para determinar e realçar campos indexados para o programador possa criar consultas eficientes.  
  
-   **Construindo cursores.** Um aplicativo, o driver ou o middleware que fornece um mecanismo de cursor rolável use **SQLSpecialColumns** para determinar qual coluna ou colunas que identificam exclusivamente uma linha. O programa foi possível construir um *keyset* que contém os valores dessas colunas para cada linha que foi buscada. Quando o aplicativo rola para a linha, ele seria usar esses valores para buscar os dados mais recentes para a linha. Para obter mais informações sobre cursores roláveis e conjuntos de chaves, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).
