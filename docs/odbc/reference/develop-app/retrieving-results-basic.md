---
title: Recuperando resultados (básico) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020473"
---
# <a name="retrieving-results-basic"></a>Recuperar resultados (básico)
Um *conjunto de resultados* é um conjunto de linhas na fonte de dados que corresponda a determinados critérios. É uma tabela conceitual que os resultados de uma consulta e que estão disponíveis para um aplicativo em formato tabular. **Selecione** instruções, funções de catálogo e alguns procedimentos de criam conjuntos de resultados. No exemplo a seguir, a primeira instrução SQL cria um conjunto de resultados contendo todas as linhas e todas as colunas na tabela de pedidos e a segunda instrução SQL cria um conjunto de resultados contendo as colunas OrderID, o vendedor e o Status das linhas na tabela de pedidos em que o Status é aberto:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Um conjunto de resultados pode ser vazio, que é diferente de nenhum resultado definido em todos os. Por exemplo, a instrução SQL a seguir cria um conjunto de resultados vazio:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Um conjunto de resultados vazio não é diferente de qualquer outro conjunto de resultados, exceto que ele não tem nenhuma linha. Por exemplo, o aplicativo pode recuperar metadados para o conjunto de resultados, poderá tentar buscar linhas e deve fechar o cursor sobre o conjunto de resultados.  
  
 O processo de recuperar linhas da fonte de dados e retorná-los para o aplicativo é chamado *buscando*. Esta seção explica as partes básicas do processo. Para obter informações sobre tópicos mais avançados, como o bloco e cursores roláveis, consulte [cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md). Para obter informações sobre a atualização, exclusão e inserção de linhas, consulte [visão geral da atualização de dados](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Um conjunto de resultados foi criado?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Colunas de associação](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Buscando dados](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Fechando o cursor](../../../odbc/reference/develop-app/closing-the-cursor.md)
