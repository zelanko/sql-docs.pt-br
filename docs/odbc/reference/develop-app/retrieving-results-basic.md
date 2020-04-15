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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304327"
---
# <a name="retrieving-results-basic"></a>Recuperar resultados (básico)
Um *conjunto de resultados* é um conjunto de linhas na fonte de dados que corresponde a certos critérios. É uma tabela conceitual que resulta de uma consulta e que está disponível para um aplicativo em forma tabular. **Instruções SELECT,** funções de catálogo e alguns procedimentos criam conjuntos de resultados. No exemplo a seguir, a primeira declaração SQL cria um conjunto de resultados contendo todas as linhas e todas as colunas na tabela Ordens, e a segunda declaração SQL cria um conjunto de resultados contendo colunas OrderID, SalesPerson e Status para as linhas na tabela '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Um conjunto de resultados pode ser vazio, o que é diferente de nenhum resultado definido. Por exemplo, a seguinte declaração SQL cria um conjunto de resultados vazio:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Um conjunto de resultados vazio não é diferente de qualquer outro conjunto de resultados, exceto que não tem linhas. Por exemplo, o aplicativo pode recuperar metadados para o conjunto de resultados, pode tentar buscar linhas e deve fechar o cursor sobre o conjunto de resultados.  
  
 O processo de recuperação de linhas da fonte de dados e devolvê-las ao aplicativo é chamado *de buscar*. Esta seção explica as partes básicas desse processo. Para obter informações sobre tópicos mais avançados, como cursores de bloco e roláveis, consulte [Cursors de bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md). Para obter informações sobre como atualizar, excluir e inserir linhas, consulte [Visão geral de dados atualizado](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Um conjunto de resultados foi criado?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Colunas de associação](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Buscar dados](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Fechar o cursor](../../../odbc/reference/develop-app/closing-the-cursor.md)
