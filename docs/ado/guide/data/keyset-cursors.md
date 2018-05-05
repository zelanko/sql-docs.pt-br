---
title: Cursores | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6abebe52390c8c3423cd3c41f212236e051e1972
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="keyset-cursors"></a>Cursores
O cursor keyset fornece funcionalidade entre static e um cursor dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele não detectar sempre alterações para a associação e a ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta as alterações dos valores de linhas no conjunto de resultados.  
  
 Os cursores controlados por conjuntos de chaves são controlados por um conjunto de identificadores exclusivos (chaves), conhecido como o conjunto de chaves. As chaves são criadas a partir de um conjunto de colunas, que identificam exclusivamente as linhas no conjunto de resultados. O conjunto de chaves é o conjunto de valores de chave de todas as linhas retornadas pela instrução de consulta.  
  
 Com cursores controlados por conjuntos de chaves, uma chave é criada e salvo para cada linha do cursor e armazenada na estação de trabalho cliente ou no servidor. Quando você acessar cada linha, a chave armazenada é usada para buscar os valores de dados atuais da fonte de dados. Em um cursor controlado por, associação de conjunto de resultados está congelada quando o conjunto de chaves é totalmente preenchido. Depois disso, adições ou atualizações que afetam a associação não fazem parte do resultado definido até que ele é reaberto.  
  
 Alterações nos valores de dados (feitas por outros processos ou o proprietário de conjunto de chaves) são visíveis como rolagens do usuário por meio do conjunto de resultados. Inserções feitas fora do cursor (por outros processos) são visíveis apenas se o cursor for fechado e reaberto. Inserções feitas de dentro do cursor são visíveis no final do conjunto de resultados.  
  
 Quando um cursor controlado por tenta recuperar uma linha que foi excluída, a linha é exibida como um "buraco" no conjunto de resultados. A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha são atualizados, a linha é considerada foi excluído e, em seguida, inserir, portanto, essas linhas também é exibido como falhas no conjunto de resultados. Enquanto um cursor controlado por conjunto de chaves sempre pode detectar as linhas excluídas por outros processos, ele também pode remover as chaves de linhas, que ela é excluída. Os cursores controlados por conjuntos de chaves que isso não é possível detectar suas próprias exclusões porque a evidência foi removida.  
  
 Uma atualização para uma coluna de chave funciona como uma exclusão da chave antigo, seguida por uma inserção da nova chave. O novo valor de chave não é visível se a atualização não foi realizada pelo cursor. Se a atualização foi feita por meio do cursor, o novo valor de chave é visível ao final do conjunto de resultados.  
  
 Há uma variação os cursores controlados por conjuntos de chaves chamado controlado por cursores padrão. Em um cursor padrão por conjunto de chaves, a associação de linhas no conjunto de resultados e a ordem das linhas são fixas no tempo de abertura de cursor, mas as alterações aos valores que são feitas pelo proprietário do cursor e as alterações confirmadas feitas por outros processos estão visíveis. Se uma alteração de uma linha para a associação se enquadra nessa ou afeta a ordem de uma linha, a linha não desaparecem ou mova a menos que o cursor for fechado e reaberto. Dados inseridos não aparecem, mas as alterações nos dados existentes são exibidas como linhas buscadas.  
  
 O cursor controlado por conjunto de chaves é difícil de usar corretamente porque a sensibilidade a alterações de dados depende de muitas circunstâncias diferentes, conforme descrito acima. No entanto, se seu aplicativo não está preocupado com atualizações simultâneas, programaticamente pode lidar com chaves inválidas e deve acessar diretamente determinadas linhas com chave, o cursor controlado por pode funcionar para você. Use o **adOpenKeyset CursorTypeEnum** para indicar que você deseja usar um cursor de conjunto de chaves no ADO.  
  
## <a name="see-also"></a>Consulte também  
 [Cursores de somente avanço](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores dinâmicos](../../../ado/guide/data/dynamic-cursors.md)
