---
description: Alinhamento
title: Alinhamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1402eee289111ca100e80730d8df4a6d0e3299cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483139"
---
# <a name="alignment"></a>Alinhamento
Os problemas de alinhamento em um aplicativo ODBC geralmente não são diferentes do que em qualquer outro aplicativo. Ou seja, a maioria dos aplicativos ODBC tem poucos problemas de alinhamento. As penalidades para não alinhar endereços variam de acordo com o hardware e o sistema operacional e podem ser tão secundárias quanto uma ligeira penalidade de desempenho ou a principal como um erro fatal de tempo de execução. Portanto, os aplicativos ODBC e os aplicativos ODBC portáteis, em particular, devem ter cuidado para alinhar os dados corretamente.  
  
 Um exemplo de quando os aplicativos ODBC encontram problemas de alinhamento é quando eles alocam um grande bloco de memória e associam partes diferentes da memória às colunas em um conjunto de resultados. É mais provável que isso ocorra quando um aplicativo genérico deve determinar a forma de um conjunto de resultados em tempo de execução e alocar e associar a memória de acordo.  
  
 Por exemplo, suponha que um aplicativo execute uma instrução **Select** inserida pelo usuário e busque os resultados dessa instrução. Como a forma desse conjunto de resultados não é conhecida quando o programa é gravado, o aplicativo deve determinar o tipo de cada coluna depois que o conjunto de resultados é criado e associar a memória de acordo. A maneira mais fácil de fazer isso é alocar um grande bloco de memória e associar endereços diferentes nesse bloco a cada coluna. Para acessar os dados em uma coluna, o aplicativo converte a memória associada a essa coluna.  
  
 O diagrama a seguir mostra um conjunto de resultados de exemplo e como um bloco de memória pode ser associado a ele usando o tipo de dados C padrão para cada tipo de dados SQL. Cada "X" representa um único byte de memória. (Este exemplo mostra apenas os buffers de dados que estão associados às colunas. Isso é feito para simplificar. No código real, os buffers de comprimento/indicador também devem ser alinhados.)  
  
 ![Associando, por padrão, o tipo de dados C com o tipo de dados SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Supondo que os endereços vinculados sejam armazenados na matriz de *endereços* , o aplicativo usa as seguintes expressões para acessar a memória associada a cada coluna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que os endereços vinculados à segunda e terceira colunas começam em bytes de números ímpares e que o endereço associado à terceira coluna não é divisível por quatro, que é o tamanho de um SDWORD. Em alguns computadores, isso não será um problema; em outras, isso causará uma ligeira penalidade de desempenho; ainda em outras, isso causará um erro fatal em tempo de execução. Uma solução melhor seria alinhar cada endereço associado em seu limite de alinhamento natural. Supondo que isso seja 1 para um UCHAR, 2 para um gumes e 4 para um SDWORD, isso daria o resultado mostrado na ilustração a seguir, em que um "X" representa um byte de memória que é usado e um "O" representa um byte de memória não utilizado.  
  
 ![Associação pelo limite de alinhamento natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Embora essa solução não use toda a memória do aplicativo, ela não encontra nenhum problema de alinhamento. Infelizmente, é preciso uma quantidade razoável de código para implementar essa solução, pois cada coluna deve ser alinhada individualmente de acordo com seu tipo. Uma solução mais simples é alinhar todas as colunas no tamanho do maior limite de alinhamento, que é 4 no exemplo mostrado na ilustração a seguir.  
  
 ![Associação pelo maior limite de alinhamento](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Embora essa solução deixe buracos maiores, o código para implementá-lo é relativamente simples e rápido. Na maioria dos casos, isso desloca a penalidade paga na memória não utilizada. Para obter um exemplo que usa esse método, consulte [usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
