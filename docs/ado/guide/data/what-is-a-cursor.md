---
description: O que é um cursor?
title: O que é um cursor? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: rothja
ms.author: jroth
ms.openlocfilehash: 3090e38507a73d00edbe3bd1cb85e408c88fdba1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978917"
---
# <a name="what-is-a-cursor"></a>O que é um cursor?
As operações em um ato de banco de dados relacional em um conjunto completo de linhas. O conjunto de linhas retornado por uma instrução SELECT consiste em todas as linhas que satisfazem as condições na cláusula WHERE da instrução. Este conjunto completo de linhas retornado pela instrução é conhecido como conjunto de resultados. Os aplicativos, especialmente aqueles que são interativos e online, nem sempre podem trabalhar com eficiência com o conjunto de resultados inteiro como uma unidade. Esses aplicativos precisam de um mecanismo para trabalhar com uma linha ou um bloco pequeno de linhas de cada vez. Os cursores são uma extensão dos conjuntos de resultados que proveem esse mecanismo.  
  
 Um cursor é implementado por uma biblioteca de cursores. Uma biblioteca de cursores é um software, geralmente implementada como parte de um sistema de banco de dados ou de uma API de acesso a data, que é usada para gerenciar atributos de dados retornados de uma fonte de dados (um conjunto de resultados). Esses atributos incluem gerenciamento de simultaneidade, posição no conjunto de resultados, número de linhas retornadas e se você pode avançar ou retroceder (ou ambos) por meio do conjunto de resultados (rolabilidade).  
  
 Um cursor mantém o controle da posição no conjunto de resultados e permite que você execute várias operações linha por linha em relação a um conjunto de resultados, com ou sem retornar à tabela original. Em outras palavras, os cursores conceitualmente retornam um conjunto de resultados com base em tabelas dentro dos bancos de dados. O cursor é tão nomeado porque indica a posição atual no conjunto de resultados, assim como o cursor em uma tela de computador indica a posição atual.  
  
 É importante familiarizar-se com o conceito de cursores antes de prosseguir para aprender as especificações de seu uso no ADO.  
  
 Usando cursores, você pode:  
  
-   Especifique o posicionamento em linhas específicas no conjunto de resultados.  
  
-   Recupere uma linha ou um bloco de linhas com base na posição atual do conjunto de resultados.  
  
-   Modifique os dados nas linhas na posição atual no conjunto de resultados.  
  
-   Defina diferentes níveis de sensibilidade às alterações de dados feitas por outros usuários.  
  
 Por exemplo, considere um aplicativo que exibe uma lista de produtos disponíveis para um comprador potencial. O comprador rola pela lista para ver os detalhes e os custos do produto e, finalmente, seleciona um produto para compra. A rolagem e a seleção adicionais ocorrem para o restante da lista. No que diz respeito ao comprador, os produtos aparecem um de cada vez, mas o aplicativo usa um cursor rolável para navegar para cima e para baixo no conjunto de resultados.  
  
 Você pode usar cursores de várias maneiras:  
  
-   Sem linhas.  
  
-   Com algumas ou todas as linhas em uma única tabela.  
  
-   Com algumas ou todas as linhas de tabelas logicamente Unidas.  
  
-   Como somente leitura ou atualizável no nível do cursor ou do campo.  
  
-   Como somente encaminhamento ou totalmente rolável.  
  
-   Com o conjunto de chaves de cursor localizado no servidor.  
  
-   Sensível a alterações de tabela subjacente causadas por outros aplicativos (como associação, classificação, inserções, atualizações e exclusões).  
  
-   Existente no servidor ou no cliente.  
  
 Cursores somente leitura ajudam os usuários a navegar pelo conjunto de resultados e os cursores de leitura/gravação podem implementar atualizações de linha individuais. Cursores complexos podem ser definidos com conjuntos de registros que apontam de volta para linhas da tabela base. Embora alguns cursores sejam somente leitura em direção à frente, outros podem se mover para frente e para trás e fornecer uma atualização dinâmica do conjunto de resultados com base nas alterações que outros aplicativos estão fazendo no banco de dados.  
  
 Nem todos os aplicativos precisam usar cursores para acessar ou atualizar dados. Algumas consultas simplesmente não exigem a atualização direta de linha usando um cursor. Os cursores devem ser uma das últimas técnicas que você escolhe para recuperar dados e, em seguida, você deve escolher o cursor de impacto mais baixo possível. Quando você cria um conjunto de resultados usando um procedimento armazenado, o conjunto de resultados não é atualizável usando os métodos de edição ou atualização do cursor.  
  
## <a name="concurrency"></a>Simultaneidade  
 Em alguns aplicativos multiusuário, é muito importante que os dados apresentados ao usuário final sejam os mais atuais possíveis. Um exemplo clássico de tal sistema é um sistema de reserva de viagens, onde muitos usuários podem estar contendendo a mesma estação em um determinado vôo (e, portanto, um único registro). Em um caso como esse, o design do aplicativo deve manipular operações simultâneas em um único registro.  
  
 Em outros aplicativos, a simultaneidade não é tão importante. Nesses casos, a despesa envolvida em manter os dados atuais em todos os momentos não pode ser justificada.  
  
## <a name="position"></a>Posição  
 Um cursor também mantém o controle da posição atual em um conjunto de resultados. Considere a posição do cursor como um ponteiro para o registro atual, semelhante ao modo como um índice de matriz aponta para o valor nesse local em particular na matriz.  
  
## <a name="scrollability"></a>Rolagem  
 O tipo de cursor empregado pelo seu aplicativo também afeta a capacidade de avançar e voltar pelas linhas em um conjunto de resultados; isso às vezes é chamado de rolabilidade. A capacidade de avançar *e* retroceder por meio de um conjunto de resultados aumenta a complexidade do cursor e, portanto, é mais cara para implementar. Por esse motivo, você deve solicitar um cursor com essa funcionalidade somente quando necessário.
