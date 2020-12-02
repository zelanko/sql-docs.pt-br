---
title: Números de ponto flutuante
description: Saiba mais sobre alguns dos problemas ao trabalhar com números de ponto flutuante no Provedor de Dados Microsoft SqlClient para SQL Server.
ms.date: 11/13/2020
ms.assetid: 73c218c6-1c44-4402-a167-4f6262629a91
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 12c9255e0f05d338d1c5cbe88019a9f288e4e8a5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126320"
---
# <a name="floating-point-numbers"></a>Números de ponto flutuante

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Este tópico descreve alguns dos problemas que os desenvolvedores costumam encontrar quando trabalham com números de ponto flutuante no Provedor de Dados Microsoft SqlClient para SQL Server. Esses problemas são causados pela maneira como os computadores armazenam números de ponto flutuante e não são específicos de determinado provedor, como <xref:Microsoft.Data.SqlClient>.

Números de ponto flutuante geralmente não têm uma representação binária exata. Em vez disso, o computador armazena uma aproximação do número. Em momentos variados, números diferentes de dígitos binários podem ser usados para representar o número. Quando um número de ponto flutuante é convertido de uma representação para outra, os dígitos menos significativos desse número podem variar um pouco. A conversão normalmente ocorre quando o número é convertido de um tipo para outro. A variação acontecerá se a conversão ocorrer em um banco de dados, entre tipos que representam valores de banco de dados, ou entre tipos. Devido a essas alterações, os números que logicamente seriam iguais podem ter alterações nos dígitos menos significativos que fazem com que eles tenham valores diferentes. O número de dígitos de precisão no número pode ser maior ou menor do que o esperado. Quando formatado como uma cadeia de caracteres, o número pode não mostrar o valor esperado.

Para minimizar esses efeitos, você deve usar a correspondência mais próxima entre os tipos numéricos disponíveis. Por exemplo, se você estiver trabalhando com SQL Server, o valor numérico exato poderá ser alterado se você converter um valor de Transact-SQL de tipo real para um valor de tipo float. No .NET Framework, a conversão de <xref:System.Single> em <xref:System.Double> também pode produzir resultados inesperados. Em ambos os casos, uma boa estratégia é fazer com que todos os valores no aplicativo usem o mesmo tipo numérico. Você também pode usar um tipo decimal de precisão fixa ou converter números de ponto flutuante para um tipo decimal de precisão fixa antes de trabalhar com eles.

Para solucionar problemas com a comparação de igualdade, considere codificar seu aplicativo para que as variações nos dígitos menos significativos sejam ignoradas. Por exemplo, em vez de comparar para ver se dois números são iguais, subtraia um número do outro. Se a diferença estiver dentro de uma margem aceitável de arredondamento, seu aplicativo poderá tratar os números como se eles fossem os mesmos.
