---
title: "Colunas de associação para uso com cursores em bloco | Microsoft Docs"
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
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4fcc0221bcf4a3555052c9562dca830e6e48f84a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Colunas de associação para uso com cursores em bloco
Como cursores em bloco retornam várias linhas, os aplicativos que utilizam devem vincular uma matriz de variáveis para cada coluna em vez de uma única variável. Essas matrizes são coletivamente conhecidos como o *buffers de conjunto de linhas*. Estes são os dois estilos de associação:  
  
-   Associe uma matriz para cada coluna. Isso é chamado de *a associação* porque cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para reter os dados para uma linha inteira e associar uma matriz dessas estruturas. Isso é chamado de *a associação* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Como quando o aplicativo associa único variáveis para colunas, ele chama **SQLBindCol** para associar as matrizes de colunas. A única diferença é que os endereços passados são endereços de matriz, endereços de variável simples não. O aplicativo define o atributo de instrução SQL_BIND_BY_COLUMN para especificar se está usando associação de coluna ou linha de associação. Se deseja usar a associação de coluna ou linha de associação é principalmente uma questão de preferência de aplicativo. A associação pode corresponder mais estritamente ao layout do aplicativo de dados, caso em que ele deve fornecer um melhor desempenho.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md)
