---
title: Matrizes de valores de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03479a0187c7720a595b550290a8f5ac8197fa9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288407"
---
# <a name="arrays-of-parameter-values"></a>Matriz de valores de parâmetros
Muitas vezes é útil para aplicativos para passar matrizes de parâmetros. Por exemplo, usando matrizes de parâmetros e um parametrizada **inserir** instrução, um aplicativo pode inserir um número de linhas ao mesmo tempo. Há diversas vantagens em usar matrizes. Primeiro, o tráfego de rede é reduzido porque os dados para muitas instruções são enviados em um único pacote (se a fonte de dados dá suporte a matrizes de parâmetro nativamente). Em segundo lugar, algumas fontes de dados podem executar instruções SQL usando matrizes mais rápido do que executar o mesmo número de instruções de SQL separadas. Por fim, quando os dados são armazenados em uma matriz, como é geralmente o caso para dados da tela, o aplicativo pode associar todas as linhas em uma determinada coluna com uma única chamada para **SQLBindParameter** e atualizá-los executando uma única instrução.  
  
 Infelizmente, não de várias fontes de dados dá suporte a matrizes de parâmetros. No entanto, um driver pode emular a matrizes de parâmetros, executando uma instrução SQL, uma vez para cada conjunto de valores de parâmetro. Isso pode levar a aumentos de velocidade, porque o driver, em seguida, pode preparar a instrução que seu plano é executado uma vez para cada conjunto de parâmetros. Ele também pode levar mais simples do código do aplicativo.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando matrizes de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Usando matrizes de parâmetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
