---
title: "Matrizes de valores de parâmetro | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5f81e6b84f53da297f806ff2d63ea0b6e29b708
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="arrays-of-parameter-values"></a>Matrizes de valores de parâmetro
Geralmente é útil para aplicativos transmitir matrizes de parâmetros. Por exemplo, usando matrizes de parâmetros e um com parâmetros **inserir** instrução, um aplicativo pode inserir um número de linhas de uma vez. Há várias vantagens de usar matrizes. Primeiro, o tráfego de rede é reduzido porque os dados para muitas instruções são enviados em um único pacote (se a fonte de dados oferece suporte a matrizes de parâmetro modo nativo). Segundo, algumas fontes de dados podem executar instruções SQL usando matrizes mais rápido do que executar o mesmo número de instruções SQL separadas. Finalmente, quando os dados são armazenados em uma matriz, como é geralmente o caso para dados da tela, o aplicativo pode associar todas as linhas em uma determinada coluna com uma única chamada para **SQLBindParameter** e atualizá-los por uma única instrução em execução.  
  
 Infelizmente, não várias fontes de dados dá suporte a matrizes de parâmetros. No entanto, um driver pode emular matrizes de parâmetros, executar uma instrução SQL, uma vez para cada conjunto de valores de parâmetro. Isso pode levar a aumentos na velocidade porque o driver, em seguida, pode preparar a instrução que seu plano é executado uma vez para cada conjunto de parâmetros. Ele também pode resultar em código de aplicativo mais simples.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando matrizes de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Usando matrizes de parâmetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
