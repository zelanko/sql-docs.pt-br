---
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
ms.openlocfilehash: 205cc3ff95dd60db215150f46ae894fbb99bd9ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288601"
---
# <a name="alignment"></a>Alinhamento
Os problemas de alinhamento em um aplicativo ODBC geralmente não são diferentes do que em qualquer outra aplicação. Ou seja, a maioria dos aplicativos ODBC tem poucos ou nenhum problema com o alinhamento. As penalidades por não alinhar endereços variam de acordo com o hardware e o sistema operacional e podem ser tão pequenas quanto uma pequena penalidade de desempenho ou tão grande quanto um erro fatal de tempo de execução. Portanto, as aplicações ODBC e as aplicações ODBC portáteis, em particular, devem ter cuidado para alinhar os dados corretamente.  
  
 Um exemplo de quando os aplicativos ODBC encontram problemas de alinhamento é quando eles alocam um grande bloco de memória e vinculam diferentes partes dessa memória às colunas em um conjunto de resultados. Isso é mais provável de ocorrer quando um aplicativo genérico deve determinar a forma de um resultado definido em tempo de execução e alocar e vincular a memória de acordo.  
  
 Por exemplo, suponha que um aplicativo execute uma declaração **SELECT** inserida pelo usuário e busque os resultados desta declaração. Como a forma deste conjunto de resultados não é conhecida quando o programa é gravado, o aplicativo deve determinar o tipo de cada coluna após a criação do conjunto de resultados e vincular a memória de acordo. A maneira mais fácil de fazer isso é alocar um grande bloco de memória e vincular diferentes endereços nesse bloco a cada coluna. Para acessar os dados em uma coluna, o aplicativo lança a memória vinculada a essa coluna.  
  
 O diagrama a seguir mostra um conjunto de resultados de amostra e como um bloco de memória pode ser vinculado a ele usando o tipo de dados C padrão para cada tipo de dados SQL. Cada "X" representa um único byte de memória. (Este exemplo mostra apenas os buffers de dados que estão vinculados às colunas. Isso é feito pela simplicidade. No código real, os buffers de comprimento/indicador também devem ser alinhados.)  
  
 ![Associando, por padrão, o tipo de dados C com o tipo de dados SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Supondo que os endereços vinculados estejam armazenados na matriz *Endereço,* o aplicativo usa as seguintes expressões para acessar a memória vinculada a cada coluna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que os endereços vinculados à segunda e terceira colunas começam em bytes numerados ímpares e que o endereço vinculado à terceira coluna não é divisível por quatro, que é do tamanho de um SDWORD. Em algumas máquinas, isso não será um problema; em outros, causará uma pequena penalidade de desempenho; em outros ainda, causará um erro fatal de tempo de execução. Uma solução melhor seria alinhar cada endereço vinculado em seu limite de alinhamento natural. Supondo que este seja 1 para um UCHAR, 2 para um SWORD e 4 para um SDWORD, isso daria o resultado mostrado na ilustração a seguir, onde um "X" representa um byte de memória que é usado e um "O" representa um byte de memória que não é utilizado.  
  
 ![Associação pelo limite de alinhamento natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Embora esta solução não use toda a memória do aplicativo, ela não encontra nenhum problema de alinhamento. Infelizmente, é preciso uma boa quantidade de código para implementar esta solução, pois cada coluna deve ser alinhada individualmente de acordo com o seu tipo. Uma solução mais simples é alinhar todas as colunas sobre o tamanho do maior limite de alinhamento, que é 4 no exemplo mostrado na ilustração a seguir.  
  
 ![Associação pelo maior limite de alinhamento](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Embora esta solução deixe buracos maiores, o código para implementá-la é relativamente simples e rápido. Na maioria dos casos, isso compensa a penalidade paga em memória não utilizada. Para um exemplo que usa este método, consulte [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
