---
title: Usos de dados de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b75d59d8fc28e364f5826d95e7fc50cb6afda7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312527"
---
# <a name="uses-of-catalog-data"></a>Usos de dados do catálogo
Aplicativos usam dados de catálogo em uma variedade de formas. Aqui estão alguns usos comuns:  
  
-   **Construindo instruções SQL em tempo de execução.** Aplicativos verticais, como um aplicativo de entrada de pedidos, contenham instruções de SQL embutido em código. As tabelas e colunas que são usadas pelo aplicativo são fixas antecipadamente, assim como as instruções que acessam essas tabelas. Por exemplo, um aplicativo de entrada de pedidos geralmente contém um único parametrizada **inserir** instrução para adicionar novos pedidos ao sistema.  
  
     Aplicativos genéricos, como um programa de planilha que usa o ODBC para recuperar dados, muitas vezes construir instruções SQL em tempo de execução com base na entrada do usuário. Esse aplicativo pode exigir que o usuário digitar os nomes das tabelas e colunas a serem usadas. No entanto, seria mais fácil para o usuário se o aplicativo exibido listas de tabelas e colunas do qual o usuário pode fazer seleções. Para criar essas listas, o aplicativo deve chamar o **SQLTables** e **SQLColumns** funções de catálogo.  
  
-   **Construindo instruções SQL durante o desenvolvimento.** Ambientes de desenvolvimento de aplicativos normalmente permitem que o programador a criar consultas de banco de dados ao desenvolver um programa. As consultas, em seguida, são embutidos em código no aplicativo que está sendo criado.  
  
     Nesses ambientes também pode usar **SQLTables** e **SQLColumns** para criar listas na qual o programador pode fazer seleções. Nesses ambientes também podem usar **SQLPrimaryKeys** e **SQLForeignKeys** para determinar automaticamente e mostrar as relações entre as tabelas selecionadas e usar **SQLStatistics** para determinar e realçar campos indexados para que o programador possa criar consultas eficientes.  
  
-   **Construção de cursores.** Pode usar um aplicativo, driver ou middleware que fornece um mecanismo de cursor rolável **SQLSpecialColumns** para determinar qual coluna ou colunas identificam exclusivamente uma linha. O programa poderia criar uma *keyset* que contém os valores dessas colunas para cada linha que foi buscada. Quando o aplicativo rola de volta para a linha, ele usaria esses valores para buscar os dados mais recentes para a linha. Para obter mais informações sobre cursores roláveis e os conjuntos de chaves, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).
