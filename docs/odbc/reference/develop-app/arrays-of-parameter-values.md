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
ms.openlocfilehash: 1e65928cd078a3f05032f4e4fb400e3e2eb1f27a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077067"
---
# <a name="arrays-of-parameter-values"></a>Matriz de valores de parâmetros
Geralmente, é útil para aplicativos passarem matrizes de parâmetros. Por exemplo, usando matrizes de parâmetros e uma instrução **Insert** com parâmetros, um aplicativo pode inserir um número de linhas ao mesmo tempo. Há várias vantagens em usar matrizes. Primeiro, o tráfego de rede é reduzido porque os dados para muitas instruções são enviados em um único pacote (se a fonte de dados der suporte a matrizes de parâmetros nativamente). Em segundo lugar, algumas fontes de dados podem executar instruções SQL usando matrizes mais rapidamente do que a execução do mesmo número de instruções SQL separadas. Por fim, quando os dados são armazenados em uma matriz, como geralmente é o caso dos dados da tela, o aplicativo pode associar todas as linhas de uma determinada coluna a uma única chamada para **SQLBindParameter** e atualizá-las executando uma única instrução.  
  
 Infelizmente, não muitas fontes de dados dão suporte a matrizes de parâmetros. No entanto, um driver pode emular matrizes de parâmetros executando uma instrução SQL uma vez para cada conjunto de valores de parâmetro. Isso pode levar a aumentos em velocidade porque o driver pode, então, preparar a instrução que planeja executar uma vez para cada conjunto de parâmetros. Ele também pode levar a um código de aplicativo mais simples.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Associar matrizes de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Usar matrizes de parâmetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
