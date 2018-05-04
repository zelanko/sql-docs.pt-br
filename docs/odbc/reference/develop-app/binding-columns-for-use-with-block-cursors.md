---
title: Colunas de associação para uso com cursores em bloco | Microsoft Docs
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
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bc72bbffc1518e5c2a93adbb8fac75ba555159b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Colunas de associação para uso com cursores em bloco
Como cursores em bloco retornam várias linhas, os aplicativos que utilizam devem vincular uma matriz de variáveis para cada coluna em vez de uma única variável. Essas matrizes são coletivamente conhecidos como o *buffers de conjunto de linhas*. Estes são os dois estilos de associação:  
  
-   Associe uma matriz para cada coluna. Isso é chamado de *a associação* porque cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para reter os dados para uma linha inteira e associar uma matriz dessas estruturas. Isso é chamado de *a associação* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Como quando o aplicativo associa único variáveis para colunas, ele chama **SQLBindCol** para associar as matrizes de colunas. A única diferença é que os endereços passados são endereços de matriz, endereços de variável simples não. O aplicativo define o atributo de instrução SQL_BIND_BY_COLUMN para especificar se está usando associação de coluna ou linha de associação. Se deseja usar a associação de coluna ou linha de associação é principalmente uma questão de preferência de aplicativo. A associação pode corresponder mais estritamente ao layout do aplicativo de dados, caso em que ele deve fornecer um melhor desempenho.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md)
