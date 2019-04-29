---
title: Colunas de associação para uso com cursores em bloco | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0ed819643e7ea818fc17c0fa317473afc8f5ca3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007861"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Colunas de associação para uso com cursores em bloco
Como cursores em bloco retornam várias linhas, os aplicativos que utilizam devem associar uma matriz de variáveis para cada coluna em vez de uma única variável. Essas matrizes são conhecidas coletivamente como o *buffers rowset*. A seguir estão os dois estilos de associação:  
  
-   Associe uma matriz para cada coluna. Isso é chamado *a associação por coluna* porque cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para armazenar os dados para uma linha inteira e ligar uma matriz dessas estruturas. Isso é chamado *associação por linha* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Como quando o aplicativo associa variáveis únicas para colunas, ele chama **SQLBindCol** para associar as matrizes de colunas. A única diferença é que os endereços passados são endereços de matriz, endereços de variáveis não simples. O aplicativo define o atributo da instrução SQL_BIND_BY_COLUMN para especificar se ela está usando a coluna ou de linha de associação. Se deseja usar a coluna ou de linha de associação é principalmente uma questão de preferência de aplicativo. A associação pode correspondem mais aproximadamente ao layout do aplicativo de dados, caso em que isso ofereceria um desempenho melhor.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md)
