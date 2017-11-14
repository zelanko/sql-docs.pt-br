---
title: "O que é um Cursor? | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03b7d4fe16a379e04fe25fe8fef95802aedabe1d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="what-is-a-cursor"></a>O que é um Cursor?
As operações em um ato de banco de dados relacional em um conjunto completo de linhas. O conjunto de linhas retornado por uma instrução SELECT consiste em todas as linhas que satisfazem as condições na cláusula WHERE da instrução. Este conjunto completo de linhas retornado pela instrução é conhecido como conjunto de resultados. Aplicativos, especialmente aqueles que são interativos e online, não podem sempre trabalhar efetivamente com todo o resultado definido como uma unidade. Esses aplicativos precisam de um mecanismo para trabalhar com uma linha ou um bloco pequeno de linhas de cada vez. Os cursores são uma extensão dos conjuntos de resultados que proveem esse mecanismo.  
  
 Um cursor é implementado por uma biblioteca de cursor. Uma biblioteca de cursor é um software, geralmente é implementado como parte de um sistema de banco de dados ou de acesso a dados API, que é usado para gerenciar os atributos dos dados retornados de uma fonte de dados (um conjunto de resultados). Esses atributos incluem gerenciamento de simultaneidade, posição no conjunto de resultados, o número de linhas retornadas e você pode mover para frente ou para trás (ou ambos) por meio do resultado definido (rolagem).  
  
 Um cursor controla a posição no conjunto de resultados e permite que você execute várias operações de linha por linha em um conjunto de resultados, com ou sem retornar para a tabela original. Em outras palavras, os cursores conceitualmente retornam um conjunto de resultados com base em tabelas em bancos de dados. O cursor é chamado assim porque ele indica a posição atual no conjunto de resultados, assim como o cursor em uma tela de computador indica a posição atual.  
  
 É importante para se familiarizar com o conceito de cursores antes de passar para conhecer as especificidades de seu uso no ADO.  
  
 Usar cursores, você pode:  
  
-   Especifique o posicionamento em linhas específicas no conjunto de resultados.  
  
-   Recupere uma linha ou um bloco de linhas com base na posição atual do conjunto de resultados.  
  
-   Modificar dados nas linhas da posição atual no conjunto de resultados.  
  
-   Defina diferentes níveis de sensibilidade a alterações de dados feitas por outros usuários.  
  
 Por exemplo, considere um aplicativo que exibe uma lista de produtos disponíveis para um cliente potencial. O comprador percorre a lista para ver detalhes do produto e custo e finalmente seleciona um produto para compra. Rolagem adicionais e seleção ocorre para o restante da lista. Quanto o comprador estiver preocupado, os produtos exibidos um de cada vez, mas o aplicativo usa um cursor rolável para percorrer o conjunto de resultados para cima e para baixo.  
  
 Você pode usar cursores de várias maneiras:  
  
-   Sem linhas de modo algum.  
  
-   Com algumas ou todas as linhas em uma única tabela.  
  
-   Com algumas ou todas as linhas de tabelas unidas logicamente.  
  
-   Como somente leitura ou atualizável no nível de cursor ou campo.  
  
-   Somente avanço ou totalmente rolável.  
  
-   Com o conjunto de chaves de cursor localizado no servidor.  
  
-   Sensíveis às alterações de tabela subjacente causadas por outros aplicativos (por exemplo, membros, classificação, inserções, atualizações e exclusões).  
  
-   Existente no servidor ou cliente.  
  
 Cursores de somente leitura ajudam os usuários a navegar pelo conjunto de resultados e cursores podem implantar as atualizações de linha individual de leitura/gravação. Cursores complexas podem ser definidos com os conjuntos de chaves que apontam para linhas da tabela de base. Embora alguns cursores são somente leitura avançando, outras pessoas possam voltar e Avançar e fornecer uma atualização dinâmica do conjunto de resultados com base nas alterações que outros aplicativos estão fazendo com o banco de dados.  
  
 Nem todos os aplicativos precisam usar cursores para acesso ou atualização de dados. Algumas consultas simplesmente não exigem a linha direta de atualização usando um cursor. Cursores devem ser uma das técnicas última escolha para recuperar dados, e, em seguida, você deve escolher o cursor menor impacto possível. Quando você cria um conjunto de resultados, usando um procedimento armazenado, o conjunto de resultados não é atualizável usando cursor editar ou métodos de atualização.  
  
## <a name="concurrency"></a>Simultaneidade  
 Em alguns aplicativos multiusuários é muito importante para os dados apresentados ao usuário final seja tão atuais quanto possível. Um exemplo clássico de um sistema como esse é um sistema de reserva aérea, onde vários usuários podem ser disputando o mesmo estação em um determinado voo (e, portanto, um único registro). Em casos como esse, o design do aplicativo deve tratar as operações simultâneas em um único registro.  
  
 Simultaneidade em outros aplicativos, não é tão importante. Nesses casos, não é possível justificar a despesa envolvidos em manter que os dados atuais em todos os momentos.  
  
## <a name="position"></a>Posição  
 Um cursor também controla de posições atuais em um conjunto de resultados. Pense da posição do cursor como um ponteiro para o registro atual, semelhante à forma como uma matriz pontos de índice para o valor nesse local específico na matriz.  
  
## <a name="scrollability"></a>Rolagem  
 O tipo de cursor usado pelo seu aplicativo também afeta a capacidade de mover-se através de linhas em um conjunto de resultados; Isso às vezes é chamado como rolagem. A capacidade de Avançar *e* com versões anteriores por meio de um resultado conjunto aumenta a complexidade do cursor e, portanto, é mais caro para implementar. Por esse motivo, você deve solicitar um cursor com essa funcionalidade somente quando necessário.

