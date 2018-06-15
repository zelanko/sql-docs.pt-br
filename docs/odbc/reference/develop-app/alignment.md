---
title: Alinhamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09460dee5104baad7168839449d10bf36845b22f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909401"
---
# <a name="alignment"></a>Alinhamento
Os problemas de alinhamento em um aplicativo ODBC geralmente não são diferentes do que em qualquer outro aplicativo. Ou seja, a maioria dos aplicativos de ODBC tem poucas ou nenhuma problemas com alinhamento. As penalidades para o alinhamento não endereços variam de acordo com o hardware e sistema operacional e podem ser tão pequenas como uma pequena penalidade de desempenho ou como principal como um erro fatal de tempo de execução. Portanto, os aplicativos ODBC portáteis e os aplicativos ODBC em particular, cuidado alinhar os dados corretamente.  
  
 Um exemplo de quando os aplicativos ODBC encontram problemas de alinhamento é ao alocar um grande bloco de memória e associar partes diferentes do que a memória para as colunas em um conjunto de resultados. Isso é mais provável de ocorrer quando um aplicativo genérico deve determinar a forma de um conjunto de resultados em tempo de execução e alocar e associar memória adequadamente.  
  
 Por exemplo, suponha que um aplicativo executa um **selecione** instrução inserida pelo usuário e agrupa os resultados da instrução. Como a forma do conjunto de resultados não é conhecida quando o programa é gravado, o aplicativo deve determinar o tipo de cada coluna depois que o conjunto de resultados é criado e associar memória adequadamente. A maneira mais fácil de fazer isso é alocar um grande bloco de memória e associe endereços diferentes no bloco para cada coluna. Para acessar os dados em uma coluna, o aplicativo usa a memória associada a essa coluna.  
  
 O diagrama a seguir mostra um resultado de exemplo definido e como um bloco de memória pode ser associado a ele usando o tipo de dados C padrão para cada tipo de dados SQL. Cada "X" representa um único byte de memória. (Este exemplo mostra apenas os buffers de dados que são associados às colunas. Isso é feito para manter a simplicidade. No código real, os buffers de comprimento/indicador também devem estar alinhados.)  
  
 ![Associação de tipo de dados C padrão para o tipo de dados do SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Supondo que os endereços associados são armazenados no *endereço* matriz, o aplicativo usa as expressões a seguir para acessar a memória associada a cada coluna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que os endereços associados à segunda e terceira colunas Iniciar em número ímpar de bytes e não é divisível por quatro, que é o tamanho de um SDWORD que o endereço associada para a terceira coluna. Em alguns computadores, isso não será um problema; em outras, ela fará com que uma pequena penalidade de desempenho; em outros ainda, ela fará com que um erro fatal de tempo de execução. A melhor solução seria alinhar cada endereço associado no seu limite de alinhamento natural. Supondo que isso é 1 para um UCHAR, 2 para um SWORD e 4 para um SDWORD, isso daria o resultado é mostrado na ilustração a seguir, onde um "X" representa um byte de memória que é usada e um "O" representa um byte de memória que é usada.  
  
 ![Associação pelo limite de alinhamento natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Embora essa solução não usar toda a memória do aplicativo, ele não encontrar os problemas de alinhamento. Infelizmente, é preciso uma quantidade razoável de código para implementar esta solução, você deve alinhado individualmente cada coluna de acordo com seu tipo. É uma solução mais simples para alinhar todas as colunas no tamanho do maior limite de alinhamento, que é 4 no exemplo mostrado na ilustração a seguir.  
  
 ![Associação pelo maior limite de alinhamento](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Embora essa solução deixa intervalos maiores, o código para implementá-lo é relativamente simples e rápida. Na maioria dos casos, isso desloca a penalidade paga na memória não utilizada. Para obter um exemplo que usa esse método, consulte [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).
