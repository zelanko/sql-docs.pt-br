---
title: Vinculando colunas para uso com cursores de bloco | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e527658a7d6945921510de898c648075c41fc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284896"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Colunas de associação para uso com cursores em bloco
Como os cursores de bloco retornam várias linhas, os aplicativos que os usam devem associar uma matriz de variáveis a cada coluna, em vez de uma única variável. Essas matrizes são coletivamente conhecidas como *buffers de conjunto de linhas*. A seguir estão os dois estilos de associação:  
  
-   Associar uma matriz a cada coluna. Isso é chamado de *associação por coluna,* pois cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para manter os dados de uma linha inteira e associar uma matriz dessas estruturas. Isso é chamado de *Associação de linha,* pois cada estrutura de dados contém os dados de uma única linha.  
  
 Como quando o aplicativo associa variáveis únicas a colunas, ele chama **SQLBindCol** para associar matrizes a colunas. A única diferença é que os endereços passados são endereços de matriz, não endereços de variável única. O aplicativo define o atributo SQL_BIND_BY_COLUMN instrução para especificar se ele está usando a associação de linha ou de coluna. A possibilidade de usar a associação de linha ou de coluna é basicamente uma questão de preferência de aplicativo. A associação de linha pode corresponder mais próximo ao layout de dados do aplicativo; nesse caso, ele forneceria um melhor desempenho.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md)
