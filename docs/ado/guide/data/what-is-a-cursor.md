---
title: O que é um cursor? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d5704a43e1ede850a225c4ec2b4df9a3563606b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184871"
---
# <a name="what-is-a-cursor"></a>O que é um cursor?
As operações em um ato de banco de dados relacional em um conjunto completo de linhas. O conjunto de linhas retornado por uma instrução SELECT consiste em todas as linhas que satisfazem as condições na cláusula WHERE da instrução. Este conjunto completo de linhas retornado pela instrução é conhecido como conjunto de resultados. Aplicativos, especialmente aquelas que são interativos e online, não podem sempre trabalhar efetivamente com todo o resultado definido como uma unidade. Esses aplicativos precisam de um mecanismo para trabalhar com uma linha ou um bloco pequeno de linhas de cada vez. Os cursores são uma extensão dos conjuntos de resultados que proveem esse mecanismo.  
  
 Um cursor é implementado por uma biblioteca de cursores. Uma biblioteca de cursor é um software, geralmente é implementado como parte de um sistema de banco de dados ou uma API, acesso a dados que é usado para gerenciar atributos dos dados retornados de uma fonte de dados (um conjunto de resultados). Esses atributos incluem o gerenciamento de simultaneidade, posição no conjunto de resultados, número de linhas retornadas e você pode mover para frente ou para trás (ou ambos) por meio de resultados definido (rolagem).  
  
 Um cursor controla a posição no conjunto de resultados e permite que você execute várias operações linha por linha em relação a um conjunto de resultados, com ou sem retornar à tabela original. Em outras palavras, os cursores conceitualmente retornam um conjunto de resultados com base em tabelas nos bancos de dados. O cursor é assim chamado porque ele indica a posição atual no conjunto de resultados, assim como o cursor em uma tela de computador indica a posição atual.  
  
 É importante para se familiarizar com o conceito de cursores antes de passar para conhecer as especificidades de seu uso no ADO.  
  
 Usar cursores, você pode:  
  
-   Especifique o posicionamento em linhas específicas no conjunto de resultados.  
  
-   Recupere uma linha ou um bloco de linhas com base na posição atual do conjunto de resultados.  
  
-   Modificar dados nas linhas da posição atual no conjunto de resultados.  
  
-   Defina diferentes níveis de sensibilidade a alterações de dados feitas por outros usuários.  
  
 Por exemplo, considere um aplicativo que exibe uma lista de produtos disponíveis para um cliente potencial. O comprador percorre a lista para ver o custo e os detalhes do produto e, finalmente, seleciona um produto para compra. Rolagem adicionais e seleção ocorre para o restante da lista. Como o comprador está preocupado, os produtos são exibidos um por vez, mas o aplicativo usa um cursor rolável para cima e para baixo navegar pelo conjunto de resultados.  
  
 Você pode usar cursores em uma variedade de maneiras:  
  
-   Sem linhas em todas.  
  
-   Com algumas ou todas as linhas em uma única tabela.  
  
-   Com algumas ou todas as linhas de tabelas unidas logicamente.  
  
-   Como somente leitura ou atualizáveis no nível do cursor ou campo.  
  
-   Somente encaminhamento ou totalmente rolável.  
  
-   Com o conjunto de chaves de cursor localizado no servidor.  
  
-   Sensível a alterações de tabela subjacentes causadas por outros aplicativos (por exemplo, associação, classificação, inserções, atualizações e exclusões).  
  
-   Existentes no servidor ou cliente.  
  
 Cursores de somente leitura ajudam usuários a navegar pelo conjunto de resultados e cursores podem implementar atualizações de linha individual de leitura/gravação. Cursores complexas podem ser definidas com os conjuntos de chaves que apontam para linhas da tabela de base. Embora alguns cursores são somente leitura em uma direção progressiva, outras pessoas possam ir e voltar e fornecer uma atualização dinâmica do conjunto de resultados com base nas alterações que outros aplicativos estão fazendo no banco de dados.  
  
 Nem todos os aplicativos precisam usar cursores para acessar ou atualizar dados. Algumas consultas simplesmente não exigem a atualização de linha direta usando um cursor. Cursores devem ser uma das técnicas a última escolha para recuperar dados – e, em seguida, você deve escolher o cursor de impacto mais baixo possível. Quando você cria um conjunto de resultados, usando um procedimento armazenado, o conjunto de resultados não é atualizável usando cursor editar ou métodos de atualização.  
  
## <a name="concurrency"></a>Simultaneidade  
 Em alguns aplicativos multiusuários, é muito importante para os dados apresentados ao usuário final ser as mais atuais possíveis. Um exemplo clássico de um sistema desse tipo é um sistema de reserva de companhia aérea, em que muitos usuários podem ser disputando o assento mesmo em um determinado voo (e, portanto, um único registro). Em casos como esse, o design do aplicativo deve lidar com operações simultâneas em um único registro.  
  
 Em outros aplicativos, a simultaneidade não é tão importante. Nesses casos, não é possível justificar a despesa envolvidos em manter que os dados atuais em todos os momentos.  
  
## <a name="position"></a>Posição  
 Também um cursor que mantém controle da posição atual em um conjunto de resultados. Considere a posição do cursor como um ponteiro para o registro atual, semelhante à forma como uma matriz pontos de índice para o valor nesse local específico na matriz.  
  
## <a name="scrollability"></a>Rolagem  
 O tipo de cursor empregado pelo seu aplicativo também afeta a capacidade de mover para frente e para trás pelas linhas em um conjunto de resultados; Isso é às vezes, chamado rolagem. A capacidade de mover para frente *e* com versões anteriores por meio de um resultado conjunto aumenta a complexidade do cursor e, portanto, é mais caro para implementar. Por esse motivo, você deve solicitar um cursor com essa funcionalidade somente quando necessário.
