---
title: Matrizes de Valores de Parâmetro | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb9389c769e3a7bb0c39959a559531e8051a7bec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298790"
---
# <a name="arrays-of-parameter-values"></a>Matriz de valores de parâmetros
Muitas vezes é útil para os aplicativos passarem matrizes de parâmetros. Por exemplo, usando matrizes de parâmetros e uma instrução **INSERT** parametrizada, um aplicativo pode inserir várias linhas ao mesmo tempo. Existem várias vantagens em usar arrays. Primeiro, o tráfego de rede é reduzido porque os dados de muitas instruções são enviados em um único pacote (se a fonte de dados suportar matrizes de parâmetros nativamente). Em segundo lugar, algumas fontes de dados podem executar instruções SQL usando arrays mais rapidamente do que executar o mesmo número de instruções SQL separadas. Finalmente, quando os dados são armazenados em um array, como é frequentemente o caso dos dados de tela, o aplicativo pode vincular todas as linhas em uma coluna específica com uma única chamada ao **SQLBindParameter** e atualizá-los executando uma única declaração.  
  
 Infelizmente, poucas fontes de dados suportam matrizes de parâmetros. No entanto, um driver pode emular matrizes de parâmetros executando uma declaração SQL uma vez para cada conjunto de valores de parâmetros. Isso pode levar a aumentos de velocidade porque o motorista pode então preparar a declaração que planeja executar uma vez para cada parâmetro definido. Também pode levar a um código de aplicação mais simples.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associar matrizes de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Usar matrizes de parâmetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
