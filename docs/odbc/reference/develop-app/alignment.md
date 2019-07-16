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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8b5a107f5ed8cd1c6c45317e60cc515a2601316
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077276"
---
# <a name="alignment"></a>Alinhamento
Os problemas de alinhamento em um aplicativo ODBC geralmente não são diferentes do que em qualquer outro aplicativo. Ou seja, a maioria dos aplicativos de ODBC tem problemas de poucas ou nenhuma com o alinhamento. As penalidades para alinhar não endereços variam de acordo com o hardware e sistema operacional e podem ser tão secundário, como uma pequena penalidade de desempenho ou como principal como um erro fatal de tempo de execução. Portanto, os aplicativos ODBC e os aplicativos ODBC portátil em particular, cuidado alinhar os dados corretamente.  
  
 Um exemplo de quando os aplicativos ODBC encontram problemas de alinhamento é quando eles alocam um grande bloco de memória e associar partes diferentes do que a memória para as colunas em um conjunto de resultados. Isso é mais provável de ocorrer quando um aplicativo genérico deve determinar a forma de um conjunto de resultados em tempo de execução e alocar associar memória adequadamente.  
  
 Por exemplo, suponha que um aplicativo executa uma **selecionar** instrução inserida pelo usuário e busca os resultados dessa instrução. Como a forma desse conjunto de resultados não é conhecida quando o programa é escrito, o aplicativo deve determinar o tipo de cada coluna depois que o conjunto de resultados é criado e associar memória adequadamente. A maneira mais fácil de fazer isso é alocar um grande bloco de memória e associar diferentes endereços nesse bloco para cada coluna. Para acessar os dados em uma coluna, o aplicativo converte a memória associada a essa coluna.  
  
 O diagrama a seguir mostra um resultado de exemplo definido e como um bloco de memória pode ser associado a ele usando o tipo de dados C padrão para cada tipo de dados SQL. Cada "X" representa um único byte de memória. (Este exemplo mostra apenas os buffers de dados que estão associados às colunas. Isso é feito para manter a simplicidade. No código real, os buffers de comprimento/indicador também devem estar alinhados.)  
  
 ![Associação pelo tipo de dados C padrão para o tipo de dados SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Supondo que os endereços associados são armazenadas em do *endereço* matriz, o aplicativo usa as expressões a seguir para acessar a memória associada a cada coluna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que os endereços associado à segunda e terceira colunas Iniciar em número ímpar de bytes e que o endereço associado para a terceira coluna não for divisível por quatro, o que é o tamanho de um SDWORD. Em alguns computadores, isso não será um problema; em outros, ela fará com que uma pequena penalidade de desempenho; em outros ainda, ela fará com que um erro fatal de tempo de execução. Uma solução melhor seria alinhar cada endereço associado em seu limite de alinhamento natural. Supondo que isso é 1 para um UCHAR, 2 para uma ESPADA e 4 para um SDWORD, isso daria o resultado mostrado na ilustração a seguir, onde um "X" representa um byte de memória que é usada e um "O" representa um byte de memória que é usada.  
  
 ![Associação pelo limite de alinhamento natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Embora essa solução use toda memória do aplicativo, ele não enfrenta nenhum problema de alinhamento. Infelizmente, leva uma quantidade razoável de código para implementar esta solução, cada coluna deve ser alinhado individualmente acordo com seu tipo. Uma solução mais simples é alinhar todas as colunas no tamanho do maior limite de alinhamento, que é 4 no exemplo mostrado na ilustração a seguir.  
  
 ![Associação pelo maior limite de alinhamento](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Embora essa solução deixa buracos maiores, o código para implementá-lo é relativamente simples e rápida. Na maioria dos casos, isso compensa a penalidade paga em memória não utilizada. Para obter um exemplo que usa esse método, consulte [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).
