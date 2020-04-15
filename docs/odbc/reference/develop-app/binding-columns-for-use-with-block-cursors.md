---
title: Colunas de vinculação para uso com cursores de bloco | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284896"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Colunas de associação para uso com cursores em bloco
Como os cursores de bloco retornam várias linhas, os aplicativos que os usam devem vincular uma matriz de variáveis a cada coluna em vez de uma única variável. Essas matrizes são coletivamente conhecidas como *buffers de conjunto de linhas*. A seguir estão os dois estilos de vinculação:  
  
-   Vincule uma matriz a cada coluna. Isso é chamado *de vinculação em termos de coluna* porque cada estrutura de dados (array) contém dados para uma única coluna.  
  
-   Defina uma estrutura para reter os dados por uma linha inteira e vincule uma matriz dessas estruturas. Isso é chamado *de vinculação em termos de linha* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Como quando o aplicativo vincula variáveis únicas a colunas, ele chama **SQLBindCol** para vincular matrizes a colunas. A única diferença é que os endereços aprovados são endereços de matriz, não endereços variáveis únicos. O aplicativo define o atributo de declaração SQL_BIND_BY_COLUMN para especificar se ele está usando a vinculação em termos de coluna ou em forma de linha. Se usar a vinculação em termos de coluna ou de linha é em grande parte uma questão de preferência de aplicativo. A vinculação em termos de linha pode corresponder mais de perto ao layout de dados do aplicativo, nesse caso, ele forneceria melhor desempenho.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md)
