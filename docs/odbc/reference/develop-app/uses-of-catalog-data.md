---
title: Usos de dados do catálogo | Microsoft Docs
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
ms.openlocfilehash: dc8999c0a7189772145f553646b45eb1f1fbd695
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091611"
---
# <a name="uses-of-catalog-data"></a>Usos de dados do catálogo
Os aplicativos usam dados de catálogo de várias maneiras. Aqui estão alguns usos comuns:  
  
-   **Construindo instruções SQL em tempo de execução.** Aplicativos verticais, como um aplicativo de entrada de pedidos, contêm instruções SQL embutidas em código. As tabelas e colunas usadas pelo aplicativo são corrigidas antes do tempo, assim como as instruções que acessam essas tabelas. Por exemplo, um aplicativo de entrada de pedido geralmente contém uma única instrução **Insert** com parâmetros para adicionar novos pedidos ao sistema.  
  
     Aplicativos genéricos, como um programa de planilha que usa o ODBC para recuperar dados, geralmente constroem instruções SQL em tempo de execução com base na entrada do usuário. Esse aplicativo pode exigir que o usuário digite os nomes das tabelas e colunas a serem usadas. No entanto, seria mais fácil para o usuário se o aplicativo exibisse listas de tabelas e colunas das quais o usuário poderia fazer seleções. Para compilar essas listas, o aplicativo chamaria as funções de catálogo **SQLTables** e **SQLColumns** .  
  
-   **Construindo instruções SQL durante o desenvolvimento.** Ambientes de desenvolvimento de aplicativos normalmente permitem que o programador crie consultas de banco de dados ao desenvolver um programa. Em seguida, as consultas são embutidas em código no aplicativo que está sendo compilado.  
  
     Esses ambientes também poderiam usar **SQLTables** e **SQLColumns** para criar listas das quais o programador poderia fazer seleções. Esses ambientes também podem usar **SQLPrimaryKeys** e **SQLForeignKeys** para determinar e mostrar automaticamente as relações entre as tabelas selecionadas e usar **SQLStatistics** para determinar e realçar campos indexados para que o programador possa criar consultas eficientes.  
  
-   **Construindo cursores.** Um aplicativo, driver ou middleware que fornece um mecanismo de cursor rolável pode usar **SQLSpecialColumns** para determinar qual coluna ou colunas identifica exclusivamente uma linha. O programa poderia criar um conjunto de *chaves* contendo os valores dessas colunas para cada linha que foi buscada. Quando o aplicativo rolar de volta para a linha, ele usará esses valores para buscar os dados mais recentes para a linha. Para obter mais informações sobre cursores roláveis e conjuntos de informações, consulte [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).
