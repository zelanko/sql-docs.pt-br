---
title: Usos de Dados de Catálogo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306807"
---
# <a name="uses-of-catalog-data"></a>Usos de dados do catálogo
Os aplicativos usam dados de catálogo de várias maneiras. Aqui estão alguns usos comuns:  
  
-   **Construindo instruções SQL em tempo de execução.** Os aplicativos verticais, como um aplicativo de entrada de pedidos, contêm instruções SQL codificadas em código rígido. As tabelas e colunas utilizadas pelo aplicativo são fixadas antecipadamente, assim como as instruções que acessam essas tabelas. Por exemplo, um aplicativo de entrada de pedidos geralmente contém uma única instrução **INSERT** parametrizada para adicionar novas ordens ao sistema.  
  
     Aplicativos genéricos, como um programa de planilha que usa ODBC para recuperar dados, muitas vezes constroem instruções SQL em tempo de execução com base na entrada do usuário. Tal aplicativo poderia exigir que o usuário digitasse os nomes das tabelas e colunas para usar. No entanto, seria mais fácil para o usuário se o aplicativo exibisse listas de tabelas e colunas das quais o usuário poderia fazer seleções. Para construir essas listas, o aplicativo chamaria as funções de catálogo **SQLTables** e **SQLColumns.**  
  
-   **Construindo declarações SQL durante o desenvolvimento.** Ambientes de desenvolvimento de aplicativos normalmente permitem que o programador crie consultas de banco de dados enquanto desenvolve um programa. As consultas são então codificadas no aplicativo que está sendo construído.  
  
     Esses ambientes também poderiam usar **SQLTables** e **SQLColumns** para criar listas a partir das quais o programador poderia fazer seleções. Esses ambientes também podem usar **SQLPrimaryKeys** e **SQLForeignKeys** para determinar e mostrar automaticamente as relações entre as tabelas selecionadas e usar **o SQLStatistics** para determinar e destacar campos indexados para que o programador possa criar consultas eficientes.  
  
-   **Construindo cursores.** Um aplicativo, driver ou middleware que forneça um mecanismo de cursor rolável pode usar **SQLSpecialColumns** para determinar qual coluna ou coluna simem exclusivamente uma linha. O programa poderia construir um *conjunto de chaves* contendo os valores dessas colunas para cada linha que foi buscada. Quando o aplicativo rola de volta para a linha, ele então usaria esses valores para buscar os dados mais recentes para a linha. Para obter mais informações sobre cursores e conjuntos de tecla roláveis, consulte [Cursors Roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).
